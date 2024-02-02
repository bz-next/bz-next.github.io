---
layout: page
title: Building
---

# Building the source code on Linux

The following instructions are for Fedora 39. If using another distro, package names and package install procedure may be different, but the overall process should be the same.

### Install development tools

```
$ sudo dnf groupinstall "Development Tools"
$ sudo dnf install cmake g++ mesa-libGL-devel mesa-libGLU-devel SDL2-devel libpng-devel curl-devel c-ares-devel glew-devel ncurses-devel
```

### Clone repository and populate submodules

```
$ git clone https://github.com/bz-next/bz-next.git
$ cd bz-next
$ git submodule update --init --recursive
```

### Make a directory to contain build stuff

```
$ mkdir build
$ cd build
```

### Run cmake to configure the build

Specify any build options here. You can build a release build (more optimized) by specifying `-DCMAKE_BUILD_TYPE=Release` instead of `Debug`. `-DCMAKE_EXPORT_COMPILE_COMMANDS=On` generates a `compile-commands.json` that can be fed to `clangd` for editor instrumentation.

The following will build a debug build, and disable the server, bzadmin, and clients:

```
$ cmake -DCMAKE_EXPORT_COMPILE_COMMANDS=On -DCMAKE_BUILD_TYPE=Debug -DENABLE_CLIENT=TRUE -DENABLE_SERVER=FALSE -DENABLE_PLUGINS=FALSE ..
```

### Run make

```
$ make -j$(nproc)
```

### Running the client

The client looks for textures in `/data` from the directory from which it is run. It's best to execute the client from the main repo directory so that it can find everything it needs.

```
$ cd ..
$ build/Debug/bin/bzflag-next
```

If you built a Release client, the path would be `build/Release/bin/bzflag-next`

# Cross-compiling for Windows from Linux using MinGW64

It is possible to build a windows release completely from Linux, using MinGW64. The rough steps are:

- Install MinGW64
- Install dependencies for the Windows build (GLEW, libpng, regex, libtre, zlib, SDL2, OpenSSL, curl, c-ares)
- Build using CMake
- Package resulting .exe along with necessary `.dll` files.
