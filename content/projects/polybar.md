---
title: "Polybar Contributions"
date: 2022-10-26T11:55:14+11:00
description: "A fast and easy to use tool for creating status bars"
featured_image: '/projects/polybar0.webp'
---

<!--more-->

Looking for ricing up your linux desktop? Polybar is *the* status bar that'll start you off. I fell in love with polybar when I discovered how customisable it can really be with custom scripts. Naturally, this was the project that I chose to make my first open source contirbutions to.

Contributions
----------

> **Option to turn off Struts**
>
> 22nd October, 2022
>
> [#2844](https://github.com/polybar/polybar/pull/2844)
>
> Setting option `enable-struts` to false in bar settings turns off struts.

> **Negative minimum length adds right padding**
>
> 24th August, 2022
>
> [#2801](https://github.com/polybar/polybar/pull/2801)
>
> Providing a minimum length to a token adds padding to the **left** if the token is not as big as the minimum length. This feature allows the user to enter a negative number for padding, which will add padding to the **right** instead of left.

> **xwindow module crash fix**
>
> 5th October, 2022
>
> [#2833](https://github.com/polybar/polybar/pull/2833)
>
> Not providing a tag to xwindow used to crash the whole bar. This bug fix ensures that no tag needs to be passed.
