
cmake_minimum_required(VERSION 3.6)
project(ray_tracer LANGUAGES CXX CUDA)
enable_language(CUDA)

set(CMAKE_CXX_STANDARD 11)

set(CMAKE_VERBOSE_MAKEFILE 1)
set(APP_VERSION_MAJOR 1)
set(APP_VERSION_MINOR 0)

set(APP_TARGET ray_tracer)

add_subdirectory(imgui)
include_directories(${PROJECT_SOURCE_DIR})
add_executable(${APP_TARGET} src/main.cu)
target_link_libraries(${APP_TARGET} imgui)

# glfw
find_package(glfw3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})
link_libraries(${GLFW_LIBRARY_DIRS})

# opengl
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

# glew
find_package(GLEW REQUIRED)
include_directories(${GLEW_INCLUDE_DIRS})

if (APPLE)
    find_library(COCOA_LIBRARY Cocoa)
    find_library(OpenGL_LIBRARY OpenGL)
    find_library(IOKIT_LIBRARY IOKit)
    find_library(COREVIDEO_LIBRARY CoreVideo)
    SET(EXTRA_LIBS ${COCOA_LIBRARY} ${OpenGL_LIBRARY} ${IOKIT_LIBRARY} ${COREVIDEO_LIBRARY})
endif (APPLE)

if (WIN32)
# nothing now
endif (WIN32)

target_link_libraries(
        ${APP_TARGET}
        ${OPENGL_LIBRARIES}
        glfw
        ${GLEW_LIBRARIES}
        ${EXTRA_LIBS}
)