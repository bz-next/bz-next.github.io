---
layout: post
title: WebGL Mapviewer Demo Online
subtitle: Supporting WebGL in BZ-Next
gh-repo: bz-next/bz-next
gh-badge: [star, fork, follow]
tags: [Site Updates]
comments: true
---

A WebGL map viewer demo app is online at [https://bz-next.github.io/mapviewer/mapviewer.html](https://bz-next.github.io/mapviewer/mapviewer.html)

![Map Viewer Demo](/assets/img/mapviewer1.jpg)

Currently the online demo can't access any textures that aren't bundled with the game, so try it on maps that don't use custom textures.
Meshes and so on should work fine, however. If you load a map that uses non-standard textures, those objects will appear white, and the app will lag a bit as it will output a bunch of errors in the background.

In the future, I'll upload the textures for some popular maps, so that those will appear properly in the app.

The map viewer can also be built for desktop, where it can load any textures from images.bzflag.org that it likes.

![Desktop Demo](/assets/img/mapviewer2.png)

Try it out if you're curious!

The real power of the Magnum graphics library is being able to support web, mobile, and desktop all from the same codebase, so you can have one codebase that generates apps for all the various targets at the same time. This is a basic demo of getting something building from the BZFlag codebase that targets both WebGL and desktop.

I'll add the desktop version of the map viewer to the next Windows release. It could be a handy tool for previewing maps quickly.