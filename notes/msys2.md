# MSYS2

MSYS2 is software distribution and a building platform for Windows. It provides a Unix-like environment, a command-line interface and a software repository making it easier to install, use, build and port software on Windows. That means Bash, Autotools, Make, Git, GCC, GDB..., all easily installable through Pacman, a fully-featured package manager.

It is an independent rewrite of MSys, based on modern Cygwin (POSIX compatibility layer) and MinGW-w64 with the aim of better interoperability with native Windows software.

# Using Packages

The MSYS2 software distribution uses a port of pacman from Arch Linux to manage (install, remove and update) binary packages and also to build those packages in the first place.

Packages in MSYS2 work like packages in popular Linux distributions. A package is an archive containing a piece of software. This normally means executable files, runtime libraries, data, shared and static link libraries, header files, config files, and manual pages. Packages also contain metadata, such as the software's name, description of its purpose, version number, vendor, checksum, and a list of dependencies necessary for the software to run properly. Upon installation, the files contained are extracted into your MSYS2 installation directory and the metadata are stored in a local database.

There are 3 package repositories, **msys2**, **mingw32**, and **mingw64**. The packages in **msys2** are named just like on a Linux distribution, the packages in **mingw** are prefixed by either `mingw-w64-i686-` for 32-bit packages, or `mingw-w64-x86_64-` for 64-bit packages.

## Find a Package

```
pacman -Ss <name or part of the name of the package>
```

## Install a Package

```
pacman -S <name of the package>
```

## Update Packages

```
pacman -Syuu
```

## Uninstall a Package

```
pacman -R <name of the package>
```
