---
author: Gili "OpenBagTwo" Barlev
title: "Game Save Backup"
description: "more than a vanity backronym"
tags: ["python", "git", "gaming", "backups", "pygit2", "click"]
date: 2023-08-09
thumbnail: /gsb.png
---

***[https://openbagtwo.github.io/gsb/](https://openbagtwo.github.io/gsb/)***

This is an idea that
[dates back over a year and a half](https://github.com/OpenBagTwo/AngerLocalBeehive/issues/2)
to when I was ~~doing stupidly
risky things~~ being experimental in my Minecraft surival world and getting frustrated
at just how long and painful it was to create—and later restore—backups of my world.

Incremental backups definitely seemed like the way to go, but the main version control
system I was familiar with was [Git](https://git-scm.com/), and isn't that kind of overkill
for this situation? Especially when I'm dealing with large binary blobs?

Well, after 18 months of dogfooding, the conclusion I reached was **no!** Git is actually
really great at quickly generating snapshots of my ~7GB of world files*, and it's been
pretty great, not just for pretending like I *didn't* just fall into the void and lose all
my enchanted gear, but also for rewinding to a backup I took months or years ago, recording
some footage or poking around in an old world, and then fast forwarding back to the present.

This workflow also integrates _really well_ with [EnderChest](../enderchest), as I have a "chest"
set up on a single file server with a lot of disk space where I can keep my backups centralized,
pushing out restores to any specific instances I want to check them out on.

The one thing that _wasn't_ working out about my git-based backup scheme was **explaining it to others**.
I'd be interacting with people frustrated with Steam deleting their cloud saves and telling them,
"why not just manage it yourself with Git?" and they'd remind me _just how intimidating_ Git can
be for newcomers. So that was the persona I had in mind, first in foremost, when developing what is
essentially little more than [yet another Git wrapper](https://gitless.com/) (I did actually
consider whether `gitless` would do what I wanted but concluded that there was still a niche
for a tool to directly cater to the gamesave backup workflow).

As it stands, `gsb`
[just hit](https://github.com/OpenBagTwo/gsb/releases/tag/v0.0.2) "steel thread" pre-MVP status today
with four operations:

1. `gsb init` is the equivalent of `git init` while also performing the first backup
1. `gsb backup` runs `git add . && git commit` (and optionally a `git tag` at the end)
1. `gsb history` is a friendly summation of one's `git history`
1. `git rewind` restores a backup via a combination of `git reset`s, `git checkout`s and `gsb backup`s in
   order to keep the history nice and linear

I've got plenty of roadmap ahead (including direct integration with [EnderChest](../enderchest), and this
might be the project that finally gets me to make a GUI so that this can _really_ find an audience
on [platforms](https://store.steampowered.com/steamdeck/) where
[typing in commands](https://rog.asus.com/gaming-handhelds/rog-ally/rog-ally-2023/)
is just a pain in the toucans.


_*After 18 months and 424 revisions, my `.git` folder is sitting at 48GB in size, which probably mainly means I could do with some [interactive rebasing](https://github.com/OpenBagTwo/gsb/issues/9)_

## Installation

The `gsb` package is available on [PyPI](https://pypi.org/project/gsb/)

Full installation instructions can be found on
[GitHub Pages](https://openbagtwo.github.io/gsb/release/installation),
though I've recently discovered the joys of [pipx](https://pypa.github.io/pipx/)
and honestly might switch to using it for everything!

## License

This project--the executable, source code and all documentation--are published
under the
[GNU Public License v3](https://github.com/OpenBagTwo/gsb/blob/dev/LICENSE).
