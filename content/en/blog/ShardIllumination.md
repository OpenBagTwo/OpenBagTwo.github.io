---
author: Gili "OpenBagTwo" Barlev
title: "HelloNeoPixel"
description: Code for illuminating "shards" of acrylic glass.
tags: ["arduino", "cnc"]
date: 2020-06-20
thumbnail: /TooShrill.png
---

***[https://github.com/OpenBagTwo/HelloNeoPixel](https://github.com/OpenBagTwo/ShardIllumination)***

During the pandemic I bought a
[tabletop CNC machine](https://www.sainsmart.com/products/sainsmart-genmitsu-cnc-router-3018-pro-diy-kit),
and I am completely in love with it. One of the first projects I attempted after
setting up my CNC was a disk of acrylic glass, engraved with a picture of an
[Oddish](https://bulbapedia.bulbagarden.net/wiki/Oddish_(Pok%C3%A9mon)), Oddishes
being my five-year-old's second favorite thing in the universe. His first favorite?
LEDs. So hey, why not combine the two?

This repo contains several sketches that perform variations on lighting up RGB
LEDs (uniform color, as opposed to individually addressible), with the intent
being that the LEDs lie in a channel inside a base holding a piece of acrylic glass.

This isn't a terribly [novel](https://www.youtube.com/watch?v=kgPghSJhkzU)
[idea](https://www.youtube.com/watch?v=697cEhHvYZk), but I had my own twist to add.
You know that obnoxiously loud person in the office who you can hear three floors down,
even when they're talking at their "normal" volume? It me. So when I saw
[this tweet](https://twitter.com/EffinBirds/status/1271819657608155136) from
[@effinbirds](https://twitter.com/EffinBirds), I knew I needed that image engraved,
mounted, and configured to flash any time my voice exceeded a certain decibel.

## Project Variants

The variants provided in this repo are:

- [DemoIllumination](https://github.com/OpenBagTwo/ShardIllumation/blob/main/DemoIllumination/DemoIllumination.ino), which cycles through a
  palette of nine colors in sequence
- [MappingTest](https://github.com/OpenBagTwo/ShardIllumation/blob/main/MappingTest/MappingTest.ino), for trying out a continuous color
  palette
- [MicCalibrate](https://github.com/OpenBagTwo/ShardIllumation/blob/main/MicCalibrate/MicCalibrate.ino), for calibrating the input coming
  from a microphone input
- [IndoorVoice](https://github.com/OpenBagTwo/ShardIllumation/blob/main/IndoorVoice/IndoorVoice.ino): illuminates the shard based on an
  analog signal from a microphone
- [TooShrill](https://github.com/OpenBagTwo/ShardIllumation/blob/main/TooShrill/TooShrill.ino): the most complex variant, where the illumination
  color and intensity is a function of an amplified microphone signal, sent through a
  high-pass filter
