---
layout: post
title: WebGL2 Map Editor Prototype Online
subtitle: WebGL2 Map Editor / Viewer
gh-repo: bz-next/bz-next
gh-badge: [star, fork, follow]
tags: [Site Updates]
comments: true
---

A fairly full-featured map viewer/editor is now online at [https://bz-next.github.io/mapviewer3/mapviewer.html](https://bz-next.github.io/mapviewer3/mapviewer.html)

![Map Viewer Demo](/assets/img/mapedit.png)

The online editor/viewer can fetch textures from images.bzflag.org using the Emscripten fetch API and CORS.

You can open the editor (found under the view menu), and tweak the currently loaded BZW file. Then, click "Update 3D View" and see your changes in the 3D view.

When you're satisfied, click "Save" in the editor, and it will download a copy of the edited map.

Textures from other sources will not load in the online viewer. A desktop release will be made available that does not have this limitation.
