
cmake_minimum_required(VERSION 3.12)

project(RixJson)

set(CMAKE_C_COMPILER "clang")
set(CMAKE_CXX_COMPILER "clang++")
set(CMAKE_CXX_STANDARD 11)

add_compile_options("-m64")
add_compile_options("--debug")

include_directories(/opt/local/include ./inc)


set(OUTPUT_DIR ${PROJECT_BINARY_DIR}/output)
set(RPATH "${OUTPUT_DIR}")
# Lib
aux_source_directory(./src SRC_LIST)

message("-- Building RixJson Library...")

add_library(RixJson SHARED ${SRC_LIST})
target_link_libraries(RixJson)

install(TARGETS RixJson DESTINATION ${OUTPUT_DIR})


# Test
aux_source_directory(./test TEST_SRC)
message("-- Buidling test...")

add_executable(Test ${TEST_SRC})
set_target_properties(Test PROPERTIES INSTALL_RPATH ${RPATH})
target_link_libraries(Test RixJson)

install(TARGETS Test DESTINATION ${OUTPUT_DIR})


