---
author: Gili "OpenBagTwo" Barlev
title: "EnderChest"
description: "Syncing and Linking for All Your Minecraft Instances"
tags: ["minecraft", "rsync", "symlink", "python"]
date: 2023-06-14
thumbnail: /EnderChest.png
---

***[https://openbagtwo.github.io/EnderChest/](https://openbagtwo.github.io/EnderChest/)***

## In a Nutshell

EnderChest is a command-line utility for selectively sharing Minecraft assets
(configurations, mods, worlds, etc.)...

1. ...across different computers
1. ...across different instances on the same computer
1. ...across server and client installations

### A Note On Linking

Starting with Minecraft 1.20, Mojang by default
[no longer allows worlds to load if they are or if they contain symbolic links](https://help.minecraft.net/hc/en-us/articles/16165590199181).
While it is true that an improper symlink could cause Minecraft to write data
to a place it shouldn't, nothing in EnderChest will ever generate a symlink whose
target is outside of your EnderChest folder _unless you place_ a symbolic link in
your EnderChest pointing to somewhere else (which you may want to do so that your
screenshots, for example, point to your "My Pictures" folder).

## Installation

EnderChest is available on [PyPI](https://pypi.org/project/enderchest/)

Full installation instructions can be found on
[GitHub Pages](https://openbagtwo.github.io/EnderChest/dev/installation).

## License

This project--the executable, source code and all documentation--are published
under the
[GNU Public License v3](https://github.com/OpenBagTwo/EnderChest/blob/dev/LICENSE).
