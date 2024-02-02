---
layout: page
title: Building
---

# Building the source code on Linux

In order to build BZ-New, you will need:
- OpenGL Support
- LibPNG
- The c-ares library
- libcurl
- CMake

```
git clone ...
cd bzflag-experiments
git checkout magnum-experiment
git submodule update --init --recursive
mkdir build
cd build
cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=On -DCMAKE_BUILD_TYPE=Debug ..
make -j$(nproc)
```

# Cross-compiling for Windows from Linux using MinGW64

It is possible to build a windows release completely from Linux, using MinGW64. The rough steps are:

- Install MinGW64
- Install dependencies for the Windows build (GLEW, libpng, regex, libtre, zlib, SDL2, OpenSSL, curl, c-ares)
- Build using CMake
- Package resulting .exe along with necessary `.dll` files.
