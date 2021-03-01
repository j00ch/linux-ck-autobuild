# linux-ck-autobuild

## About 
> Linux-ck is a package that allows users to run a kernel and headers setup patched with Con Kolivas' ck patchset, including a CPU scheduler named MuQSS (Multiple Queue Skiplist Scheduler, pronounced mux) which replaces Brain Fuck Scheduler (BFS), his previous work. Many Arch Linux users choose this kernel for its excellent desktop interactivity and responsiveness under any load situation.

https://wiki.archlinux.org/index.php/linux-ck

Being a longtime user and advocate of linux-ck myself, i felt a bit handicapped when a few older architectures were dropped from Graysky's unofficial repository:

https://bbs.archlinux.org/viewtopic.php?pid=1934484#p1934484

This means that users now have to build the kernels themselves for each of the dropped architectures. Now i have to say that the linux-ck package from the AUR (Arch User Repository) works very well and is easy to configure, however it takes at least an hour to build one architecture and cannot be automated.
This means you'll have to check for updates, check the build and then build another. All in all that would just be a very painful experience, so i decided to make a fully automated version of linux-ck.

## Features

* Automatically builds desired architectures
* Daemon which monitors for new releases and automatically starts the build script
* Option to limit system resources
* Compatible with modprobe-db
* Custom commands that can be run after the build script
* Automatically checks the ck repo for pre-built kernels
* Option to add build kernels to your local repo

## Installing

This package can be installed from the AUR:
https://aur.archlinux.org/packages/linux-ck-autobuild

from a command line simply run:

``git clone https://aur.archlinux.org/linux-ck-autobuild.git``

``makepkg -si``

## Usage
First you'll need to setup the configuration file, simply by running ``linux-ck-autobuild`` from a command line. The script will notify you about configuration missing and will copy the default config to your home folder. The script will then open the new config where you can manually edit it to your preferences. Directions are given in the configuration file.

The minimum options you'll have to modify will be the SUBARCH (the micro architectures you want to build) and probably the BUILDDIR, which sets the location where the builds take place (don't worry, you don't have to download anything yourself).

If you want to fully automate the build script you can enable the daemon by running:

``linux-ck-autobuild --enable-autostart``

or

``sudo systemd enable linux-ck-autobuild@$USER.service``

The first option is recommended if you run a graphical user environment, which notifies the user in case of an update and the option to postpone the build.

The second option is handy for servers that don't have a console, it is advisable to look at the ``makeflags`` and ``maxload`` option in the config. The configuration can be accessed at any time by running ``linux-ck-autobuild -c`` from a command line.
