---
author: Gili "OpenBagTwo" Barlev
title: Head Hunter
description: Scripts for Customizing VanillaTweaks' Wandering Trades data pack
tags: ["minecraft", "datapack", "vanillatweaks", "hermitcraft"]
date: 2023-06-21
thumbnail: /head-hunter.png
---

***https://OpenBagTwo.github.io/head-hunter***

A package for customizing [Vanilla Tweaks\'](https://vanillatweaks.net)
[Wandering Trades data pack](https://www.youtube.com/watch?v=L3En7cuOdHY) to stock
[everyone\'s favorite](https://www.youtube.com/shorts/tbkQ-IXRdbs) [ex-nitwit](https://www.youtube.com/watch?v=tVA8eNh7VWs)
with your own personalized list of custom player heads.

## Functionality

This package is compatible with Python 3.8 or newer and consists of four modules:

1. `extract`, which extracts files from existing data packs
1. `parse`, which parses head configurations from data pack functions and `/give` commands
1. `write`, which write the various data pack files
1. `release`, which bundles everything up into a handy zip file

You can grab information about the methods in each module using the
[help()](https://docs.python.org/3/library/functions.html#help)
function, or you can browse [the API documentation online](https://openbagtwo.github.io/head-hunter/reference/head_hunter/).

There's also a handy [end-to-end tutorial](https://openbagtwo.github.io/head-hunter/Tutorial) that you can even run interactively
in [Jupyter](https://jupyter.org/).

## License

The `head_hunter` package and its contents are licensed under [the GNU Public License v3](https://github.com/OpenBagTwo/head-hunter/blob/main/LICENSE). Any data packs produced
by this package must be licensed under [Vanilla Tweaks' terms of use](https://github.com/OpenBagTwo/head-hunter/blob/main/Head%20Hunter/credits.txt).
