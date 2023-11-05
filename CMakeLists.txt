cmake_minimum_required(VERSION 3.14)

project(
    kneditor
    VERSION 0.1
    LANGUAGES CXX
)

list(APPEND CMAKE_MODULE_PATH ${CMAKE_BINARY_DIR})
list(APPEND CMAKE_PREFIX_PATH ${CMAKE_BINARY_DIR})

set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTORCC ON)
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

if(CMAKE_BUILD_TYPE STREQUAL "Debug")
    set(NO_CACHEGEN "NO_CACHEGEN")
endif()

include(FeatureSummary)

find_package(
    Qt6
    COMPONENTS Core SerialPort Widgets
    REQUIRED
)


set(PROJECT_SOURCES
    arrow.cpp
    diagramitem.cpp
    diagramscene.cpp
    diagramtextitem.cpp
    main.cpp
    diagramscene.qrc
    mainwindow.cpp
    settingsform.cpp
)

qt_add_executable(${PROJECT_NAME} WIN32 ${PROJECT_SOURCES})
target_link_libraries(${PROJECT_NAME} PRIVATE Qt::Core Qt::SerialPort Qt::Widgets)
target_include_directories(${PROJECT_NAME} PUBLIC $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}>)

feature_summary(WHAT ALL INCLUDE_QUIET_PACKAGES FATAL_ON_MISSING_REQUIRED_PACKAGES)
