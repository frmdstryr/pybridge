# Sets the minimum version of CMake required to build your native library.
# This ensures that a certain set of CMake features is available to
# your build.

cmake_minimum_required(VERSION 3.4.1)

find_program(PYTHON "python")

if (PYTHON)
    set(SETUP_PY    "${CMAKE_CURRENT_BINARY_DIR}/app/src/main/python/atom/setup.py")
    set(DEPS        "${CMAKE_CURRENT_SOURCE_DIR}/module/__init__.py")
    set(OUTPUT      "${CMAKE_CURRENT_BINARY_DIR}/build")


    add_custom_command(OUTPUT ${OUTPUT}
                       COMMAND ${PYTHON}
                       ARGS setup.py build
                       DEPENDS ${DEPS})

    add_custom_target(target ALL DEPENDS ${OUTPUT})

    install(CODE "execute_process(COMMAND ${PYTHON} ${SETUP_PY} install)")
endif()
