README:
-------

Build Status:
- [![Build Status](https://travis-ci.org/careychow/libIEC61850.png?branch=master)](https://travis-ci.org/careychow/libIEC61850)

This file is part of the documentation of libiec61850. More documentation can be found online at http://libiec61850.com or in the provided doxygen documentation.

Content:
- Overview
- Building and running the examples
- Installing the library and the API headers
- Building on Windows with GOOSE support
- Building with the cmake build script


Overview
---------

libiec61850 is an open-source (GPLv3) implementation of an IEC 61850 client and server library. It is implemented in C (according to the C99 standard) to provide maximum portability. It can be used to implement IEC 61850 compliant client and server applications on embedded systems and PCs running Linux and Windows. Included is a set of simple example applications that can be used as a starting point to implement own IEC 61850 compliant devices or to communicate with IEC 61850 devices.


Building and running the examples
----------------------------------------

In the project root directoy type

> make examples

If the build succeeds you can find a few binary files in the projects root directory. You can also find a binary version of the library ("libiec61850.a") in the "build" directory.

Run the sample applications in the example folders. E.g.:

> cd examples/server_example1
> sudo ./server_example1

on the Linux command line.

You can test the server examples by using a generic client or the provided client example applications.


Installing the library and the API headers
--------------------------------------------

The make and cmake build scripts provide an install target. This target copies the API header files and the static library to a single directory for the headers (INSTALL_PREFIX/include) and the static library (INSTALL_PREFIX/lib). With this feature it is more easy to integrate libiec61850 in an external application since you only have to add a simple include directory to the build tool of your choice.

This can be invoked with

make install

The default install directory for the make build script is ".install".

You can modify this by setting the INSTALL_PREFIX environment variable (e.g.):

make INSTALL_PREFIX=/usr/local install

For the cmake build script you have to provide the CMAKE_INSTALL_PREFIX variable


Building on windows with GOOSE support
---------------------------------------

To build the library and run libiec61850 applications with GOOSE support on Windows (7/8) the use of a third-party library (winpcap) is required. This is necessary because current versions of Windows have no working support for raw sockets. You can download winpcap here (http://www.winpcap.org).

1. Download and install winpcap. Make sure that the winpcap driver is loaded at boot time (you can choose this option at the last screen of the winpcap installer).
2. Reboot the system (you can do this also later, but you need to reboot or load the winpcap driver before running any llibiec61850 applications that use GOOSE).
3. Download the winpcap developers pack from here (http://www.winpcap.org/install/bin/WpdPack_4_1_2.zip)
4. Unpack the zip file. Copy the folders Lib and Include from the WpdPack directory in the third_party/winpcap directory of libiec61850

Building with the cmake build script
-------------------------------------

With the help of the cmake build script it is possible to create platform independet project descriptions and let cmake create specific project or build files for other tools like Make or Visual Studio.

If you have cmake installed fire up a command line (cmd.exe) and create a new subdirectory in the libiec61850-0.x folder. Change to this subdirectory. Then you can invoke cmake. As an command line argument you have to supply a "generator" that is used by cmake to create the project file for the actual build tool (in our case Visual Studio).

cmake -G "Visual Studio 11" ..

will instruct cmake to create a "solution" for Visual Studio 2012. To do the same thing for Visual Studio 2010 type

cmake -G "Visual Studio 10" ..

Note: The ".." at the end of the command line tells cmake where to find the main build script file (called CMakeLists.txt). This should point to the folder libiec61850-0.x which is in our case the parent directory (..).

To select some configuration options you can use ccmake or cmake-gui.





