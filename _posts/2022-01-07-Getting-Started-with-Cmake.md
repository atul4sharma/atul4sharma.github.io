---
title: Getting Started with CMake
tags: ['cmake']
category: til
classes: wide
---

[CMake](https://cmake.org/) is an open-source, cross-platform family of tools designed to build, test and package software. CMake is used to control the software compilation process using simple platform and compiler independent configuration files, and generate native makefiles and workspaces that can be used in the compiler environment of your choice. 

> I am skipping installation instructions and jumping directly to the usage.  
> Installed cmake version is 3.22.1


## Minimal C++ Project  

- #### Project structure  

  ```bash
  <lab_dir>
  ├── build
  └── src
      ├── CMakeLists.txt
      └── main.cpp
  
  2 directories, 2 files
  ```

- #### `main.cpp`  

  ```cpp
  #include <iostream>
  #include <functional>
  
  int main()
  {
    [out = std::ref(std::cout << "Hello ")]() {
      out.get() << "World\n";
    }();
    return 0;
  }
  ```

- #### `CMakeLists.txt`  

  ```make
  cmake_minimum_required(VERSION 3.5)
  project(lab)
  add_compile_options(-Wall -Wextra -Wpedantic)
  add_executable(lab main.cpp)
  target_compile_features(lab PRIVATE cxx_lambda_init_captures)
  install(TARGETS lab DESTINATION bin)
  ```

- #### Run following commands  

  ```bash
  cd build
  cmake ../src
  cmake --build . --config Release --target lab
  ```

> Your build is ready!!  
> An executable with the name lab will be generated in the `build` directory

- #### Running the executable

  ```bash
  ➤ ./lab
  Hello World
  ```


---

### Understanding the `CMakeLists.txt` file 
All CMake projects start with a file called `CMakeLists.txt` and it is expected to be placed at the top of the source tree.
`CMakeLists.txt` is just an ordinary text files that contains *cmake commands*.  
CMake defines its own language which has many things, such as variables, functions, macros, conditional logic, looping, code comments and so on. 

The bare minimum commands required for any cmake projects are:   
```make
cmake_minimum_required(VERSION 3.5)
project(lab)
add_executable(lab main.cpp)
```

- `cmake_minimum_required` command  
  `cmake_minimum_required(VERSION major.minor[.patch[.tweak]])`   
  - This should be the first line of `CMakeLists.txt`. It specifies the minimum version of CMake the project needs.  
    This ensures that the particular CMake funtionality is available before proceeding.  
  - It enforces policy settings to match CMake behaviour to the specified version.  

- `project` command  
  `project(projectName [VERSION major[.minor[.patch[.tweak]]]] [LANGUAGES languageName ...])`  
    - projectName is required. Can contain alphabets, numbers, underscore, hyphen  
    - VERSION is optional. Can be used to specify the project version here and other parts of the project can refer to it.  
    - LANGUAGES defines the programming languages that should be enabled for the project.  

  One of it's important responsibility is to check the compilers for each enabled language and ensure that they are able to compile and link successfully. 

- `add_executable` command  
  `add_executable(targetName source1 [source2 ...])`  
  Tells the CMake to create an executable from the source files.  
  When the project is built, an executable with the `targetName` will be created in the `build` directory with a platform-dependent name(\<targetName\>.exe of windows, targetName on unix-based platforms etc.)  

- **Adding comments**: Any line beginning with `#` is considered as comment.


#### Summary of commands used in CMakeLists.txt for lab project

Command | Summary 
---|---  
cmake_minimum_required | Sets the minimum required version of cmake for a project.  
project | Sets the name of the project.  
add_compile_options | Add options to the compilation of source files.  
add_executable | Add an executable to the project using the specified source files.  
target_compile_features | Add expected compiler features to a target. `target_compile_features(<target> <PRIVATE|PUBLIC|INTERFACE> <feature> [...])`  <br/>Adding this automatically figure out the `std=c++` flag to be used for compiler  
install | Specify rules to run at install time.  


## References
Chapter 3 - [Professional CMake: A Practical Guide - By Craig Scott](https://www.goodreads.com/book/show/40776823-professional-cmake)

