# THIS IS A DRAFT, work in progress

# Distributing plugins on Linux

## Standard path

Sytem wide installation:
- `/usr/lib/clap/<vendor>/plug.so`
- `/usr/share/<vendor>/plug/` for your skins, factory content, ...

User installation:
- `~/.clap/<vendor>/plug.so`
- `~/.local/share/<vendor>/`  for your skins, factory content, ...

Settings, activation, licenses:
- `~/.config/<vendor>/`

Caches:
- `~/.cache/<vendor>`

Indexes, like for searches presets
- `~/.local/var/<vendor>` ???

User presets
- `$XDG_DOCUMENTS/Audio Plugins/<vendor>/<plug>/presets`

User skins
- ???

User additionnal content, wavetable, samples, ...
- ???

Type of installation: system install, user install, prefix install?
Where to put the plugin shared library?
Where to put the images, skins, factory preset content?
Where to put activation/license files?
Where to put user's presets?
Where to put caches and temporary files?

## Runtime situation

Linux comes in various different distributions, with differing sets of installed packages.

The widest compatibility can usually be achieved by picking an old Debian or Ubuntu
stable release as build platform and statically linking against library dependencies.
Static linking increases binary size but ensures that all needed dependencies are
shipped along/inside the plugin.

A small set of libraries can create problems when statically linked and need
to be excluded so plugins either rely on it already being present on the host system
or make their dependencies optional (e.g. by using `dlopen(3)`).
The [AppImage](https://github.com/AppImage) project maintains a list of problematic libraries here:
https://github.com/AppImage/pkg2appimage/blob/master/excludelist

Building against an old stable distributions means that library and symbol dependencies
can likely be resolved on newer host systems. And by building insider a Docker environment,
reproducability of the build process is vastly improved (helps with CI debugging) and the
host platform can be freely chosen.

## Cleanup the plugin

How to strip and control exported symbols using a linker script.

## Docker setup

Maybe provide a starting point Dockerfile which can be used to build plugins that are ready to be deployed.
This docker could have an old glibc and the latest build tools.

## Getting static libs

Maybe explain how to do this using vcpkg.

## Distribution

Make a .tar.gz? Ship a .deb or .rpm? Have a `install.sh`?
I think the right way is to have a `.tar.gz` which can then be used for repackaging and performing custom installation.
How to publish on flathub.
