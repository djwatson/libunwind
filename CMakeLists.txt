project(libunwind)
cmake_minimum_required(VERSION 2.8)
enable_testing ()
include(CheckIncludeFile)

CHECK_INCLUDE_FILE("elf.h" HAVE_ELF_H)

configure_file(config.h.cmake config.h)
add_definitions(-DHAVE_CONFIG_H)
add_definitions(-D_GNU_SOURCE)

add_subdirectory(src)
add_subdirectory(tests)
