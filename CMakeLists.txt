cmake_minimum_required(VERSION 3.26)
project(wimic VERSION 0.0.1 LANGUAGES C CXX)

if(CMAKE_SYSTEM_NAME STREQUAL "Linux")
  set(LINUX true)
endif()

set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(
    WIMIC_SOURCES

    # imgui
    src/imgui/imgui.cpp
    src/imgui/imgui_tables.cpp
    src/imgui/imgui_draw.cpp
    src/imgui/imgui_widgets.cpp
    src/imgui/imgui_widgets.cpp
    src/imgui/backends/imgui_impl_glfw.cpp
    src/imgui/backends/imgui_impl_opengl3.cpp

    # wimic
    src/main.cpp
)

add_executable( ${PROJECT_NAME} ${WIMIC_SOURCES})

target_compile_features(${PROJECT_NAME} PRIVATE cxx_std_20)

if(WIN32)
    target_link_libraries(
        ${PROJECT_NAME} PRIVATE
        ${CMAKE_SOURCE_DIR}/lib/glfw/windows/libglfw3.a
    )
endif()

target_include_directories(
    ${PROJECT_NAME} PRIVATE
    ${CMAKE_SOURCE_DIR}/include
    ${CMAKE_SOURCE_DIR}/src
    ${CMAKE_SOURCE_DIR}/src/imgui
)

# Install

install(
    TARGETS ${PROJECT_NAME}
    RUNTIME DESTINATION .
    LIBRARY DESTINATION .
    ARCHIVE DESTINATION lib
)