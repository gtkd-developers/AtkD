# AtkD

D bindings for the ATK Accessibility Toolkit.

please view COPYING for AtkD's license.

## Building

For building you will need the Atk development files, and the [gir-to-d](https://github.com/gtkd-developers/gir-to-d) tool.

Both [dub](https://code.dlang.org/) and [Meson](https://mesonbuild.com) build files are available.

Compiling with meson:
```
$ meson builddir && cd builddir
$ ninja
```
