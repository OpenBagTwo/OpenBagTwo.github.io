---
author: Gili "OpenBagTwo" Barlev
title: "Developing for elementary OS the Hard Way"
description: "Because I use Arch, btw"
tags: ["elementary os", "linux", "arch", "vala"]
date: 2023-10-23
thumbnail: /hello-vala.png
---

I'm a Stan for [elementary OS](https://elementary.io/). People say that it's a macOS clone for Linux, and I'll loudly tell them that they're wrong--
it's an _OSX_ clone for Linux, and that is a different thing entirely. But while I love the look and feel of the Pantheon desktop environment,
and I was, for a decade and a half, a "`.deb` or Die" Ubuntu-variant devotee, I ended up switching to Arch (+ Pantheon) on my main workstation about
a year ago.

Today I decided I'd like to try designing a GUI app for the first time since undergrad, and while, thanks to Flatpak, I could choose from one of dozens
of toolkits, I'm going with [Granite](https://github.com/elementary/granite) because I want this to be an _elementary OS_ application first and foremost.

Obviously, the [elementary OS developer guides](https://docs.elementary.io/develop/) weren't written for my particular setup, so this post is serving to
document what I did for anyone else who chooses ~~insanity~~ to walk down a similar path.


## Of course there's no `elementary-sdk` package in the AUR

_Though wouldn't that have been nice!_

Of course, `elementary-sdk` is just a metapackage anyway,

![screenshot showing the contents of the elementary-sdk metapackage](/elementary-sdk.png)

and I could just hunt down each metapackage member, but hitting this barrier did make me stop and think: "Wait, why would I install an entire development
environment onto my base system?" I wouldn't do that for a _Python_ project--I'd use a [conda](https://docs.conda.io/) environment. So why wouldn't I do
that here?

### Solution: Install [Distrobox](https://github.com/89luca89/distrobox)

Honestly, I'm more surprised that I've gone this long without using it.

There's no base elementary OS container, but an Ubuntu 22.04 one should work fine with the added PPAs:

```bash
$ distrobox create -n elementary-dev -i ubuntu:22.04
$ distrobox enter elementary-dev
openbagtwo@elementary-dev $ sudo apt update && sudo apt dist-upgrade
openbagtwo@elementary-dev $ sudo apt install software-properties-common
openbagtwo@elementary-dev $ sudo add-apt-repository https://ppa.launchpadcontent.net/elementary-os/stable/ubuntu
openbagtwo@elementary-dev $ sudo apt update
openbagtwo@elementary-dev $ sudo apt install elementary-sdk
```

And that worked a charm!

## Flatpak And Containers Don't Mix

Following along in [the developer guide](https://docs.elementary.io/develop/writing-apps/the-basic-setup#flatpak),
the next step was to install the elementary appcenter flatpak.

That failed spectacularly inside of my dev instance with the very unhelpful error:

```
error: No such file or directory
```

which took me a minute to track down to
[a known limitation of Flatpak](https://github.com/flatpak/flatpak/issues/5076#issuecomment-1236410300):
running them inside of containers is [a little too meta](https://imgflip.com/memegenerator/Yo-Dawg-Heard-You)
for them.

### Solution: Install appcenter on the system

And honestly, having the elementary Flathub repo available on my system is something I want regardless.

```bash
$ flatpak remote-add --if-not-exists --system appcenter https://flatpak.elementary.io/repo.flatpakrepo
$ flatpak install -y appcenter io.elementary.Platform io.elementary.Sdk
```

(I chose the newest available runtimes, which were one point release ahead of the current)

## Hello World!

And now, finally, it was time to write [my first Vala app](https://docs.elementary.io/develop/writing-apps/hello-world).

![my first Vala app, with the title changed from the example](/hello-vala.png)

Some notes:

- I thought for sure I'd need something like [syncthing](https://syncthing.net/) to make my files available inside
  the container, but nope--the container had access to the files in my current directory automagically!
- On the flip side, I needed to "enter" the container from the project directory (couldn't `cd` there from `~`),
  and I needed to have `cd`'d to the _absolute_ / resolved path (my "Workspaces" directory is actually a symlink
  pointing to a different drive, and distrobox didn't know how to work with that).
- While the container could be used to compile the project, the actual GUI application needed to be run from the _host_

For ease of copy-pasting, here's the commands I used to compile and run my first Vala app:

```bash
$ cd /path/to/workspace/vala-project
$ mkdir -p build
$ distrobox enter elementary-dev
openbagtwo@elementary-dev $ valac --pkg gtk4 src/Application.vala -o build/Application
openbagtwo@elementary-dev $ logout
$ ./build/Application
```

## Granite and meson

So far my application has just been a bog-standard GTK4 app, but the whole point of this exercise was to build something
for _elementary._ Some of the high-level concepts are covered [here](https://docs.elementary.io/develop/writing-apps/our-first-app/the-build-system)
but at this point I was better served by just copying and modifying `meson.build` files from
[a template project](https://github.com/elementary/calculator).

The big thing was switching over to using [GObject-style construction](https://docs.elementary.io/develop/writing-apps/code-style/class-construction)
so the top of my program now looks like:

```vala
public class EnderChest.Application : Gtk.Application {
    construct {
        application_id = "com.github.openbagtwo.babys-first-vala";
        flags = ApplicationFlags.FLAGS_NONE;
    }
...
```

I also copied over their [startup() method](https://github.com/elementary/calculator/blob/98085d8774aa4b4f10a2f3f6d5f67386d7838ae0/src/Application.vala#L32-L57)
which sets the application styling and registers Ctrl-Q as a keyboard shortcut to quit.

With those changes made and files in place, I hopped back into my distrobox container and ran:

```
$ cd /path/to/workspace/vala-project
$ distrobox enter elementary-dev
openbagtwo@elementary-dev $ meson build --prefix=/usr
openbagtwo@elementary-dev $ cd build
openbagtwo@elementary-dev $ ninja
openbagtwo@elementary-dev $ logout
$ ./build/src/com.github.openbagtwo.enderchest-gui
```

which looks the same as before, but now closes with Ctrl-Q.

## Next Steps

The project I'm working towards is a frontend for [EnderChest](https://openbagtwo.github.io/EnderChest)
and [GSB](https://openbagtwo.github.io/GSB), and there's a lot I don't know about how to integrate a Python
backend with a GUI frontend written in a completely different language (without resorting to just calling the CLI
in between). Ahead of me is a fun journey of learning about [ABIs](https://en.wikipedia.org/wiki/Application_binary_interface)
and [GObject Introspection](https://gi.readthedocs.io/en/latest/)!
