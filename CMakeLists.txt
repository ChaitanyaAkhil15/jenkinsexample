cmake_minimum_required(VERSION 3.16)
project(jenkinsexample)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)

set(CMAKE_TOOLCHAIN_FILE ${CMAKE_SOURCE_DIR}/vcpkg/scripts/buildsystems/vcpkg.cmake)
set(Catch2_DIR ${CMAKE_SOURCE_DIR}/vcpkg/installed/x64-linux/share/catch2)

message("CMAKE_SOURCE_DIR: ${CMAKE_SOURCE_DIR}")
message("CMAKE_TOOLCHAIN_FILE: ${CMAKE_TOOLCHAIN_FILE}")

set(CMAKE_CXX_STANDARD 11)

add_executable(jenkinsexample main.cpp helloWorld.cpp helloWorld.h)

find_package(Qt5 COMPONENTS Core Widgets REQUIRED)

target_compile_definitions(jenkinsexample PRIVATE $<$<OR:$<CONFIG:Debug>,$<CONFIG:RelWithDebInfo>>:QT_QML_DEBUG>)
target_link_libraries(jenkinsexample PRIVATE Qt5::Core Qt5::Widgets)

include(CTest)
add_subdirectory(test)

