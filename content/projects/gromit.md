---
title: "Gromit Notes"
date: 2023-10-01T11:55:14+11:00
description: "Fork of gromit-mpx that provides save functionality"
featured_image: '/projects/gromit0.png'
---

<!--more-->

[Gromit-mpx](https://github.com/bk138/gromit-mpx) is primarily designed to be a on-screen annotation tool useful for highlighting things during presentations. However due to its quick and easy hotkeys, it also showed potential as a basic note taking tool. This fork of gromit-mpx aims to give you full freedom to sketch anything anywhere on your desktop, and persist those notes between launches. 

> [Github repository](https://github.com/VanillaViking/gromit-notes)

## Features of Gromit-notes

**Non root window**

Since gromit-notes somewhat moves away from gromit-mpx's original goal of being a screen annotation tool, It is no longer necessary for its transparent annotation window to be drawn on top of other application windows. Instead, it simply provides for a way to write things onto your desktop, while also not interefering with other tasks. Therefore, gromit-notes initialises the window with `GTK_WINDOW_TOPLEVEL`, instead of `GTK_WINDOW_ROOT`.

**F10 to save**

Gromit notes adds a save keybind, which very simply saves the strokes on screen to PNG file in your config folder. A notification is also sent through the default notification daemon on the system (Linux only). The next time you load the application, it will check for this file and attempt to load the strokes from it, giving you persistent data.

