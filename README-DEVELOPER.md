# Developer notes

## Output folder hierarchy

The scripts build separate 32/64-bit versions of all tools, installed in
separate folders ("x86_64-w64-mingw32" "i686-w64-mingw32");
the binaries are installed in `bin` and are prefixed.

The target specific dependencies are also installed in separate folders
below a folder specific to the build machine (like `x86_64-apple-darwin21.6.0`).

```console
├── README.md
├── bin
│   ├── i686-w64-mingw32-addr2line
│   ├── i686-w64-mingw32-ar
│   ├── i686-w64-mingw32-as
│   ├── i686-w64-mingw32-c++
│   ├── i686-w64-mingw32-c++filt
│   ├── i686-w64-mingw32-cpp
│   ├── i686-w64-mingw32-dlltool
│   ├── i686-w64-mingw32-dllwrap
│   ├── i686-w64-mingw32-elfedit
│   ├── i686-w64-mingw32-g++
│   ├── i686-w64-mingw32-gcc
│   ├── i686-w64-mingw32-gcc-12.2.0
│   ├── i686-w64-mingw32-gcc-ar
│   ├── i686-w64-mingw32-gcc-nm
│   ├── i686-w64-mingw32-gcc-ranlib
│   ├── i686-w64-mingw32-gcov
│   ├── i686-w64-mingw32-gcov-dump
│   ├── i686-w64-mingw32-gcov-tool
│   ├── i686-w64-mingw32-gendef
│   ├── i686-w64-mingw32-gfortran
│   ├── i686-w64-mingw32-gprof
│   ├── i686-w64-mingw32-ld
│   ├── i686-w64-mingw32-ld.bfd
│   ├── i686-w64-mingw32-lto-dump
│   ├── i686-w64-mingw32-nm
│   ├── i686-w64-mingw32-objcopy
│   ├── i686-w64-mingw32-objdump
│   ├── i686-w64-mingw32-ranlib
│   ├── i686-w64-mingw32-readelf
│   ├── i686-w64-mingw32-size
│   ├── i686-w64-mingw32-strings
│   ├── i686-w64-mingw32-strip
│   ├── i686-w64-mingw32-widl
│   ├── i686-w64-mingw32-windmc
│   ├── i686-w64-mingw32-windres
│   ├── x86_64-w64-mingw32-addr2line
│   ├── x86_64-w64-mingw32-ar
│   ├── x86_64-w64-mingw32-as
│   ├── x86_64-w64-mingw32-c++
│   ├── x86_64-w64-mingw32-c++filt
│   ├── x86_64-w64-mingw32-cpp
│   ├── x86_64-w64-mingw32-dlltool
│   ├── x86_64-w64-mingw32-dllwrap
│   ├── x86_64-w64-mingw32-elfedit
│   ├── x86_64-w64-mingw32-g++
│   ├── x86_64-w64-mingw32-gcc
│   ├── x86_64-w64-mingw32-gcc-12.2.0
│   ├── x86_64-w64-mingw32-gcc-ar
│   ├── x86_64-w64-mingw32-gcc-nm
│   ├── x86_64-w64-mingw32-gcc-ranlib
│   ├── x86_64-w64-mingw32-gcov
│   ├── x86_64-w64-mingw32-gcov-dump
│   ├── x86_64-w64-mingw32-gcov-tool
│   ├── x86_64-w64-mingw32-gendef
│   ├── x86_64-w64-mingw32-gfortran
│   ├── x86_64-w64-mingw32-gprof
│   ├── x86_64-w64-mingw32-ld
│   ├── x86_64-w64-mingw32-ld.bfd
│   ├── x86_64-w64-mingw32-lto-dump
│   ├── x86_64-w64-mingw32-nm
│   ├── x86_64-w64-mingw32-objcopy
│   ├── x86_64-w64-mingw32-objdump
│   ├── x86_64-w64-mingw32-ranlib
│   ├── x86_64-w64-mingw32-readelf
│   ├── x86_64-w64-mingw32-size
│   ├── x86_64-w64-mingw32-strings
│   ├── x86_64-w64-mingw32-strip
│   ├── x86_64-w64-mingw32-widl
│   ├── x86_64-w64-mingw32-windmc
│   └── x86_64-w64-mingw32-windres
├── distro-info
│   ├── CHANGELOG.md
│   ├── licenses
│   ├── patches
│   └── scripts
├── i686-w64-mingw32
│   ├── bin
│   ├── include
│   └── lib
├── include
│   ├── ctf-api.h
│   ├── ctf.h
│   └── libiberty
├── lib
│   ├── bfd-plugins
│   ├── gcc
│   ├── libcc1.0.so
│   ├── libcc1.a
│   ├── libcc1.la
│   ├── libcc1.so -> libcc1.0.so
│   ├── libctf-nobfd.0.dylib
│   ├── libctf-nobfd.a
│   ├── libctf-nobfd.dylib -> libctf-nobfd.0.dylib
│   ├── libctf-nobfd.la
│   ├── libctf.0.dylib
│   ├── libctf.a
│   ├── libctf.dylib -> libctf.0.dylib
│   ├── libctf.la
│   └── libiberty.a
├── libexec
│   ├── libgmp.10.dylib
│   ├── libiconv.2.dylib
│   ├── libisl.23.dylib
│   ├── libmpc.3.dylib
│   ├── libmpfr.6.dylib
│   ├── libz.1.2.11.dylib
│   ├── libz.1.dylib -> libz.1.2.11.dylib
│   └── libzstd.1.5.2.dylib
├── share
│   └── gcc-12.2.0
├── x86_64-apple-darwin21.6.0
│   ├── i686-w64-mingw32
│   └── x86_64-w64-mingw32
└── x86_64-w64-mingw32
    ├── bin
    ├── include
    └── lib

24 directories, 95 files
```

