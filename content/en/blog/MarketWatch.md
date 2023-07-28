---
author: Gili "OpenBagTwo" Barlev
title: "Financial Headline Generator"
description: "Taking a silly idea way too far"
tags: ["python", "The Guardian", "api", "Hugo", "SMBC Comics", "humor"]
date: 2023-07-27
thumbnail: /MarketWatch.png
---

***[https://openbagtwo.github.io/MarketWatch/](https://openbagtwo.github.io/MarketWatch/)***

I woke up this morning, as am I am wont to do, was randomly wandering through the [SMBC](https://www.smbc-comics.com) archive
when I came across [this webcomic](https://www.smbc-comics.com/comic/markets) from 2020:

![SMBC Markets](https://www.smbc-comics.com/comics/1592665375-20200620.png)

and I thought to myself, "Hey, I bet I could code that pretty easily!"

[which is exactly what I did.](https://openbagtwo.github.io/MarketWatch/)


## How does it work?

The two components going into this work were:

- getting market data (is the market up or down on any given day?)
- getting news headlines

I figured the first would be easy and the second would be hard, but the reverse ended up being true,
as most Finance APIs I could find were either decommissioned (Google), paid (NASDAQ DataLink) or
didn't contain composite indices (Alpha Vantage). Luckily, not only is [Yahoo Finance](https://finance.yahoo.com)
still around, but there's even a well-maintained Python package called [`yfinance`](https://aroussi.com/post/python-yahoo-finance)
that I could use without even creating a developer account!

On the news side, I found [this handy list of news media APIs](https://en.wikipedia.org/wiki/List_of_news_media_APIs) and decided to go with
[The Guardian](https://open-platform.theguardian.com/). Their documentation was excellent and their API was extremely easy
to use.

If you'd like to get a deeper look at how I combined the two halves, the code, as always,
[is freely available on GitHub,](https://github.com/OpenBagTwo/MarketWatch/) where you can find
[the development notebook](https://github.com/OpenBagTwo/MarketWatch/blob/d4a93f49243e5b85f67d649edd1efe0f08e5f97e/Development%20Notebook.ipynb)
I used to prototype everything in addition to [the script that generates the posts](https://github.com/OpenBagTwo/MarketWatch/blob/main/post_generator.py).

The project is licensed under the _Affero_ GPL this time, because if anyone out there wants to serve this ridiculously stupid content,
they should be making the source code readily available.
