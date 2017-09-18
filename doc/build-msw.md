# BlakeStar build instructions for MS Windows

Copyright (c) 2009-2012 Bitcoin Developers
Distributed under the MIT/X11 software license, see the accompanying
file license.txt or http://www.opensource.org/licenses/mit-license.php.
This product includes software developed by the OpenSSL Project for use in
the OpenSSL Toolkit (http://www.openssl.org/).  This product includes
cryptographic software written by Eric Young (eay@cryptsoft.com) and UPnP
software written by Thomas Bernard.


See readme-qt.rst for instructions on building BlakeStar QT, the
graphical user interface.

## WINDOWS BUILD NOTES


### Compilers Supported

TODO: What works?
Note: releases are cross-compiled using mingw running on Linux.


### Dependencies

Libraries you need to download separately and build:

Dependency|Default path|Download
----------|------------|--------
OpenSSL | \openssl-1.0.1c-mgw | http://www.openssl.org/source/ Alternative: https://www.openssl.org/source/old/1.0.1/
Berkeley DB | \db-4.8.30.NC-mgw | http://www.oracle.com/technology/software/products/berkeley-db/index.html Alternative: http://www.oracle.com/technetwork/database/berkeleydb/downloads/index-082944.html
Boost | \boost-1.50.0-mgw | http://www.boost.org/users/download/
miniupnpc | \miniupnpc-1.6-mgw | http://miniupnp.tuxfamily.org/files/

Dependency|License|Version used
----------|-------|------------
OpenSSL | Old BSD license with the problematic advertising requirement | 1.0.1c
Berkeley DB | New BSD license with additional requirement that linked software must be free open source | 4.8.30.NC
Boost | MIT-like license | 1.50.0
miniupnpc | New (3-clause) BSD license | 1.6

### Useful libraries

Name | Instructions | Download
-----|--------------|---------
ActivePerl | Typical installation | https://www.activestate.com/activeperl/downloads
Python | Typical installation + add to PATH | http://www.python.org/ftp/python/3.3.3/python-3.3.3.amd64.msi
MinGW | Install MSYS shell | https://sourceforge.net/projects/mingw/files/Installer/mingw-get-setup.exe/download

### OpenSSL

MSYS shell:
un-tar sources with MSYS 'tar xfz' to avoid issue with symlinks (OpenSSL ticket 2377)
change 'MAKE' env. variable from 'C:\MinGW32\bin\mingw32-make.exe' to '/c/MinGW32/bin/mingw32-make.exe'

```
cd /c/openssl-1.0.1c-mgw
./config
make
```

### Berkeley DB

MSYS shell:
```
cd /c/db-4.8.30.NC-mgw/build_unix
sh ../dist/configure --enable-mingw --enable-cxx
```
make

### Boost

DOS prompt:
```
downloaded boost jam 3.1.18
cd \boost-1.50.0-mgw
bjam toolset=gcc --build-type=complete stage
```

### MiniUPnPc

UPnP support is optional, make with USE_UPNP= to disable it.

MSYS shell:

```
cd /c/miniupnpc-1.6-mgw
make -f Makefile.mingw
mkdir miniupnpc
cp *.h miniupnpc/
```

### BlakeStar

DOS prompt:

```
cd \BlakeStar\src
mingw32-make -f makefile.mingw
strip BlakeStard.exe
```