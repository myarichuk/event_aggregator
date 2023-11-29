cmake_minimum_required(VERSION 3.21)
project(EventAggregator VERSION 0.1.0 LANGUAGES CXX)

if(WIN32)
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set(VCPKG_TARGET_TRIPLET "x64-windows" CACHE STRING "")
    else()
        set(VCPKG_TARGET_TRIPLET "x86-windows" CACHE STRING "")
    endif()
elseif(UNIX AND NOT APPLE)
    if(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set(VCPKG_TARGET_TRIPLET "x64-linux" CACHE STRING "")
    else()
        set(VCPKG_TARGET_TRIPLET "x86-linux" CACHE STRING "")
    endif()
else(APPLE)
    if(CMAKE_OSX_ARCHITECTURES STREQUAL "arm64")
        set(VCPKG_TARGET_TRIPLET "arm64-osx" CACHE STRING "")
    elseif(CMAKE_SIZEOF_VOID_P EQUAL 8)
        set(VCPKG_TARGET_TRIPLET "x64-osx" CACHE STRING "")
    else()
        message(FATAL_ERROR "Unsupported architecture on macOS")
    endif()
endif()

# Add your header-only library
add_library(library INTERFACE)
target_include_directories(library INTERFACE ${CMAKE_CURRENT_SOURCE_DIR}/include)
target_compile_features(library INTERFACE cxx_std_23) # Use C++23 standard for consumers of the library

# Add test directory
enable_testing()
add_subdirectory(tests)
