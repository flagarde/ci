cmake_minimum_required(VERSION 3.0)

project(Test LANGUAGES C CXX)

message(STATUS "${CMAKE_VERSION}")

add_executable(main main.cpp)
