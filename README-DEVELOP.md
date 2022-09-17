TODO

```sh
bash ${HOME}/Work/mingw-w64-gcc-xpack.git/scripts/helper/build-native.sh --develop --without-pdf
bash ${HOME}/Work/mingw-w64-gcc-xpack.git/scripts/helper/build-native.sh --develop --win

```

## Patches

A good source of patches for Windows is
[MSYS2](https://github.com/msys2/MINGW-packages/tree/master/mingw-w64-gcc).

In the `forks/gcc.git` repo:

- select tag like `releases/gcc-12.2.0`
- checkout
- create new branch `gcc-12.2.0-xpack`
- select the commits from the previous release
- cherry pick
- if empty, it was already applied
