# Arch Linux Package Build for libavg

This is a git based PKGBUILD for [libavg](https://www.libavg.de/site/).

This version works for the new cmake build system and will generate the colorplugin library, as well as deploy global configuration files.

I´d like to credit [the old original packagebuild](https://github.com/libavg/libavg_PKGBUILD/blob/master/PKGBUILD), which does not work anymore and seems to be orphaned.


Usage:
```shell
makepkg -c
sudo pacman -U libvg-git-date-ver-arch.pkg.tar.xz
```