## Bootstrap

Compiling the Windows binaries require a bootstrap, which is more or
less the same thing, but configured to run on Linux, not on Windows
(the binaries are ELFs, not EXEs).

The bootstrap is built in a separate folder (`x86_64-pc-linux-gnu`),
and includes only a single target specific folder (`x86_64-w64-mingw32`)
since only 64-bit Windows binaries are finally created.

Note: The bootstrap cannot be replaced by an external mingw-gcc package
since it is mandatory to be of exactly the same version as the final
release, otherwise subtle header differences might break the build
(in theory it might be possible to configure the build to use
an older compiler and the current headers, but in practice this
proved tricky).

## DLLs

The compiled binaries refer to various DLLs.

```sh
% ls -l x86_64-w64-mingw32/lib/*.dll
-rwxr-xr-x  1 ilg  staff    38296 Dec  1 21:14 x86_64-w64-mingw32/lib/libatomic-1.dll
-rwxr-xr-x  1 ilg  staff   662864 Dec  1 21:14 x86_64-w64-mingw32/lib/libgcc_s_seh-1.dll
-rwxr-xr-x  1 ilg  staff  3132646 Dec  1 21:14 x86_64-w64-mingw32/lib/libgfortran-5.dll
-rwxr-xr-x  1 ilg  staff   261049 Dec  1 21:14 x86_64-w64-mingw32/lib/libgomp-1.dll
-rwxr-xr-x  1 ilg  staff   378712 Dec  1 21:14 x86_64-w64-mingw32/lib/libquadmath-0.dll
-rwxr-xr-x  1 ilg  staff    23251 Dec  1 21:14 x86_64-w64-mingw32/lib/libssp-0.dll
-rwxr-xr-x  1 ilg  staff  1990289 Dec  1 21:14 x86_64-w64-mingw32/lib/libstdc++-6.dll
-rwxr-xr-x  1 ilg  staff    61808 Dec  1 21:10 x86_64-w64-mingw32/lib/libwinpthread-1.dll
```

When running the binaries, this folder must be added to the Windows path.

## libwinpthread-1.dll

Due to the specifics of the MinGW-w64 build, the threading library is
not very well integrated into the build, and invoking the compiler
with `-static-libgcc -static-libstdc++` does not apply to this DLL,
so the resulting binaries might still have a reference to it.

