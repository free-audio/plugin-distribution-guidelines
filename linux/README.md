#### THIS IS A DRAFT, work in progress

### Distributing plugins on Linux

## Standard path

Type of installation: system install, user install, prefix install?
Where to put the plugin shared library?
Where to put the images, skins, factory preset content?
Where to put activation/license files?
Where to put user's presets?
Where to put caches and temporary files?

## Runtime situation

Explain the complexity about Linux deployment.
How to link against an old glibc.
What to link statically and what to link dynamically.

## Cleanup the plugin

How to strip and control exported symbols using a linker script.

## Docker setup

Maybe provide a starting point Dockerfile which can be used to build plugins that are ready to be deployed.

## Distribution

Make a .tar.gz? Ship a .deb or .rpm? Have a `install.sh`?
I think the right way is to have a `.tar.gz` which can then be used for repackaging and performing custom installation.
How to publish on flathub.
