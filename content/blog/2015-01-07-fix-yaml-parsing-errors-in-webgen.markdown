---
layout: post
title: "Fix YAML parsing errors in WebGen"
date: 2015-01-07 12:20:34 -0500
type: posts
tags:
---
After a clean install of Mac OS X Yosemite I've had to reinstall much of my development environment. This process was mostly beneficial as I moved to the latest and greatest tooling but several of my static websites leverage the prior major version of [Thomas Leitner's Webgen](http://webgen.gettalong.org/index.html) and getting version 0.5.x up and running has been a challenge.

After working through several Ruby & Gem issues I ran into a particularly opaque error when executing webgen on a project that previously generated without issue: "(<unknown>): found character that cannot start any token while scanning for the next token"

This error is usually a sign that your content contains tab characters but I'd already ensured that wasn't the case.  Instead of diving deep into the workings of the libraries at play I was able to use [this post from Thomas to resolve the issue](https://groups.google.com/d/msg/webgen-users/wYYWrwljJ1Y/Q8G4SzG_lEcJ) by reverting to the syck TAML implementation instead of its replacement.  Problem solved!
