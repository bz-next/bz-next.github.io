---
layout: post
title: Mesh generation cleaned up
subtitle: Memory and CPU reduction
gh-repo: bz-next/bz-next
gh-badge: [star, fork, follow]
tags: [Site Updates]
comments: true
---

The world mesh generation code was cleaned up a bit, yielding significant memory savings, and a speedup as well.

In certain cases (involving drawinfo meshes), the old code would copy much more data per mesh than was necessary.