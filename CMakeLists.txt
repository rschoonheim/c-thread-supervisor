cmake_minimum_required(VERSION 4.1)
project(thread_supervisor C)

set(CMAKE_C_STANDARD 23)

add_executable(
        thread_supervisor
        main.c
)
