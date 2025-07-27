cmake_minimum_required(VERSION 3.22)

project(FIRST_STEPS)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_CXX_FLAGS "-static")

add_executable(first-steps
    main.cpp
)
