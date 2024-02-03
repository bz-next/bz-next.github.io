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
- Install dependencies for the Windows build (GLEW, libpng, libtre, zlib, SDL2, OpenSSL, curl, c-ares, ...)
- Build using CMake
- Package resulting .exe along with necessary `.dll` files and program data.

```
# Install MinGW64 if you haven't already
# sudo dnf install mingw64-gcc mingw64-gcc-c++ mingw64-libstdc++

# Set this to your MinGW64 system root
export MINGW_PREFIX=/usr/x86_64-w64-mingw32/sys-root/mingw

$ mkdir mingw-libs-src
$ cd mingw-libs-src

$ wget https://c-ares.org/download/c-ares-1.26.0.tar.gz
$ tar -xf ./c-ares-1.26.0.tar.gz
$ cd c-ares-1.26.0/
$ mkdir build
$ cd build
$ mingw64-cmake -DCMAKE_PREFIX_PATH=$MINGW_PREFIX ..
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install

$ cd ../..

$ wget https://github.com/rockdaboot/libpsl/releases/download/0.21.5/libpsl-0.21.5.tar.gz
$ tar -xf ./libpsl-0.21.5.tar.gz
$ cd libpsl-0.21.5/
$ mingw64-configure --prefix=$MINGW_PREFIX
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install

$ cd ..

$ wget https://github.com/libsdl-org/SDL/releases/download/release-2.28.5/SDL2-2.28.5.tar.gz
$ tar -xf ./SDL2-2.28.5.tar.gz
$ cd SDL2-2.28.5/
$ mingw64-configure --prefix=$MINGW_PREFIX
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install -j$(nproc)

$ cd ..

$ wget https://sourceforge.net/projects/glew/files/glew/2.1.0/glew-2.1.0.tgz/download -O glew-2.1.0.tgz
$ tar -xf ./glew-2.1.0.tgz
$ cd glew-2.1.0/build/cmake
$ mkdir build
$ cd build
$ mingw64-cmake -DCMAKE_PREFIX_PATH=$MINGW_PREFIX ..
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install

$ cd ../../../..

$ # Need zlib for libpng
$ wget https://www.zlib.net/zlib-1.3.1.tar.gz
$ tar -xf ./zlib-1.3.1.tar.gz
$ cd zlib-1.3.1/
$ mkdir build
$ cd build
$ mingw64-cmake -DCMAKE_PREFIX_PATH=$MINGW_PREFIX ..
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install

$ cd ../..

$ wget http://prdownloads.sourceforge.net/libpng/libpng-1.6.41.tar.gz?download -O libpng-1.6.41.tar.gz
$ tar -xf ./libpng-1.6.41.tar.gz
$ cd libpng-1.6.41/
$ mkdir build
$ cd build
$ mingw64-cmake -DCMAKE_PREFIX_PATH=$MINGW_PREFIX ..
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install

$ cd ../..

# Need perl for the OpenSSL install, get it if you don't have it yet
$ sudo dnf install perl

# Need OpenSSL for curl
$ wget https://www.openssl.org/source/openssl-3.0.13.tar.gz
$ tar -xf ./openssl-3.0.13.tar.gz
$ cd openssl-3.0.13/
$ ./Configure mingw64 --cross-compile-prefix=x86_64-w64-mingw32- --prefix=$MINGW_PREFIX --openssldir=$MINGW_PREFIX
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install -j$(nproc)

$ cd ..

$ wget https://curl.se/download/curl-8.6.0.tar.gz
$ tar -xf ./curl-8.6.0.tar.gz
$ cd curl-8.6.0/
$ mkdir build
$ cd build
$ mingw64-cmake -DCMAKE_PREFIX_PATH=$MINGW_PREFIX -DCURL_USE_OPENSSL=ON ..
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install -j$(nproc)

$ cd ../..

# Need autopoint installed to install tre
# sudo dnf install gettext-devel

# Need libtool to install tre
# sudo dnf install libtool

# Need tre for systre
$ git clone https://github.com/laurikari/tre.git
$ cd tre
$ ./utils/autogen.sh
$ mingw64-configure --prefix=$MINGW_PREFIX --enable-static
$ mingw64-make -j$(nproc)
$ sudo mingw64-make install -j$(nproc)

$ cd ..

$ wget https://github.com/msys2/MINGW-packages/raw/master/mingw-w64-libsystre/systre-1.0.1.tar.xz
$ tar -xf ./systre-1.0.1.tar.xz
$ cd systre-1.0.1/
$ mingw64-configure --prefix=$MINGW_PREFIX
$ sudo mingw64-make -j$(nproc)
$ sudo mingw64-make install -j$(nproc)

$ cd ..

# Finally, we need corrade-rc from corrade for resource-packaging in bz-next
# It has to be a locally-runnable executable, it's used during the build process
# I assume you want to install it to $HOME/.local/bin
# Whereever it gets installed, it should be on your $PATH
$ git clone https://github.com/mosra/corrade.git
$ cd corrade
$ mkdir build
$ cd build
$ cmake -DCMAKE_INSTALL_PREFIX=$HOME/.local ..
$ make -j$(nproc)
$ make install

# We need to fixup tre's install, since gcc can't find it by default
$ cd $MINGW_PREFIX/lib
$ sudo cp ./libtre.dll.a ./libtre.a
```

Now we are finally tooled up to build the client.

```
$ git clone https://github.com/bz-next/bz-next.git
$ cd bz-next

# Currently, we have a branch called mingw-test where the cmake has been hacked
# for a Windows build. This will be cleaned up and merged in the future.
$ git checkout mingw-test
$ git submodule update --init --recursive

mkdir build
cd build

# Just build the client. Builds for other targets might be broken
$ mingw64-cmake -DENABLE_BZADMIN=FALSE -DENABLE_SERVER=FALSE -DENABLE_ROBOTS=FALSE -DENABLE_PLUGINS=FALSE -DCMAKE_BUILD_TYPE=Release ..

# Build
$ mingw64-make -j$(nproc)
```

To make a distribution, copy the files from `Release/bin/` to a new directory. Copy the `data` directory from the main source dir as well.
Finally, we need to package the `.dll` files that Windows users will need to run the program. A quick fix is to just copy all the `.dll` files
from `$MINGW_PREFIX/bin` to your distribution:

```
cp $MINGW_PREFIX/bin/*.dll .
```