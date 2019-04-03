project(libunwind)
cmake_minimum_required(VERSION 2.8)

include_directories(../include . ../include/tdep-x86_64)

add_executable(test_bt Ltest-bt.c ident.c)
target_link_libraries(test_bt unwind_static lzma)

add_test (NAME test_bt COMMAND test_bt)
