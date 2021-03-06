#------------------------------------------------------------------------------
# General Projects Settings
#------------------------------------------------------------------------------
cmake_minimum_required (VERSION 3.11)
set(PROJECT_NAME SOIL)
project(${PROJECT_NAME}
        LANGUAGES C
)

#------------------------------------------------------------------------------
# The main executable
#------------------------------------------------------------------------------
add_library(${PROJECT_NAME}
        src/image_DXT.c
        src/image_helper.c
        src/SOIL.c
        src/stb_image_aug.c
        )

target_compile_options(${PROJECT_NAME} PRIVATE -Wall)

if(NOT CMAKE_BUILD_TYPE)
    set(CMAKE_BUILD_TYPE ${CMAKE_BUILD_TYPE} Debug)
endif()

if(NOT BUILD_TYPE)
    set(BUILD_TYPE ${BUILD_TYPE} "desktop")
endif()

#------------------------------------------------------------------------------
# Detect emscripten is used.
#------------------------------------------------------------------------------
if(${BUILD_TYPE} STREQUAL webassembly)

    set(CMAKE_C_COMPILER "emcc")
    set(CMAKE_CXX_COMPILER "em++")

    set_target_properties(${PROJECT_NAME} PROPERTIES OUTPUT_NAME ${PROJECT_NAME})

    string(APPEND CMAKE_C_FLAGS " -Wall")
    string(APPEND CMAKE_C_FLAGS " -s DEMANGLE_SUPPORT=1")
    string(APPEND CMAKE_C_FLAGS " -s DISABLE_EXCEPTION_CATCHING=2")
    string(APPEND CMAKE_C_FLAGS " -s WASM=1")

endif()