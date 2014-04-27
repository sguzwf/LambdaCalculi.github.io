---
title: CMake Tips
---

# Intorduciton
[**CMake**](http://www.cmake.org/) is a collection of building, testing and packaging tools. Admittedly autoconf/automake is the de facto tools for opensource project in a long period of time, there are many reasons for chosing CMake: it is powerfull and easy to use, supports various IDE, and cross platform. 

In this article I write down various snippets during my daily usage of CMake/CTest/CPack. In addtion, I assumed that the readers are already familiar with CMake, otherwise [Mastering CMake](http://www.kitware.com/products/books/CMakeBook.htmll) and the [official online doc](http://www.cmake.org/cmake/help/documentation.html) are the best material for reference.

# Tips
1. **Generate both static and shared library file**  
    add_library(foo SHARED ${SRC_LIST})
    add_library(foo_static STATIC ${SRC_LIST})
    set_target_properties(foo_static PROPERTIES OUTPUT_NAME "foo")

2. **Use different compiler**  
  The CMAKE_C_COMPILER and CMAKE_CXX_COMPILER are used for these purpose, but those variable must be set before project() command. The recommended way is using "cmake -D", i.e.:
    cmake -D CMAKE_CXX_COMPILER=/path/to/your/compiler

3. **Retrieve the absolute path**  
There're three frequently-used variables:
    * CMAKE_SOURCE_DIR
      The full path to the top level of source tree
    * CMAKE_CURRENT_SOURCE_DIR
      The full path to the source directory currently being processed
    * CMAKE_CURRENT_BINARY_DIR
      The full path to the build directory that is currently being processed


4. **Pass value to parent directory.**  
Certainly it is not a good practice to pass value to parent directory, sometimes it's reasonable to do so. Here are three methods:
    * use PARENT_SCOPE with set(the simplest method)
      in subdir: set(VAR_IN_SUB "put something here" PARENT_SCOPE)
    * set variable in sub directory, and then get its definition
      in subdir: set(VAR_IN_SUB "put something here")
      in current dir: get_directory_property(VAR DIRECTORY subdir DEFINITION VAR_IN_SUB)
    * set directory property in sub directory, and then get its value
      in subdir: set_directory_properties(PROPERTIES PRO_IN_SUB "put something here"
      in current dir: get_directory_property(VAR DIRECTORY subdir PRO_IN_SUB)


5. **Generate version, build time/host etc. info.**



# Final words
Note that this article will be updated from time to time, please feel free to contact me if you have any comment, suggestion and criticism.
