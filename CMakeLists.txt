cmake_minimum_required(VERSION 3.10)
project(CYaml C)

set(VERSION_MAJOR 2)
set(VERSION_MINOR 0)
set(VERSION_PATCH 0)
set(VERSION_DEVEL 1)
set(VERSION_STR ${VERSION_MAJOR}.${VERSION_MINOR}.${VERSION_PATCH})

set(BUILD_TESTING OFF)
add_subdirectory(vendor/libyaml)

add_library(LibCYaml STATIC src/mem.c src/free.c src/load.c src/save.c src/copy.c src/util.c src/utf8.c)
target_include_directories(LibCYaml PRIVATE include/ vendor/libyaml/include)
target_compile_definitions(LibCYaml PRIVATE VERSION_MAJOR=${VERSION_MAJOR} VERSION_MINOR=${VERSION_MINOR} VERSION_PATCH=${VERSION_PATCH})
target_link_libraries(LibCYaml yaml)

set_target_properties(LibCYaml PROPERTIES OUTPUT_NAME "cyaml")
