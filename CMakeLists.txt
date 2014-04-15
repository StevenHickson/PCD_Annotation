cmake_minimum_required(VERSION 2.8 FATAL_ERROR)

project(PCD_Annotation)

SET_PROPERTY(GLOBAL PROPERTY TARGET_SUPPORTS_SHARED_LIBS TRUE)

IF(WIN32 OR win64)
   SET(CMAKE_FIND_LIBRARY_SUFFIXES .lib .dll)
ELSE()
   SET(CMAKE_FIND_LIBRARY_SUFFIXES .a)
ENDIF()


find_package(PCL 1.7 REQUIRED)
find_package( OpenCV REQUIRED )

add_subdirectory(src)

include_directories(C:/opencv/build)
include_directories(${PCL_INCLUDE_DIRS})
include_directories(${PCD_Annotation_SOURCE_DIR}/include)

link_directories(${PCL_LIBRARY_DIRS})

add_definitions(${PCL_DEFINITIONS})

file(GLOB_RECURSE PCD_Annotation_HEADERS include/*.h)
file(GLOB_RECURSE PCD_Annotation_SOURCES src/*.cpp)
set (PCD_Annotation_INCLUDE_DIRS "")
foreach (_headerFile ${PCD_Annotation_HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND PCD_Annotation_INCLUDE_DIRS ${_dir})
endforeach()
list(REMOVE_DUPLICATES PCD_Annotation_INCLUDE_DIRS)

include_directories(${PCD_Annotation_INCLUDE_DIRS})

add_executable (PCD_Annotation ${PCD_Annotation_SOURCES} ${PCD_Annotation_HEADERS})
target_link_libraries (PCD_Annotation ${PCL_LIBRARIES} ${OpenCV_LIBS})