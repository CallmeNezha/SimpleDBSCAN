project( SimpleDBSCAN )
cmake_minimum_required( VERSION 3.5 )

set( CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11" )

set(SOURCES 
    dbscan.h
    kdtree.cpp
    kdtree.h
    main.cpp
)

add_executable(dbscan_example ${SOURCES})