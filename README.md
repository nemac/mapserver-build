mapserver-build
===============

This project contains the materials needed to build a MapServer binary suitable
for use on NEMAC servers.  It includes a copy of the MapServer source code, and
a script with the relevant build configuration settings.

Prerequisites
=============

This build process depends on several tools, libraries, and packages already
being installed on the system.  NEMAC's *rpmbuild* puppet manifest includes
all the prerequisites, so you should be able to run the build process on a server
on which that manifest has been applied.

Build Process
=============

These instructions are written assuming that you're compiling
mapserver version 6.4.1; if you are working with a different version,
adjust the version numbers accordingly.

First, if necessary, clean up the results of a previous build by doing

    rm -rf build
    rm -rf src/mapserver-*
    
Then create an empty `build` directory

    mkdir build
    
From inside the `src` directory, unpack the source tar file:

    cd src
    tar xvfz ../mapserver-6.4.1.tar.tgz
    
Then, from inside the `build` directory, run the `do_cmake` script

    cd ../build
    sh ../do_cmake
    
The `do_cmake` script contains various compilation settings;
if you want to change the settings, edit that script before running it.

Finally, still inside the `build` directory, run `make`.  You can speed
up the compilation process substantially by using the `-j` flag to enable
parallel compilation.

    make -j 8

Once compilation is done, the final MapServer executable will be
in the file `build/mapserv`.
