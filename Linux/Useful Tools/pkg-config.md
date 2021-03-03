# pkg-config
- pkg-config is a computer program that defines and supports a unified interface for querying installed libraries for the purpose of compiling software that depends on them.
- It allows programmers and installation scripts to work without explicit knowledge of detailed library path information.
- It outputs various information about installed libraries. This information may include:
	- Parameters for C or C++ compiler
	- Parameters for linker
	- Version of the package in question
- When a library is installed, a .pc file should be included and placed into a directory with other .pc files.
- To see where pkg-config (version 0.24 or later) searches for installed libraries by default, use the following command:
	```pkg-config --variable pc_path pkg-config```
- To add to that path, set the PKG_CONFIG_PATH environment variable.
- Here is an example .pc file for libpng:
```
prefix=/usr/local
exec_prefix=${prefix}
libdir=${exec_prefix}/lib
includedir=${exec_prefix}/include
 
Name: libpng
Description: Loads and saves PNG files
Version: 1.2.8
Libs: -L${libdir} -lpng12 -lz
Cflags: -I${includedir}/libpng12
```
- Here is an example of usage of pkg-config while compiling:
```
gcc -o test test.c $(pkg-config --libs --cflags libpng)
```