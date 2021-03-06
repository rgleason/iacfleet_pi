IAC Fleetcode plugin Plugin for OpenCPN
=======================================

[![Build Status](https://travis-ci.org/nohal/iacfleet_pi.svg?branch=master)](https://travis-ci.org/nohal/iacfleet_pi)
[![Build status](https://ci.appveyor.com/api/projects/status/405d7cygmln0urfj?svg=true)](https://ci.appveyor.com/project/nohal/iacfleet-pi)
[![Coverity scan](https://scan.coverity.com/projects/4964/badge.svg)](https://scan.coverity.com/projects/nohal-iacfleet_pi)

Compiling
=========
You have to be able to compile OpenCPN itself - Get the info at http://opencpn.org/ocpn/developers_manual

* This plugin now builds out of the OpenCPN source tree
```
git clone git://github.com/nohal/iacfleet_pi.git
```

### Build:
```
mkdir iacfleet_pi/build
cd iacfleet_pi/build
cmake .. # To produce a binary compatible with Windows XP, you must set the respective toolset - use 'cmake -T v120_xp ..'
cmake --build .
```
Windows note: You must place opencpn.lib into your build directory to be able to link the plugin DLL. You can get this file from your local OpenCPN build, or

Debugging:
If you check out the plugin source into the plugins subdirectory of your OpenCPN source tree, you can build it as part of it.

Windows Specific Libraries
--------------------------

Under windows, you must find the file "opencpn.lib" (Visual Studio) or "libopencpn.dll.a" (mingw) which is built in the build directory after compiling opencpn

### Build on Mac OS X:
Tools: Can be installed either manually or from Homebrew (http://brew.sh)
```
#brew install git #If I remember well, it is already available on the system
brew install cmake
brew install gettext
ln -s /usr/local/Cellar/gettext/0.19.2/bin/msgmerge /usr/local/bin/msgmerge
ln -s /usr/local/Cellar/gettext/0.19.2/bin/msgfmt /usr/local/bin/msgfmt
```

To target older OS X versions than the one you are running, you need the respective SDKs installed. The easiest way to achieve that is using https://github.com/devernay/xcodelegacy

#### Building wxWidgets
(do not use wxmac from Homebrew, it is not compatible with OpenCPN)
Get wxWidgets 3.0.x source from http://wxwidgets.org
Configure, build and install
```
cd wxWidgets-3.0.2
./configure --enable-unicode --with-osx-cocoa --with-macosx-sdk=/Applications/Xcode.app/Contents/Developer/Platforms/MacOSX.platform/Developer/SDKs/MacOSX10.7.sdk/ --with-macosx-version-min=10.7 --enable-aui --disable-debug --enable-opengl
make
sudo make install
```

#### Building the plugin
Before running cmake, you must set the deployment target to OS X 10.7 to be compatible with the libraries used by core OpenCPN
```
export MACOSX_DEPLOYMENT_TARGET=10.7
```

#### Packaging on OS X
Get and install the Packages application from http://s.sudre.free.fr/Software/Packages/about.html
```
make create-pkg
```

License
=======
The plugin code is licensed under the terms of the GPL v2 or, at your will, later.

## TODO
* ~~Finish the OpenGL rendering implementation~~
* Support all the available datasources:
  * ~~fleet.nadi to query@saildocs.com~~
  * ~~http://www.mar.mil.br/dhn/chm/meteo/prev/iac/iac.htm~~
  * ~~http://weather.noaa.gov/pub/data/raw/as/asxx21.egrr..txt~~
* ~~Automatic download from NOAA and BR~~
* ~~Refine the GUI to save space~~
* Extend beyond IACFleet - at least to data from http://weather.gmdss.org/index.html
