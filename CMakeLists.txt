cmake_minimum_required(VERSION 3.0.2)

set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} "${PROJECT_SOURCE_DIR}/modules/")

option(BUILD_EXAMPLE "Build example" ON)
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

add_compile_definitions(IMGUI_IMPL_OPENGL_LOADER_CUSTOM="gl.h")
include_directories(imgui src)
# project(imgui CXX)

set(CMAKE_DEBUG_POSTFIX d)
set(CMAKE_WINDOWS_EXPORT_ALL_SYMBOLS ON)

set(IMGUI_NAME imgui)

set(IMGUI_INCLUDES_PUBLIC
    imgui/imgui.h
    imgui/imconfig.h
)

set(IMGUI_INCLUDES_PRIVATE
    imgui/imgui_internal.h
)

file(GLOB IMGUI_SOURCES imgui/*.cpp)

add_library(${IMGUI_NAME}
    ${IMGUI_INCLUDES_PUBLIC}
    ${IMGUI_INCLUDES_PRIVATE}
    ${IMGUI_SOURCES}
)

target_include_directories(${IMGUI_NAME} PUBLIC $<INSTALL_INTERFACE:include>)

install(TARGETS ${IMGUI_NAME}
    EXPORT IMGUIExport
    RUNTIME DESTINATION bin
    LIBRARY DESTINATION lib
    ARCHIVE DESTINATION lib
)

install(EXPORT IMGUIExport FILE ${IMGUI_NAME}Config.cmake NAMESPACE ${IMGUI_NAME}:: DESTINATION share/${IMGUI_NAME})

if(NOT IMGUI_SKIP_HEADERS)
    install(
        FILES ${IMGUI_INCLUDES_PUBLIC}
        DESTINATION include
    )
endif()

add_subdirectory(src)
