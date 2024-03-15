---
layout: post
title: Shaders and Shadows
subtitle: Flexible rendering pipeline
gh-repo: bz-next/bz-next
gh-badge: [star, fork, follow]
tags: [Site Updates]
comments: true
---

The client now supports a more flexible render pipeline, which can incorporate arbitrary shaders.

Basic shadow mapping is implemented. An improvement over the old renderer, objects can now cast shadows on arbitrary geometry.

As a demo, there is also a simple ray-marching cloud and atmosphere shader.

The sun position can be set using an ImGUI widget.

![Embedding of scene in shader skydome](/assets/img/embed.jpg)
Embedding of scene in shader skydome

![Urban jungle with clouds and shadows](/assets/img/urbanclouds.jpg)
Urban Jungle with Clouds and Shadows

![Gameplay](/assets/img/mf_clouds.jpg)
Gameplay demo

