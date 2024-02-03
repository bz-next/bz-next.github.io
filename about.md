---
layout: page
title: About BZ-Next
subtitle: Modernizing BZFlag, Building New Tools for the Community
---

## What is it?

BZ-Next is an experimental fork of BZFlag that redoes the rendering engine from the ground-up, using modern OpenGL, and the Magnum graphics library.

A new renderer will open the doors to game UI improvements, development of new tools (map editors, admin tools), and, most importantly, custom shaders!
There should also be significant framerate improvements for most maps. Development versions of BZ-Next routinely break 1000fps in tests, and efficiency
is a key focus.

The BZ-Next project is already a full-featured BZFlag client. You can connect to a server, chat, watch the scoreboard, and inspect the map. Tanks, bullets,
effects and sounds will be added incrementally.

## Project philosophy (what this project isn't)

BZFlag is already a fun game. The purpose of this project is not to change gameplay, physics, or add new, breaking client and server features. Rather,
the goal is 100% compatibility with existing BZFlag infrastructure.

The goal of this project is not to overhaul the game UI (menus, UI layout, etc). That is a job best left to a UI-focused team. The UI developed
as part of this project has a few key purposes:

- To get the game into a playable, functional state with the new renderer
- To provide debug info and tools
- To serve as the basis for a map editor in the future

The new rendering engine will, however, enable developers to use modern UI development tools, which would make a UI overhaul for the game possible.

## What does it currently look like?

![Rats Nest by Winny](../assets/img/screen0.jpg)
Map: Rats Nest by Winny

![Urban Jungle by Army of One](../assets/img/screen1.jpg)
Map: Urban Jungle by Army of One

![Fairground](../assets/img/screen2.jpg)
Map: Fairground

## What's different about it
- It's much faster than the classic BZFlag client for real-world maps. Framerates can be 5-10x higher in the new client when compared to the old one.
- Modern OpenGL allows for custom shaders, which could allow shadow mapping, bloom, ambient occlusion, PBR, and other cool effects that could make maps look awesome.
- Wraps up legacy code in a new interface that allows access to map geometry, allowing developers to more easily build tools like map editors, viewers, custom clients, etc.
- Easy integration with modern UI toolkits, as well as debug toolkits like ImGui