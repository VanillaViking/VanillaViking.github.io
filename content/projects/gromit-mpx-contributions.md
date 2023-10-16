---
title: "Gromit Mpx Contributions"
date: 2023-10-16T17:57:44+11:00
description: "Fast on-screen annotating tool"
featured_image: '/projects/gromit-mpx0.png'
---

<!--more-->

> [Github repository](https://github.com/bk138/gromit-mpx)

My original need was a tool that I could use to take notes anywhere on screen. Gromit-mpx came very close, but was just missing some features to fully satisfy my use case. I decided to dive into the source code and see if I could tweak it to my needs, which resulted in [Gromit-notes](/projects/gromit-notes). 

After playing around with the codebase, I think it is only fair that I give back by also making a contribution to gromit-mpx itself.

## Draw lines command

> [Pull Request](https://github.com/bk138/gromit-mpx/pull/180)

This PR adds the ability to draw lines on the screen with gromit using the command line. This unlocks quite a bit of automation features by using shell scripts.

```bash
gromit-mpx --line <startX> <startY> <endX> <endY> <color> <thickness>
    will draw a straight line with characteristics specified by the arguments (or "-l")
    eg: gromit-mpx -l 200 200 400 400 '#C4A7E7' 6	
```
