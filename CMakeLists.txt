cmake_minimum_required(VERSION 2.8)
project( OCVE )

set(LIB_NAME egbis)
set(SRC_DIR ${PROJECT_SOURCE_DIR}/egbis)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${PROJECT_SOURCE_DIR}/bin)

option(BUILD_DEMO OFF)

find_package( OpenCV REQUIRED )

# Add the EGBIS algortihm
FILE(GLOB_RECURSE EGBIS_SRC ${SRC_DIR}/src/*.cpp)
include_directories(${SRC_DIR}/include)

add_library(${LIB_NAME} STATIC ${EGBIS_SRC})

# Install rules
install(TARGETS ${LIB_NAME} egbis
    DESTINATION lib)
install(DIRECTORY ${SRC_DIR}/include
    DESTINATION include)

if (BUILD_DEMO)
    add_executable( main demo/main.cpp ${EGBIS_SRC})
    target_link_libraries( main ${OpenCV_LIBS} )
endif (BUILD_DEMO)
