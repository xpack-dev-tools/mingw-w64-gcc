---
title:  xPack MinGW-w64 GCC v{{ XBB_RELEASE_VERSION }} released

TODO: select one summary

summary: "Version **{{ XBB_RELEASE_VERSION }}** is a maintenance release; it updates to
the latest upstream master."

summary: "Version **{{ XBB_RELEASE_VERSION }}** is a new release; it follows the official GNU GCC release."

gcc_version: "12.2.0"
gcc_version_major: "12"
gcc_release_date: "August 19, 2022"
binutils_version: "2.39"
binutils_release_url: "https://lists.gnu.org/archive/html/info-gnu/2022-08/msg00002.html"
binutils_date: "Aug 5, 2022"
mingw_release: "10.0.0"

version: "{{ XBB_RELEASE_VERSION }}"
npm_subversion: "1"

download_url: https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/releases/tag/v{{ XBB_RELEASE_VERSION }}/

comments: true

date:   {{ RELEASE_DATE }}

categories:
  - releases
  - mingw-w64-gcc

tags:
  - releases
  - gcc
  - mingw
  - mingw-w64

---

[The xPack MinGW-w64 GCC](https://xpack.github.io/mingw-w64-gcc/)
is a standalone cross-platform binary distribution of
[Mingw-w64](https://www.mingw-w64.org)
[GCC](https://gcc.gnu.org).

There are separate binaries for **Windows** (Intel 64-bit),
**macOS** (Intel 64-bit, Apple Silicon 64-bit)
and **GNU/Linux** (Intel 64-bit, Arm 32/64-bit).

{% raw %}{% include note.html content="The main targets for the Arm binaries
are the **Raspberry Pi** class devices (armv7l and aarch64;
armv6 is not supported)." %}{% endraw %}

## Download

The binary files are available from GitHub [Releases]({% raw %}{{ page.download_url }}{% endraw %}).

## Prerequisites

- GNU/Linux Intel 64-bit: any system with **GLIBC 2.27** or higher
  (like Ubuntu 18 or later, Debian 10 or later, RedHat 8 later,
  Fedora 29 or later, etc)
- GNU/Linux Arm 32/64-bit: any system with **GLIBC 2.27** or higher
  (like Raspberry Pi OS, Ubuntu 18 or later, Debian 10 or later, RedHat 8 later,
  Fedora 29 or later, etc)
- Intel Windows 64-bit: Windows 7 with the Universal C Runtime
  ([UCRT](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c)),
  Windows 8, Windows 10
- Intel macOS 64-bit: 10.13 or later
- Apple Silicon macOS 64-bit: 11.6 or later

## Install

The full details of installing the **xPack MinGW-w64 GCC** on various platforms
are presented in the separate
[Install]({% raw %}{{ site.baseurl }}{% endraw %}/dev-tools/gcc/install/) page.

### Easy install

The easiest way to install GCC is with
[`xpm`]({% raw %}{{ site.baseurl }}{% endraw %}/xpm/)
by using the **binary xPack**, available as
[`@xpack-dev-tools/mingw-w64-gcc`](https://www.npmjs.com/package/@xpack-dev-tools/mingw-w64-gcc)
from the [`npmjs.com`](https://www.npmjs.com) registry.

With the `xpm` tool available, installing
the latest version of the package and adding it as
a dependency for a project is quite easy:

```sh
cd my-project
xpm init # Only at first use.

xpm install @xpack-dev-tools/mingw-w64-gcc@latest --verbose

ls -l xpacks/.bin
```

To install this specific version, use:

```sh
xpm install @xpack-dev-tools/mingw-w64-gcc@{% raw %}{{ page.version }}.{{ page.npm_subversion }}{% endraw %} --verbose
```

It is also possible to install Meson Build globally, in the user home folder,
but this requires xPack aware tools to automatically identify them and
manage paths.

```sh
xpm install --global @xpack-dev-tools/mingw-w64-gcc@latest --verbose
```

### Uninstall

To remove the links created by xpm in the current project:

```sh
cd my-project

xpm uninstall @xpack-dev-tools/mingw-w64-gcc
```

To completely remove the package from the global store:

```sh
xpm uninstall --global @xpack-dev-tools/mingw-w64-gcc
```

## Compliance

The xPack MinGW-w64 GCC generally follows the official
[GCC](https://gcc.gnu.org/releases.html) releases.

The current version is based on:

- GCC version [{% raw %}{{ page.gcc_version }}{% endraw %}](https://gcc.gnu.org/gcc-{% raw %}{{ page.gcc_version_major }}{% endraw %}/) from {% raw %}{{ page.gcc_release_date }}{% endraw %};
- binutils version
[{% raw %}{{ page.binutils_version }}{% endraw %}]({% raw %}{{ page.binutils_release_url }}{% endraw %})
from {% raw %}{{ page.binutils_date }}{% endraw %}
- MinGW-w64 version [{% raw %}{{ page.mingw_release }}{% endraw %}](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/)

## Supported languages

The supported languages are:

- C
- C++
- Fortran
- Obj-C
- Obj-C++

Note: Obj-C/C++ support is minimalistic.

## Changes

Compared to the upstream, there are no functional changes.

## Bug fixes

- none

## Enhancements

- none

## Known problems

- none

## Shared libraries

On all platforms the packages are standalone, and expect only the standard
runtime to be present on the host.

All dependencies that are build as shared libraries are copied locally
in the `libexec` folder (or in the same folder as the executable for Windows).

### `-static-libgcc -static-libstdc++`

To avoid issues with DLLs, specific when using toolchains installed
in custom locations, it is highly recommended to use only the
static versions of the GCC libraries.

For C programs, append `-static-libgcc` to the linker line.

For C++ programs, since the toolchain is configured to use POSIX threads,
instead of `-static-libstdc++`, use the more explicit variant
`-Wl,-Bstatic,-lstdc++,-lpthread,-Bdynamic` when invoking the linker.

### `DT_RPATH` and `LD_LIBRARY_PATH`

On GNU/Linux the binaries are adjusted to use a relative path:

```console
$ readelf -d library.so | grep runpath
 0x000000000000001d (RPATH)            Library rpath: [$ORIGIN]
```

In the GNU ld.so search strategy, the `DT_RPATH` has
the highest priority, higher than `LD_LIBRARY_PATH`, so if this later one
is set in the environment, it should not interfere with the xPack binaries.

Please note that previous versions, up to mid-2020, used `DT_RUNPATH`, which
has a priority lower than `LD_LIBRARY_PATH`, and does not tolerate setting
it in the environment.

### `@rpath` and `@loader_path`

Similarly, on macOS, the binaries are adjusted with `install_name_tool` to use a
relative path.

## Documentation

To save space and bandwidth, the original GNU GCC documentation is available
[online](https://gcc.gnu.org/onlinedocs/).

## Build

The binaries for all supported platforms
(Windows, macOS and GNU/Linux) were built using the
[xPack Build Box (XBB)](https://xpack.github.io/xbb/), a set
of build environments based on slightly older distributions, that should be
compatible with most recent systems.

The scripts used to build this distribution are in:

- `distro-info/scripts`

For the prerequisites and more details on the build procedure, please see the
[How to build](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/blob/xpack/README-BUILD.md) page.

## CI tests

Before publishing, a set of simple tests were performed on an exhaustive
set of platforms. The results are available from:

- [GitHub Actions](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/actions/)
- [Travis CI](https://app.travis-ci.com/github/xpack-dev-tools/mingw-w64-gcc-xpack/builds/)

## Tests

The binaries were tested on a variety of platforms,
but mainly to check the integrity of the
build, not the compiler functionality.

## Checksums

The SHA-256 hashes for the files are:
