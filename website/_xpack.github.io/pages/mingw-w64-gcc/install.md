---

title: How to install the xPack MinGW-w64 GCC binaries
permalink: /dev-tools/mingw-w64-gcc/install/

summary: "The recommended method is via xpm."

version: "11.3.0"
xpack-subversion: "1.3"

comments: true
toc: false

date: 2022-10-04 11:43:00 +0300

redirect_to: https://xpack-dev-tools.github.io/mingw-w64-gcc-xpack/docs/install/

---

## Overview

The **xPack MinGW-w64 GCC** can be installed automatically,
via `xpm` (the
recommended method), or manually, by downloading and unpacking one of the
portable archives.

{% capture easy_install %}

## Easy install

The easiest way to install MinGW-w64 GCC is by using the
**binary xPack**, available as
[`@xpack-dev-tools/mingw-w64-gcc`](https://www.npmjs.com/package/@xpack-dev-tools/mingw-w64-gcc)
from the [`npmjs.com`](https://www.npmjs.com) registry.

### Prerequisites

The only requirement is a recent
`xpm`, which is a portable
[Node.js](https://nodejs.org) command line application. To install it,
follow the instructions from the
[xpm install]({{ site.baseurl }}/xpm/install/) page.

### Install

With xpm available, installing
the latest version of the package is quite easy:

```sh
cd my-project
xpm init # Only at first use.

xpm install @xpack-dev-tools/mingw-w64-gcc@latest --verbose
```

This command will always install the latest available version,
in the global xPacks store, which is a platform dependent folder
(check the output of the `xpm` command for the actual folder used on
your platform).

{% capture include_1 %}
The install location can be configured using the
`XPACKS_STORE_FOLDER` environment variable; for more details please check the
[xpm folders]({{ site.baseurl }}/xpm/folders/) page.
{% endcapture %}

{% include tip.html content=include_1 %}

{% include tip.html content="The archive content is unpacked into a folder
named `.content`. On some platforms
this might be hidden for normal browsing, and require
separate options (like `ls -A`) or, in file browsers, to enable
settings like **Show Hidden Files**." %}

### Update

For the moment, to update the package, try to install the latest release again,
as shown before. If there is a new release, it will be installed,
otherwise a message will warn that the package is already installed.

Future versions of xpm will implement the `outdated` and `update` commands,
as npm does.

### Uninstall

To remove the links from the current project:

```sh
cd my-project

xpm uninstall @xpack-dev-tools/mingw-w64-gcc
```

To completely remove the package from the central xPacks store:

```sh
xpm uninstall --global @xpack-dev-tools/mingw-w64-gcc --verbose
```

{% endcapture %}

{% capture manual_install %}

## Manual install

For all platforms, the **xPack MinGW-w64 GCC** binaries are
released as portable
archives that can be installed in any location.

The archives can be downloaded from the
GitHub [releases](https://github.com/xpack-dev-tools/mingw-w64-gcc-xpack/releases/)
pages.
{% endcapture %}

{% capture windows %}

{{ easy_install }}

### Test

To check if the xpm installed GCC starts, use something like:

```doscon
C:\>%USERPROFILE%\AppData\Roaming\xPacks\@xpack-dev-tools\mingw-w64-gcc\{{ page.version }}-{{ page.xpack-subversion }}.1\.content\bin\x86_64-w64-mingw32-gcc.exe" --version
x86_64-w64-mingw32-gcc.exe (xPack MinGW-w64 GCC x86_64) {{ page.version }}
```

{{ manual_install }}

### Download

The Windows versions of **xPack MinGW-w64 GCC**
are packed as ZIP files.
Download the latest version named like:

- `xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-win32-x64.zip`

{% include note.html content="In case you wonder where the suffix comes
from, it is exactly the Node.js `process.platform` and `process.arch`.
The `win32` part is confusing, but we have to live with it." %}

### Unpack

To manually install the xPack MinGW-w64 GCC,
unpack the archive and copy the versioned folder into the
`%USERPROFILE%\AppData\Roaming\xPacks\mingw-w64-gcc`
(for example `C:\Users\ilg\AppData\Roaming\xPacks\mingw-w64-gcc`) folder;
according to Microsoft, `AppData\Roaming` is the recommended location for
installing user specific packages.

You may shorten the last folder name and keep only the version.

{% include note.html content="For manual installs, the recommended
install location is slightly different from the xpm install folders,
which use the scope (like `@xpack-dev-tools`) to group different tools,
and `.content` to store the unpacked archive." %}

### Test

To check if the manually installed GCC starts, use something like:

```doscon
C:\>%USERPROFILE%\AppData\Roaming\xPacks\mingw-w64-gcc\xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}\bin\mingw-w64-gcc.exe" --version
x86_64-w64-mingw32-gcc (xPack MinGW-w64 GCC x86_64) {{ page.version }}
```

{% endcapture %}

{% capture macos %}

{{ easy_install }}

### Test

To check if the xpm installed GCC starts, use something like:

```console
$ ~/.local/xPacks/@xpack-dev-tools/mingw-w64-gcc/{{ page.version }}-{{ page.xpack-subversion }}.1/.content/bin/x86_64-w64-mingw32-gcc --version
x86_64-w64-mingw32-gcc (xPack MinGW-w64 GCC x86_64) {{ page.version }}
```

{{ manual_install }}

### Download

The macOS versions of **xPack MinGW-w64 GCC**
are packed as `.tar.gz` archives.
Download the latest version named like:

- `xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-darwin-x64.tar.gz`
- `xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-darwin-arm64.tar.gz`

### Unpack

To manually install the xPack MinGW-w64 GCC,
unpack the archive and copy it to
`~/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-<version>`:

```sh
mkdir -p ~/.local/xPacks/mingw-w64-gcc
cd ~/.local/xPacks/mingw-w64-gcc

tar xvf ~/Downloads/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-darwin-x64.tar.gz
chmod -R -w xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}
```

You may shorten the last folder name and keep only the version.

{% include note.html content="For manual installs, the recommended
install location is different from the xpm install folders." %}

The result is a structure like:

```console
$ tree -L 2 /Users/ilg/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}
/Users/ilg/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}
├── README.md
├── bin
│   ├── i686-w64-mingw32-addr2line
│   ├── i686-w64-mingw32-ar
│   ├── i686-w64-mingw32-as
│   ├── i686-w64-mingw32-c++
│   ├── i686-w64-mingw32-c++filt
│   ├── i686-w64-mingw32-cpp
│   ├── i686-w64-mingw32-dlltool
│   ├── i686-w64-mingw32-dllwrap
│   ├── i686-w64-mingw32-elfedit
│   ├── i686-w64-mingw32-g++
│   ├── i686-w64-mingw32-gcc
│   ├── i686-w64-mingw32-gcc-11.3.0
│   ├── i686-w64-mingw32-gcc-ar
│   ├── i686-w64-mingw32-gcc-nm
│   ├── i686-w64-mingw32-gcc-ranlib
│   ├── i686-w64-mingw32-gcov
│   ├── i686-w64-mingw32-gcov-dump
│   ├── i686-w64-mingw32-gcov-tool
│   ├── i686-w64-mingw32-gendef
│   ├── i686-w64-mingw32-gfortran
│   ├── i686-w64-mingw32-gprof
│   ├── i686-w64-mingw32-ld
│   ├── i686-w64-mingw32-ld.bfd
│   ├── i686-w64-mingw32-lto-dump
│   ├── i686-w64-mingw32-nm
│   ├── i686-w64-mingw32-objcopy
│   ├── i686-w64-mingw32-objdump
│   ├── i686-w64-mingw32-ranlib
│   ├── i686-w64-mingw32-readelf
│   ├── i686-w64-mingw32-size
│   ├── i686-w64-mingw32-strings
│   ├── i686-w64-mingw32-strip
│   ├── i686-w64-mingw32-widl
│   ├── i686-w64-mingw32-windmc
│   ├── i686-w64-mingw32-windres
│   ├── x86_64-w64-mingw32-addr2line
│   ├── x86_64-w64-mingw32-ar
│   ├── x86_64-w64-mingw32-as
│   ├── x86_64-w64-mingw32-c++
│   ├── x86_64-w64-mingw32-c++filt
│   ├── x86_64-w64-mingw32-cpp
│   ├── x86_64-w64-mingw32-dlltool
│   ├── x86_64-w64-mingw32-dllwrap
│   ├── x86_64-w64-mingw32-elfedit
│   ├── x86_64-w64-mingw32-g++
│   ├── x86_64-w64-mingw32-gcc
│   ├── x86_64-w64-mingw32-gcc-11.3.0
│   ├── x86_64-w64-mingw32-gcc-ar
│   ├── x86_64-w64-mingw32-gcc-nm
│   ├── x86_64-w64-mingw32-gcc-ranlib
│   ├── x86_64-w64-mingw32-gcov
│   ├── x86_64-w64-mingw32-gcov-dump
│   ├── x86_64-w64-mingw32-gcov-tool
│   ├── x86_64-w64-mingw32-gendef
│   ├── x86_64-w64-mingw32-gfortran
│   ├── x86_64-w64-mingw32-gprof
│   ├── x86_64-w64-mingw32-ld
│   ├── x86_64-w64-mingw32-ld.bfd
│   ├── x86_64-w64-mingw32-lto-dump
│   ├── x86_64-w64-mingw32-nm
│   ├── x86_64-w64-mingw32-objcopy
│   ├── x86_64-w64-mingw32-objdump
│   ├── x86_64-w64-mingw32-ranlib
│   ├── x86_64-w64-mingw32-readelf
│   ├── x86_64-w64-mingw32-size
│   ├── x86_64-w64-mingw32-strings
│   ├── x86_64-w64-mingw32-strip
│   ├── x86_64-w64-mingw32-widl
│   ├── x86_64-w64-mingw32-windmc
│   └── x86_64-w64-mingw32-windres
├── distro-info
│   ├── CHANGELOG.md
│   ├── licenses
│   ├── patches
│   └── scripts
├── i686-w64-mingw32
│   ├── bin
│   ├── include
│   └── lib
├── include
├── lib
│   ├── bfd-plugins
│   ├── gcc
│   ├── libcc1.0.so
│   ├── libcc1.a
│   ├── libcc1.la
│   └── libcc1.so -> libcc1.0.so
├── libexec
│   ├── libgcc_s.1.dylib
│   ├── libgmp.10.dylib
│   ├── libiconv.2.dylib
│   ├── libisl.23.dylib
│   ├── libmpc.3.dylib
│   ├── libmpfr.6.dylib
│   ├── libstdc++.6.dylib
│   ├── libz.1.2.11.dylib
│   └── libz.1.dylib -> libz.1.2.11.dylib
├── share
│   ├── gcc-11.3.0
│   └── locale
└── x86_64-w64-mingw32
    ├── bin
    ├── include
    └── lib

21 directories, 85 files
```

### Test

To check if the manually installed GCC starts, use something like:

```console
$ ~/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}/bin/x86_64-w64-mingw32-gcc --version
x86_64-w64-mingw32-gcc (xPack MinGW-w64 GCC, 64-bit) {{ page.version }}
```

{% endcapture %}

{% capture linux %}

{{ easy_install }}

### Test

To check if the xpm installed GCC starts, use something like:

```console
$ ~/.local/xPacks/@xpack-dev-tools/mingw-w64-gcc/{{ page.version }}-{{ page.xpack-subversion }}.1/.content/bin/x86_64-w64-mingw32-gcc --version
x86_64-w64-mingw32-gcc (xPack MinGW-w64 GCC, 64-bit) {{ page.version }}
```

{{ manual_install }}

### Download

The GNU/Linux versions of **xPack MinGW-w64 GCC**
are packed as `.tar.gz` archives.
Download the latest version named like:

- `xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-x64.tar.gz`
- `xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-arm.tar.gz`
- `xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-arm64.tar.gz`

As the name implies, these are GNU/Linux `tar.gz` archives; they were build on
Ubuntu, but can be executed on most recent GNU/Linux distributions.

### Unpack

To manually install the xPack MinGW-w64 GCC,
unpack the archive and copy it to
`~/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-<version>`:

```sh
mkdir -p ~/.local/xPacks/mingw-w64-gcc
cd ~/.local/xPacks/mingw-w64-gcc

tar xvf ~/Downloads/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}-linux-x64.tar.gz
chmod -R -w xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}
```

You may shorten the last folder name and keep only the version.

{% include note.html content="For manual installs, the recommended
install location is slightly different from the xpm install folders,
which use the scope (like `@xpack-dev-tools`) to group different tools,
and `.content` to store the unpacked archive." %}

The result is a structure like:

```console
$ tree -L 2 /home/ilg/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}
/home/ilg/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}
├── bin
│   ├── i686-w64-mingw32-addr2line
│   ├── i686-w64-mingw32-ar
│   ├── i686-w64-mingw32-as
│   ├── i686-w64-mingw32-c++
│   ├── i686-w64-mingw32-c++filt
│   ├── i686-w64-mingw32-cpp
│   ├── i686-w64-mingw32-dlltool
│   ├── i686-w64-mingw32-dllwrap
│   ├── i686-w64-mingw32-elfedit
│   ├── i686-w64-mingw32-g++
│   ├── i686-w64-mingw32-gcc
│   ├── i686-w64-mingw32-gcc-11.3.0
│   ├── i686-w64-mingw32-gcc-ar
│   ├── i686-w64-mingw32-gcc-nm
│   ├── i686-w64-mingw32-gcc-ranlib
│   ├── i686-w64-mingw32-gcov
│   ├── i686-w64-mingw32-gcov-dump
│   ├── i686-w64-mingw32-gcov-tool
│   ├── i686-w64-mingw32-gendef
│   ├── i686-w64-mingw32-gfortran
│   ├── i686-w64-mingw32-gprof
│   ├── i686-w64-mingw32-ld
│   ├── i686-w64-mingw32-ld.bfd
│   ├── i686-w64-mingw32-lto-dump
│   ├── i686-w64-mingw32-nm
│   ├── i686-w64-mingw32-objcopy
│   ├── i686-w64-mingw32-objdump
│   ├── i686-w64-mingw32-ranlib
│   ├── i686-w64-mingw32-readelf
│   ├── i686-w64-mingw32-size
│   ├── i686-w64-mingw32-strings
│   ├── i686-w64-mingw32-strip
│   ├── i686-w64-mingw32-widl
│   ├── i686-w64-mingw32-windmc
│   ├── i686-w64-mingw32-windres
│   ├── x86_64-w64-mingw32-addr2line
│   ├── x86_64-w64-mingw32-ar
│   ├── x86_64-w64-mingw32-as
│   ├── x86_64-w64-mingw32-c++
│   ├── x86_64-w64-mingw32-c++filt
│   ├── x86_64-w64-mingw32-cpp
│   ├── x86_64-w64-mingw32-dlltool
│   ├── x86_64-w64-mingw32-dllwrap
│   ├── x86_64-w64-mingw32-elfedit
│   ├── x86_64-w64-mingw32-g++
│   ├── x86_64-w64-mingw32-gcc
│   ├── x86_64-w64-mingw32-gcc-11.3.0
│   ├── x86_64-w64-mingw32-gcc-ar
│   ├── x86_64-w64-mingw32-gcc-nm
│   ├── x86_64-w64-mingw32-gcc-ranlib
│   ├── x86_64-w64-mingw32-gcov
│   ├── x86_64-w64-mingw32-gcov-dump
│   ├── x86_64-w64-mingw32-gcov-tool
│   ├── x86_64-w64-mingw32-gendef
│   ├── x86_64-w64-mingw32-gfortran
│   ├── x86_64-w64-mingw32-gprof
│   ├── x86_64-w64-mingw32-ld
│   ├── x86_64-w64-mingw32-ld.bfd
│   ├── x86_64-w64-mingw32-lto-dump
│   ├── x86_64-w64-mingw32-nm
│   ├── x86_64-w64-mingw32-objcopy
│   ├── x86_64-w64-mingw32-objdump
│   ├── x86_64-w64-mingw32-ranlib
│   ├── x86_64-w64-mingw32-readelf
│   ├── x86_64-w64-mingw32-size
│   ├── x86_64-w64-mingw32-strings
│   ├── x86_64-w64-mingw32-strip
│   ├── x86_64-w64-mingw32-widl
│   ├── x86_64-w64-mingw32-windmc
│   └── x86_64-w64-mingw32-windres
├── distro-info
│   ├── CHANGELOG.md
│   ├── licenses
│   ├── patches
│   └── scripts
├── i686-w64-mingw32
│   ├── bin
│   ├── include
│   └── lib
├── include
│   ├── ctf-api.h
│   └── ctf.h
├── lib
│   ├── bfd-plugins
│   ├── gcc
│   ├── libctf.a
│   ├── libctf.la
│   ├── libctf-nobfd.a
│   ├── libctf-nobfd.la
│   ├── libctf-nobfd.so -> libctf-nobfd.so.0.0.0
│   ├── libctf-nobfd.so.0 -> libctf-nobfd.so.0.0.0
│   ├── libctf-nobfd.so.0.0.0
│   ├── libctf.so -> libctf.so.0.0.0
│   ├── libctf.so.0 -> libctf.so.0.0.0
│   └── libctf.so.0.0.0
├── lib64
│   ├── libcc1.a
│   ├── libcc1.la
│   ├── libcc1.so -> libcc1.so.0.0.0
│   ├── libcc1.so.0 -> libcc1.so.0.0.0
│   └── libcc1.so.0.0.0
├── libexec
│   ├── libfl.so.2 -> libfl.so.2.0.0
│   ├── libfl.so.2.0.0
│   ├── libgcc_s.so.1
│   ├── libgmp.so.10 -> libgmp.so.10.4.1
│   ├── libgmp.so.10.4.1
│   ├── libiconv.so.2 -> libiconv.so.2.6.1
│   ├── libiconv.so.2.6.1
│   ├── libisl.so.23 -> libisl.so.23.1.0
│   ├── libisl.so.23.1.0
│   ├── libmpc.so.3 -> libmpc.so.3.2.1
│   ├── libmpc.so.3.2.1
│   ├── libmpfr.so.6 -> libmpfr.so.6.1.0
│   ├── libmpfr.so.6.1.0
│   ├── libstdc++.so.6 -> libstdc++.so.6.0.29
│   ├── libstdc++.so.6.0.29
│   ├── libz.so.1 -> libz.so.1.2.11
│   └── libz.so.1.2.11
├── README.md
├── share
│   └── gcc-11.3.0
├── x86_64-pc-linux-gnu
│   ├── i686-w64-mingw32
│   └── x86_64-w64-mingw32
└── x86_64-w64-mingw32
    ├── bin
    ├── include
    └── lib

24 directories, 106 files
```

### Test

To check if the manually installed GCC starts, use something like:

```console
$ ~/.local/xPacks/mingw-w64-gcc/xpack-mingw-w64-gcc-{{ page.version }}-{{ page.xpack-subversion }}/bin/x86_64-w64-mingw32-gcc --version
x86_64-w64-mingw32-gcc (xPack MinGW-w64 GCC x86_64) {{ page.version }}
```

{% endcapture %}

{% include platform-tabs.html %}

{% include warning.html content="**DO NOT** add the toolchain path to
the user or system path!" %}
