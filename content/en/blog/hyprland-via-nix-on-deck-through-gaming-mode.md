---
author: Gili "OpenBagTwo" Barlev
title: "I got a Tiling WM working on SteamOS in Gaming Mode"
description: "Ask me anything"
tags: ["steam deck", "linux", "wayland", "nix", "hyprland"]
date: 2023-11-19
thumbnail: /hyprland-on-nix-on-deck.jpg
---

***[https://holo-shed.github.io/dev-diary/04-holoshed-on-the-deck/](https://holo-shed.github.io/dev-diary/04-holoshed-on-the-deck/)***

The one thing I have disliked most about SteamOS is that Desktop Mode
and Gaming Mode are two separate sessions, where you essentially have
to _restart_ your Deck to switch from one to the other.

The second thing that's ground my gears is how hard it is to customize
the software on the Deck because of its read-only file system.

That why I was so excited about Steam OS 3.5 enabling Nix packages,
pretty much out of the box. The link above is my "diary" of how I safely
set up Hyprland, a Wayland-first tiling Window Manager, on my Steam Deck, as a
"non-Steam game," thus ensuring that I pretty much never have to boot to
"desktop mode" ever again.
