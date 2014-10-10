cmake_minimum_required(VERSION 2.6.0)

set(POD_NAME module2)
project(module2-project)

include(cmake/pods.cmake)

find_package(PkgConfig REQUIRED)
find_package(OpenGL REQUIRED)

add_subdirectory(src)
