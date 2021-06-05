

cmake_minimum_required(VERSION 3.10)

# set project name
project(chessEngine)
cmake_policy(SET CMP0072 NEW)

# packages
find_package(OpenGL REQUIRED)
find_package(GLEW REQUIRED)
find_package(PkgConfig REQUIRED)
pkg_search_module(GLFW REQUIRED glfw3)

# add_library("glad" "lib/glad/src/glad.c")

add_library(imgui STATIC
        lib/imgui/imconfig.h
        lib/imgui/imgui_demo.cpp
        lib/imgui/imgui_draw.cpp
        lib/imgui/backends/imgui_impl_glfw.h
        lib/imgui/backends/imgui_impl_glfw.cpp
        lib/imgui/backends/imgui_impl_opengl3.h
        lib/imgui/backends/imgui_impl_opengl3.cpp
        lib/imgui/imgui_internal.h
        lib/imgui/imgui_widgets.cpp
        lib/imgui/imgui.cpp
        lib/imgui/imgui.h
        lib/imgui/imstb_rectpack.h
        lib/imgui/imgui_tables.cpp
        lib/imgui/imstb_textedit.h
        lib/imgui/imstb_truetype.h
)

target_include_directories(imgui PUBLIC ${GLFW_INCLUDE_DIRS})
target_include_directories(imgui PUBLIC "lib/imgui")
target_include_directories(imgui PUBLIC "lib/imgui/backends")
target_include_directories(imgui PUBLIC "lib/glad/include")

# add the executable
add_executable(
        chessEngine
        main.cpp
        src/functions.cpp
        lib/glad/src/glad.c
)


target_include_directories(chessEngine PUBLIC ${OPENGL_INCLUDE_DIRS})
target_include_directories(chessEngine PUBLIC ${GLFW_INCLUDE_DIRS})
target_include_directories(chessEngine PUBLIC ${GLEW_INCLUDE_DIRS})
target_include_directories(chessEngine PUBLIC "include")
target_include_directories(chessEngine PUBLIC "lib/glad/include")
target_include_directories(chessEngine PUBLIC "lib/imgui")
target_include_directories(chessEngine PUBLIC "lib/imgui/backends")

target_link_libraries(chessEngine PUBLIC imgui)
target_link_libraries(chessEngine PUBLIC ${OPENGL_LIBRARIES})
target_link_libraries(chessEngine PUBLIC ${GLFW_LIBRARIES})
target_link_libraries(chessEngine PUBLIC ${GLEW_LIBRARIES})
target_link_libraries(chessEngine PUBLIC ${CMAKE_DL_LIBS})
