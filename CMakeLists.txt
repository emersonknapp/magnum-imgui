cmake_minimum_required(VERSION 3.0.2)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/modules/")

option(BUILD_EXAMPLE "Build example" ON)
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

add_compile_definitions(IMGUI_IMPL_OPENGL_LOADER_CUSTOM="gl.h")
include_directories(imgui src)

include(imgui.cmake)
add_subdirectory(src)
