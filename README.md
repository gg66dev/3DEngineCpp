3DEngineCpp
==

It's like the 3D Game Engine, except in C++

## Dependencies##
- [CMAKE](http://www.cmake.org/)
- [GLEW](http://glew.sourceforge.net/)
- [SDL2](http://www.libsdl.org/)
- [ASSIMP](http://assimp.sourceforge.net/)


## clone repo with submodules

```
git clone git@github.com:gg66dev/3DEngineCpp.git 
git submodule update --init --recursive
```

## Build

```
cmake -B Build
cmake --build Build
cp Build\lib\assimp\bin\Debug\assimp-vc143-mtd.dll Build\
cp -rf res\ Build\
```

## Run

```
cd Build
Debug\3DEngineCpp.exe
```




##Additional Credits##
- Etay Meiri, for http://ogldev.atspace.co.uk/ which inspired the base code for this repository.
- [@mxaddict](https://github.com/mxaddict) for setting up the awesome CMake build system
- Everyone who's created or contributed to issues and pull requests, which make the project better!
