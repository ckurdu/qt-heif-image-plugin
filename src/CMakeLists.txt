cmake_minimum_required(VERSION 3.14)  # lowest version tried

project(HeifPlugin LANGUAGES CXX)

#old
#set(CMAKE_CXX_STANDARD 11)
#set(CMAKE_CXX_STANDARD_REQUIRED ON)
#set(CMAKE_CXX_EXTENSIONS OFF)

set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
# make release build, if not specified
# (from https://blog.kitware.com/cmake-and-the-default-build-type/)
# set(default_build_type "RelWithDebInfo")

#if (NOT CMAKE_BUILD_TYPE AND NOT CMAKE_CONFIGURATION_TYPES)
#  set(CMAKE_BUILD_TYPE "${default_build_type}" CACHE STRING "Build type" FORCE)
#  set_property(
#    CACHE CMAKE_BUILD_TYPE PROPERTY STRINGS
#    "Debug" "Release" "MinSizeRel" "RelWithDebInfo")
#endif ()

# compiler flags
# TODO: separate GCC and Clang warnings; add more
#set(
#  CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} \
#  -Wall \
#  -Wextra \
#  -Wshadow \
#  -Wformat-nonliteral \
#  -Wformat-security \
#  -Wnon-virtual-dtor \
#  ")

#set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} -Og")

#set(sanitizer_flags "-fsanitize=address -fsanitize=undefined")
#set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} ${sanitizer_flags}")
#set(CMAKE_MODULE_LINKER_FLAGS_DEBUG "${CMAKE_MODULE_LINKER_FLAGS_DEBUG} ${sanitizer_flags}")

#
# third-party libs
#

find_package(QT NAMES Qt6 Qt5 COMPONENTS Gui REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Gui REQUIRED)
# qt
#find_package(Qt5 COMPONENTS Core Gui REQUIRED)
#add_definitions(-DQT_NO_KEYWORDS)
#set(CMAKE_AUTOMOC ON)

# libheif
#find_package(PkgConfig)
#pkg_check_modules(libheif REQUIRED libheif>=1.1)

#
# project source
#

list(APPEND CMAKE_PREFIX_PATH "D:/uprojects/qtprojects/tests/vcpkg/packages/libheif_x64-windows/share/libheif" )
find_package(libheif CONFIG REQUIRED)

#set(CMAKE_INCLUDE_CURRENT_DIR ON)

set(sources main.cpp qheifhandler.cpp heif.json)

add_library(qheif SHARED ${sources})

target_link_libraries(qheif PRIVATE Qt${QT_VERSION_MAJOR}::Gui heif ${libheif_LIBRARIES} )
target_compile_definitions(qheif PRIVATE HEIFPLUGIN_LIBRARY)
