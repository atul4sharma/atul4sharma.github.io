---
title: Cmake - building *targets*
tags: ['cmake']
category: til
classes: wide
toc: true
---

## Executables  

### `add_executable` command  

  ```make
  add_executable(targetName [WIN32] [MACOSX_BUNDLE]
                   [EXCLUDE_FROM_ALL]
                   source1 [source2 ...]
  )
  ```  
  Tells the CMake to create an executable from the source files.  
  When the project is built, an executable with the `targetName` will be created in the `build` directory with a platform-dependent name(\<targetName\>.exe of windows, targetName on unix-based platforms etc.)  

  - **WIN32**: When building the executable on Windows platform, this option instructs CMake to build the executable as Windows GUI application.  
    This option is ignored for other platforms.  
  - **MACOSX_BUNDLE**: When present, this option directs CMake to build an app bundle when building on an Apple platform.  
    On non-Apple platforms, the MACOSX_BUNDLE keyword is ignored.  
  - **EXCLUDE_FROM_ALL**: If an executable is defined with the EXCLUDE_FROM_ALL option, it will not be included in that default ALL target.
    The executable will then only be built if it is explicitly requested by the build command or if it is a dependency for another target that is part of the default ALL build.  


## Libraries  
  
### `add_libary` command  
  
  ```make
  add_library(targetName [STATIC | SHARED | MODULE]
                [EXCLUDE_FROM_ALL]
                source1 [source2 ...]
  )
  ```
  - **targetName**: Name of the library to build.
  - **EXCLUDE_FROM_ALL**: Same effect as it has in `add_executable`
  - Type of library to be built 
    - **STATIC**: static library or archive. Windows `targetName.lib` on unix like platform `targetName.a`.  
    - **SHARED**: shared or dynamically linked library. Windows `targetName.dll`, Apple platforms `libtargetName.dylib` and on other Unix-like platforms `libtargetName.so`.  
    - **MODULE**: library that is somewhat like a shared library, but is intended to be loaded dynamically at run-time rather than being linked directly to a library or executable.
    In case someone omit these keywords, the choice is determined by the CMake variable `BUILD_SHARED_LIBS`. It it is true then SHARED library will be build otherwise STATIC library will be build. Ways to define the variable.
    a) commandline: `cmake -DBUILD_SHARED_LIBS=YES /path/to/source`
    b) inside CMakeLists.txt: Use this command `set(BUILD_SHARED_LIBS YES)`
 

## Linking the targets  

### `target_link_libraries` command  

  ```make
  target_link_libraries(targetName
         <PRIVATE|PUBLIC|INTERFACE> item1 [item2 ...]
        [<PRIVATE|PUBLIC|INTERFACE> item3 [item4 ...]]
  ... )
  ```
  CMake allows the developer to handle the dependency relationships among libraries in an elegant manner.
  Assuming `library A` needing `library B`, so **A** is linked to **B**.
  - **PRIVATE**: Private dependencies specify that `library A` uses `library B` in its own internal implementation. Anything else that links to `library A` doesn’t need to know about B because it is an internal implementation detail of A.
  - **PUBLIC**: Public dependencies specify that not only does `library A` use `library B` internally, it also uses B in its interface. This means that A cannot be used without B, so anything that uses A will also have a direct dependency on B.  
  - **INTERFACE**: Interface dependencies specify that in order to use `library A`, parts of `library B` must also be used. This differs from a public dependency in that library A doesn’t require B internally, it only uses B in its interface. An example of where this is useful is when working with library targets defined using the INTERFACE form of add_library(), such as when using a target to represent a header-only library’s dependencies
  `target_link_libraries` can also be used to link non-targets. One can pass full path to a library file or just plain library file as well. The options are passed to the linker accordingly.  



## References
Chapter 4 - [Professional CMake: A Practical Guide - By Craig Scott](https://www.goodreads.com/book/show/40776823-professional-cmake)

