---
title: '[Protobuf] (De)Serialize with Protobuf'
published: true
---

## Intro

You should use Protobuf when you need to (de)serialize binary your data.

## Installing

#### Ubuntu
```
sudo apt install protobuf-compiler
sudo apt install libprotobuf-dev protobuf-compiler
```  
OR  
 
There is a good [manual](https://github.com/protocolbuffers/protobuf/blob/master/src/README.md)

## Syntax
```
[proto] message = class [C++]
[proto] package = namespace [C++]
```

## Using in C++ project

### Create human.proto

```proto
syntax = "proto3";

message Location {
    string location = 1;
    int32 x = 2;
    int32 y = 3;
}

message Human {
    string name = 1;
    int32 age = 2;
    Location location = 3;
}
```
### Compile human.proto
`protoc -I . --cpp_out . human.proto`

Your folder looks like:  
```bash
.
├── human.pb.cc
├── human.pb.h
└── human.proto
```

### Build the project with Protobuf  

CMakeLists.txt  

```cmake
cmake_minimum_required(VERSION 3.10)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED on)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Werror")

find_package(Protobuf REQUIRED)

include_directories(${PROTOBUF_INCLUDE_DIR})
include_directories(${CMAKE_CURRENT_BINARY_DIR})

protobuf_generate_cpp(PROTO_SRC PROTO_HEADER human.proto)

add_library(proto ${PROTO_HEADER} ${PROTO_SRC})

add_executable(main main.cpp ${PROTO_SRC} ${PROTO_HDRS})

target_link_libraries(main ${PROTOBUF_LIBRARY})

# To build *nix makefiles, run: cmake -G "Unix Makefiles" ..
```  
Run:  
`cmake -G "Unix Makefiles" ..'

Your folder should looks like:
```bash
.
├── CMakeCache.txt
├── CMakeFiles
│   ├── 3.10.2
│   │   ├── CMakeCCompiler.cmake
│   │   ├── CMakeCXXCompiler.cmake
...
├── cmake_install.cmake
├── CMakeLists.txt
├── human.pb.cc
├── human.pb.h
├── human.proto
├── main.cpp
└── Makefile
```  
You can see that CMake generated the Makefile.  

Not, let's modify the `main.cpp`
```cpp
#include <human.pb.h>
#include <iostream>

int main()
{
    Location human_location;
    human_location.set_location("Africa");
    human_location.set_x(32);
    human_location.set_y(234);

    std::cout << "human_location.location(): " << human_location.location() << std::endl;
    std::cout << "human_location.x()       : " << human_location.x() << std::endl;
    std::cout << "human_location.y()       : " << human_location.y() << std::endl;

    Human human;
    if (human.has_location())
        std::cout << "human have the location!\n";
    else
        std::cout << "human have not thelocation!\n";

    human_location.set_location("Europe");

    *human.mutable_location() = human_location;
    if (human.has_location())
    {
        std::cout << "human have the location!\n";

        std::cout << "human.location()     : " << human.location().location() << std::endl;
        std::cout << "human.location().x() : " << human.location().x() << std::endl;
        std::cout << "human.location().y() : " << human.location().y() << std::endl;
    }
    else
    {
        std::cout << "human have not thelocation!\n";
    }
    std::cout << "Done!\n";
}
```  
Note:  
 for the single field: set/get  
 for the string and nested structures in addition: mutable_*  

Let's test it!  
Run:  
```
make all
./main
```   
Expected output:  
```bash
human_location.location(): Africa
human_location.x()       : 32
human_location.y()       : 234
human have not thelocation!
human have the location!
human.location()     : Europe
human.location().x() : 32
human.location().y() : 234
Done
```
