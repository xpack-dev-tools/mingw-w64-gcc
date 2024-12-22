---

title:  xPack MinGW-w64 GCC v11.3.0-1 released

summary: "Version **11.3.0-1** is the first release."

version: "11.3.0-1"
npm_subversion: 3
gcc_version: "11.3.0"
gcc_version_major: "11"
gcc_release_date: "Aug 19, 2022"
binutils_version: "2.38"
binutils_release_url: "https://lists.gnu.org/archive/html/info-gnu/2022-02/msg00009.html"
binutils_date: "Feb 9, 2022"
mingw_release: "9.0.0"

download_url: https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/releases/tag/v11.3.0-1/

date: 2022-09-25 21:31:38 +0300

redirect_to: https://xpack-dev-tools.github.io/mingw-w64-gcc-xpack/blog/2022/09/25/mingw-w64-gcc-v11-3-0-1-released/

comments: true

categories:
  - releases
  - mingw-w64-gcc

tags:
  - releases
  - gcc
  - mingw
  - mingw-w64

---

The [xPack MinGW-w64 GCC](https://xpack.github.io/dev-tools/mingw-w64-gcc/)
is a standalone cross-platform binary distribution of
[Mingw-w64](https://www.mingw-w64.org)
[GCC](https://gcc.gnu.org).

There are separate binaries for **Windows** (x64),
**macOS** (x64, arm64)
and **GNU/Linux** (x64, arm64 and arm).

{% include note.html content="The main targets for the GNU/Linux Arm
binaries are the **Raspberry Pi** class devices (armv7l and aarch64;
armv6 is not supported)." %}

## Download

The binary files are available from [GitHub Releases]({{ page.download_url }}).

## Prerequisites

- x64 GNU/Linux: any system with **GLIBC 2.27** or higher
  (like Ubuntu 18 or later, Debian 10 or later, RedHat 8 or later,
  Fedora 29 or later, etc)
- arm64/arm GNU/Linux: any system with **GLIBC 2.27** or higher
  (like Raspberry Pi OS, Ubuntu 18 or later, Debian 10 or later, RedHat 8 or later,
  Fedora 29 or later, etc)
- x64 Windows: Windows 7 with the Universal C Runtime
  ([UCRT](https://support.microsoft.com/en-us/topic/update-for-universal-c-runtime-in-windows-c0514201-7fe6-95a3-b0a5-287930f3560c)),
  Windows 8, Windows 10
- x64 macOS: 10.13 or later
- arm64 macOS: 11.6 or later

## Install

The full details of installing the **xPack MinGW-w64 GCC** on various platforms
are presented in the separate [Install]({{ site.baseurl }}/dev-tools/mingw-w64-gcc/install/) page.

### Easy install

The easiest way to install GCC is with
[`xpm`]({{ site.baseurl }}/xpm/)
by using the **binary xPack**, available as
[`@xpack-dev-tools/mingw-w64-gcc`](https://www.npmjs.com/package/@xpack-dev-tools/mingw-w64-gcc)
from the [`npmjs.com`](https://www.npmjs.com) registry.

With the `xpm` tool available, installing
the latest version of the package and adding it as
a dependency for a project is quite easy:

```sh
cd my-project
xpm init # Only at first use.

xpm install @xpack-dev-tools/mingw-w64-gcc@latest

ls -l xpacks/.bin
```

To install this specific version, use:

```sh
xpm install @xpack-dev-tools/mingw-w64-gcc@{{ page.version }}.{{ page.npm_subversion }}
```

It is also possible to install Meson Build globally, in the user home folder,
but this requires xPack aware tools to automatically identify them and
manage paths.

```sh
xpm install --global @xpack-dev-tools/mingw-w64-gcc@latest --verbose
```

### Uninstall

To remove the links from the current project:

```sh
cd my-project

xpm uninstall @xpack-dev-tools/mingw-w64-gcc
```

To completely remove the package from the central xPacks store:

```sh
xpm uninstall --global @xpack-dev-tools/mingw-w64-gcc
```

## Compliance

The xPack MinGW-w64 GCC generally follows the official
[GCC](https://gcc.gnu.org/releases.html) releases.

The current version is based on:

- GCC version [{{ page.gcc_version }}](https://gcc.gnu.org/gcc-{{ page.gcc_version_major }}/) from {{ page.gcc_release_date }};
- binutils version
[{{ page.binutils_version }}]({{ page.binutils_release_url }}) from {{ page.binutils_date }}
- MinGW-w64 version [{{ page.mingw_release }}](https://sourceforge.net/projects/mingw-w64/files/mingw-w64/mingw-w64-release/)

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
[README-MAINTAINER](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/blob/xpack/README-MAINTAINER.md) page.

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

```txt
cc2f9cc866fdb52667b6ef8fdf94c268483c19c3810e446ebde17b30d58cdf6e
xpack-mingw-w64-gcc-11.3.0-1-darwin-arm64.tar.gz

d2a0ea0079366330ed8202793a077d5e27aa58d6ebd985b4221f7027f5493ce5
xpack-mingw-w64-gcc-11.3.0-1-darwin-x64.tar.gz

666d49555bc66dbbcc359463fccf0a144bb505895726c5121b76693f5b124335
xpack-mingw-w64-gcc-11.3.0-1-linux-arm.tar.gz

532e9fc75808badd373c28981f1775c7ee32054251cb92c4f3291b9eecc1462a
xpack-mingw-w64-gcc-11.3.0-1-linux-arm64.tar.gz

133b37b848d1e00a51c4117126e9d56ed12ca1da97c00d075d0db9796bfe61d8
xpack-mingw-w64-gcc-11.3.0-1-linux-x64.tar.gz

2ff8e6d82a6de1a260403f6cc93bff9a5b99c036edbbc20839f913fc6c51a815
xpack-mingw-w64-gcc-11.3.0-1-win32-x64.zip

```

## Deprecation notices

### 32-bit support

Support for 32-bit x86 GNU/Linux and x86 Windows was
dropped in 2022. Support for 32-bit Arm GNU/Linux (armv7l) will be preserved
for a while, due to the large user base of 32-bit Raspberry Pi systems.

### GNU/Linux minimum requirements

Support for RedHat 7 was dropped in 2022 and the
minimum requirement was raised to GLIBC 2.27, available starting
with Ubuntu 18, Debian 10 and RedHat 8.

## Download analytics

- GitHub [xpack-dev-tools/mingw-w64-gcc-xpack](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/)
  - this release [![Github All Releases](https://img.shields.io/github/downloads/xpack-dev-tools/mingw-w64-gcc-xpack/v{{ page.version }}/total.svg)](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/releases/v{{ page.version }}/)
  - all xPack releases [![Github All Releases](https://img.shields.io/github/downloads/xpack-dev-tools/mingw-w64-gcc-xpack/total.svg)](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/releases/)
  - [individual file counters](https://somsubhra.github.io/github-release-stats/?username=xpack-dev-tools&repository=gcc-xpack) (grouped per release)
- npmjs.com [@xpack-dev-tools/mingw-w64-gcc](https://www.npmjs.com/package/@xpack-dev-tools/mingw-w64-gcc)
  - latest releases [![npm](https://img.shields.io/npm/dw/@xpack-dev-tools/mingw-w64-gcc.svg)](https://www.npmjs.com/package/@xpack-dev-tools/mingw-w64-gcc/)
  - all @xpack-dev-tools releases [![npm](https://img.shields.io/npm/dt/@xpack-dev-tools/mingw-w64-gcc.svg)](https://www.npmjs.com/package/@xpack-dev-tools/mingw-w64-gcc/)

Credit to [Shields IO](https://shields.io) for the badges and to
[Somsubhra/github-release-stats](https://github.com/Somsubhra/github-release-stats)
for the individual file counters.
