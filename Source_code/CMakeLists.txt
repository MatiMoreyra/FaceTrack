cmake_minimum_required(VERSION 3.1.0)

project(HelloTests)

# TODO: fix warnings and remove -fpermissive.
set(CMAKE_CXX_FLAGS "-fpermissive -g")

# Output binaries to a bin directory
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Qt5
find_package(
    Qt5
    COMPONENTS
        Charts
        Core
        Gui
        Widgets
    REQUIRED
)

# OpenCV
find_package(OpenCV REQUIRED)

# ALGLIB
find_package(ALGLIB REQUIRED)

include_directories(
    ${OpenCV_INCLUDE_DIRS}
    ${ALGLIB_INCLUDE_DIRS}
    ${Qt5Core_INCLUDE_DIRS}
    ${CMAKE_CURRENT_SOURCE_DIR}
)

add_executable(FaceTrack
    main.cpp
)

target_link_libraries(FaceTrack
    Qt5::Charts
    Qt5::Core
    Qt5::Gui
    Qt5::Widgets
    ${OpenCV_LIBS}
    ${ALGLIB_LIB}
)

# Set AUTO* tools.
set(CMAKE_AUTOMOC ON)
set(CMAKE_AUTOUIC ON)
set(CMAKE_AUTORCC ON)

# robo-scope-library
set_target_properties(
    FaceTrack
    PROPERTIES
        AUTOMOC
        ON # for moc_
        AUTOUIC
        ON # for ui_
        AUTORCC
        ON # for resource files like resources.qrc
)

target_sources(
    FaceTrack
    PRIVATE
        MatToQImage.cpp
        facialmesh.cpp
        facetracking.cpp
        logfile.cpp
        main.cpp
        mainwindow.cpp
        keyframeselection.cpp
        modelfitting.cpp
        onlymesh.cpp
        results.cpp
        trackingvideo.cpp
        PointState.cpp
        resources/resources.qrc
)
