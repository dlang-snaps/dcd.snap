dcd.snap
========

This project defines a snap package for DCD, an auto-complete program
for the D programming language.  It is an 'external' snap, meaning that
it downloads and builds the source from the official DCD git repo.  For
more information on DCD, see: https://github.com/dlang-community/DCD

The D programming language is a systems programming language with C-like
syntax and static typing.  It combines efficiency, control and modelling
power with safety and programmer productivity.  For more information on
the D language, see: https://dlang.org/

Snap packages are designed to provide secure, containerized applications
that are appropriately sandboxed away from the rest of the system they
are running on.  For more information on snap packages, see:
http://snapcraft.io/


Building
--------

On Ubuntu 16.04 or higher with snapcraft installed
(`sudo apt install snapcraft`):

    git clone https://github.com/dlang-snaps/dcd.snap.git
    cd dcd.snap
    snapcraft

To ensure a clean build, install lxd (`sudo apt install lxd`), configure
its network settings, and then:

    snapcraft cleanbuild


Installing
----------

DCD has been packaged as a `classic` snap, so installing it requires the
`--classic` flag to be used in order to grant the necessary confinement
permissions.  Self-built snaps are unsigned and therefore also require
the `--dangerous` flag in order to install them:

    sudo snap install --classic --dangerous dcd_VERSION_amd64.snap

replacing `VERSION` as appropriate.

For more information on `classic` confinement, see:
https://insights.ubuntu.com/2017/01/09/how-to-snap-introducing-classic-confinement/


Configuration
----------

To make the DCD server work properly, you must manually specify the 
import directories paths for D module imports, this snap does not do 
this automatically to allow the user to use dmd with any druntime + phobos configuration.

If you simply want to configure DCD to work with our DMD package (snapcraft.io/dmd) 
you just need to run this command which will enable the import paths of the 
DMD snap package in the current user:

    echo -e "/snap/dmd/current/import/druntime\n/snap/dmd/current/import/phobos" > ~/.config/dcd/dcd.conf
    
For other dmd, druntime and phobos providers, consult their documentation 
to find out their import path.

More information is available on the official DCD documentation: https://github.com/dlang-community/DCD#configuration-files
