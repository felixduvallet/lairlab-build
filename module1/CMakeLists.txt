cmake_minimum_required(VERSION 2.6.0)

# pull in the pods macros. See cmake/pods.cmake for documentation
set(POD_NAME planner)
include(cmake/pods.cmake)

# require python
find_package(PythonInterp REQUIRED)

# install all python files in the python/ subdirectory
pods_install_python_packages(${CMAKE_CURRENT_SOURCE_DIR}/python)

# This pod is for running the python code.
pods_install_python_script(module1-hello hello.run)
