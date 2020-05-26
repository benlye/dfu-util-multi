# dfu-util-multi
Customised version of dfu-util for Flash Multi.  Forked from https://sourceforge.net/p/dfu-util/dfu-util/ci/v0.7/tree/.
 
## Build Instructions
http://dfu-util.sourceforge.net/build.html

### Building on Windows using MinGW-w64 from MSYS2
This assumes using release tarballs or having run ./autogen.sh on the git sources.

First install MSYS2 from the [MSYS2 installer home page](https://www.msys2.org/).

To avoid interference from other software on your computer, set a clean path in the MSYS window before running the upgrade commands:

```
PATH=/usr/local/bin:/usr/bin:/bin:/opt/bin

pacman -Syu
pacman -Su
```

Close all MSYS windows and open a new one to install the toolchain:

```
PATH=/usr/local/bin:/usr/bin:/bin:/opt/bin

pacman -S mingw-w64-x86_64-gcc
pacman -S make
```

Now open a MINGW64 shell to build libusb and dfu-util:

```
PATH=/mingw64/bin:/usr/local/bin:/usr/bin:/bin

cd libusb-1.0.20
./configure --prefix=$PWD/../build
make
make install
cd ..

cd dfu-util-0.9
./configure USB_CFLAGS="-I$PWD/../build/include/libusb-1.0" \
            USB_LIBS="-L $PWD/../build/lib -lusb-1.0" --prefix=$PWD/../build
make
make install
cd ..
```

To link libusb statically into dfu-util.exe use instead of only "make":
`make LDFLAGS=-static`

The built executables (and DLL) will now be in the build/bin folder.
