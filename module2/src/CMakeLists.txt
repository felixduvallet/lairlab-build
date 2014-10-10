add_executable(module2-hello
        hello.cpp
    )

# This actually puts the binary in the correct place.
pods_install_executables(module2-hello)
