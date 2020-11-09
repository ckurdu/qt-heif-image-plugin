cmake_minimum_required(VERSION 3.14)  # lowest version tried

project(HeifPlugin LANGUAGES CXX)


set(CMAKE_INCLUDE_CURRENT_DIR ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

find_package(QT NAMES Qt6 Qt5 COMPONENTS Gui REQUIRED)
find_package(Qt${QT_VERSION_MAJOR} COMPONENTS Gui REQUIRED)
find_package(libheif CONFIG REQUIRED)

set(sources main.cpp qheifhandler.cpp heif.json)

add_library(qheif SHARED ${sources})

target_link_libraries(qheif PRIVATE Qt${QT_VERSION_MAJOR}::Gui heif ${libheif_LIBRARIES} )
target_compile_definitions(qheif PRIVATE HEIFPLUGIN_LIBRARY)
