cmake_minimum_required(VERSION 3.1)
project(MinMEA)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++14")

include_directories(
        "${PROJECT_SOURCE_DIR}/include/"
)

# Create Library
add_library(MinMEA SHARED src/minmea.c)

set(PUBLIC_HEADERS
        include/minmea/minmea.h
        include/minmea/windows.h
        include/minmea/ti-rtos.h
        )

set_target_properties(MinMEA PROPERTIES
        PREFIX "lib"
        OUTPUT_NAME "minmea"
        PUBLIC_HEADER "${PUBLIC_HEADERS}"
        )


install(TARGETS         MinMEA
        ARCHIVE         DESTINATION         "lib/static"
        LIBRARY         DESTINATION         "lib/shared"
        RUNTIME         DESTINATION         "bin"
        PUBLIC_HEADER   DESTINATION         "include/minmea"
        )

CONFIGURE_FILE(
        ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}Config.cmake.in
        ${CMAKE_CURRENT_BINARY_DIR}/${PROJECT_NAME}Config.cmake @ONLY
)

CONFIGURE_FILE(
        ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}Config.cmake.in
        ${CMAKE_INSTALL_PREFIX}/${PROJECT_NAME}Config.cmake @ONLY
)