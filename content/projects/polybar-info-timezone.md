---
title: "Polybar Timezone Module"
date: 2023-04-16T11:55:14+11:00
description: "A date module for polybar which can cycle through different timezones"
featured_image: '/projects/timezone0.webp'
---

<!--more-->

This was a neat little script that I cooked up for myself originally. I found scheduling tounaments to be difficult because I need to constantly swap back and fourth between AEST and some other timezone. This was error-prone and quite annoying, and has cost me some matches in the past.

The script here aims to solve that in a simple way. When I click the time on my status bar, it should switch to a different timezone. In my case, I want it to cycle between Australian, Indian and UTC timezones, since those are most common in the tournaments that I participate in. 

After a bit of tinkering, I came up with [this script](https://github.com/polybar/polybar-scripts/tree/master/polybar-scripts/info-timezone)

![timezone switcher](/projects/tz.gif)

To get started, follow the instructions on the main page of the repository, or here's a quick summary:

* Copy the script somewhere into your computer and make it executable with `chmod +x info-timezone.sh`
* Enter the timeones that you want inside the script
* Copy the following example configuration into your polybar config file:
```ini
[module/info-timezone]
type = custom/script
exec = ~/polybar-scripts/info-timezone.sh
tail = true
click-left = kill -USR1 %pid%
```


Also check out the other scripts in the [polybar scripts repository](https://github.com/polybar/polybar-scripts/). There are tons of different modules so you are bound to find something useful.

