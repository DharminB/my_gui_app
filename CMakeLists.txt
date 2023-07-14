cmake_minimum_required(VERSION 3.10)
project(my_gui_app)

add_compile_options(-std=c++11 -Wall)

set(IMGUI_DIR ../imgui)

include_directories(
    include
    ${IMGUI_DIR}/backends
    ${IMGUI_DIR}
)

add_library(imgui
    STATIC
        ${IMGUI_DIR}/imgui.cpp
        ${IMGUI_DIR}/imgui_demo.cpp
        ${IMGUI_DIR}/imgui_draw.cpp
        ${IMGUI_DIR}/imgui_tables.cpp
        ${IMGUI_DIR}/imgui_widgets.cpp
        ${IMGUI_DIR}/backends/imgui_impl_glfw.cpp
        ${IMGUI_DIR}/backends/imgui_impl_opengl3.cpp
)

find_package(glfw3 REQUIRED)
include_directories(${GLFW_INCLUDE_DIRS})
link_libraries(${GLFW_LIBRARY_DIRS})

# opengl
set(OpenGL_GL_PREFERENCE "LEGACY")
find_package(OpenGL REQUIRED)
include_directories(${OPENGL_INCLUDE_DIRS})

add_executable(my_gui_app
    src/main.cpp
    src/App.cpp
)
target_link_libraries(my_gui_app
    imgui
    glfw
    ${OPENGL_LIBRARIES}
    ${CMAKE_DL_LIBS}
)
