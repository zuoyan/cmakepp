# Downloading and Including `cmakepp` in a `CMakeLists.txt`

This sample shows you how to include `cmakepp` in your `CMakeLists.txt`. If you do not have `cmakepp` the script automatically downloads it from github.


## Prerequisites

* CMake version `>=2.8.12`
* `bash`, `powershell` or `cmd.exe` 
* `cmakepp.cmake` 
 
## Usage

```bash
# create a build dir
sample folder/> mkdir build 
sample folder/> cd build 
# generate the project
sample folder/build/> cmake -DCMAKE_RUNTIME_OUTPUT_DIRECTORY=bin-DCMAKE_RUNTIME_OUTPUT_DIRECTORY_DEBUG=bin .. 
-- Building for: Visual Studio 12 2013
-- The C compiler identification is ;MSVC 18.0.31010.0
-- The CXX compiler identification is ;MSVC 18.0.31010.0
-- Check for working C compiler using: Visual Studio 12 2013
-- Check for working C compiler using: Visual Studio 12 2013 -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Check for working CXX compiler using: Visual Studio 12 2013
-- Check for working CXX compiler using: Visual Studio 12 2013 -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- Configuring done
-- Generating done
-- Build files have been written to: C:/Temp/cutil/temp/mktemp_2QrNe/build

# build the configured project
sample_folder/build/> cmake --build . 
... build output ...
# run executable
sample folder/build/> bin/myexe 
hello

```

*CMakeLists.txt*: 
```cmake
cmake_minimum_required(VERSION 2.8.12)

## be sure to have the compiled cmakepp in the project dir
if(NOT EXISTS "${CMAKE_SOURCE_DIR}/cmakepp.cmake")
    file(DOWNLOAD "https://github.com/toeb/cmakepp/releases/download/v0.0.3/cmakepp.cmake" "${CMAKE_SOURCE_DIR}/cmakepp.cmake")
endif()
include("cmakepp.cmake")

## now that cmakepp is available it is ready to use.
## and you can use it in you normal CMakeLists.txt
project(sample03)

# write a simple main file
fwrite("main.cpp" "
#include <iostream>
int main(){
  std::cout << \"hello\" << std::endl;
}")

# and create an executable form it
add_executable(myexe main.cpp)
```


