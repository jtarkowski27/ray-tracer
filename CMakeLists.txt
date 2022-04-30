cmake_minimum_required(VERSION 3.8 FATAL_ERROR)
project(ray_tracer LANGUAGES CXX CUDA)
enable_language(CUDA)
add_executable(ray_tracer src/main.cu)