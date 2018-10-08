project(MagnumImGui CXX)

# Build library
find_package(Magnum REQUIRED
  Shaders
  MeshTools
  Primitives
  Sdl2Application)
find_package(SDL2 REQUIRED)



add_library(
    ${PROJECT_NAME}
    MagnumImGui.cpp
    # imgui_impl_magnum_gl3.cpp
    ../imgui/examples/imgui_impl_opengl3.cpp
    ${MagnumImGuiShaders_RCS}
)

target_link_libraries(${PROJECT_NAME}
  Magnum::Application
  Magnum::GL
  imgui
  )

install(TARGETS ${PROJECT_NAME}
  EXPORT MAGNUMIMGUIExport
  RUNTIME DESTINATION bin
  LIBRARY DESTINATION lib
  ARCHIVE DESTINATION lib
  )
install(FILES MagnumImGui.h DESTINATION "include/")
install(EXPORT MAGNUMIMGUIExport FILE ${PROJECT_NAME}Config.cmake NAMESPACE ${PROJECT_NAME}:: DESTINATION share/${PROJECT_NAME})

# Build exmaple
if(BUILD_EXAMPLE)
  add_executable(Example Example.cpp)

  target_link_libraries(Example
    Magnum::Application
    Magnum::Magnum
    Magnum::Shaders
    Magnum::MeshTools
    Magnum::Primitives
    ${PROJECT_NAME}
    SDL2::SDL2
    imgui
    )
endif()
