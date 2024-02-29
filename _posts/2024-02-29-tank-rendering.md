---
layout: post
title: Tank Rendering and Animation
subtitle: Drawing player tanks in new renderer
gh-repo: bz-next/bz-next
gh-badge: [star, fork, follow]
tags: [Site Updates]
comments: true
---

The client can now render animated player tanks. Tread and wheel animation, explosions, and resizing (squish factor, flags like tiny/narrow/thief etc) are supported.

You can now watch much of an in-progress game through the client.

Tanks use the main material manager for all materials, for uniformity with other code.

![Tanks](/assets/img/tanks.png)
Tank Rendering Demo