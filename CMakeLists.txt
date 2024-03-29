set(VERSION "2.8.4") # Create var "VERSION"
set(SOURCE_FILES ${CMAKE_CURRENT_SOURCE_DIR}/src/*) # Create var "SOURCE_FILES", I guess init.c is enough cus anything linked to it is compiled?

# Disable sh.exe mingw error
set(DCMAKE_SH="CMAKE_SH-NOTFOUND")

cmake_minimum_required(VERSION ${VERSION})
project(VexRobot CXX)

set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_FLAGS  "${CMAKE_CXX_FLAGS} -Wall")

file(GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c")
file(GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
file(GLOB_RECURSE HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h")
file(GLOB_RECURSE HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.hpp")

set (INCLUDE_DIRS "")
foreach (_headerFile ${HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND INCLUDE_DIRS ${_dir})
endforeach()

list(REMOVE_DUPLICATES INCLUDE_DIRS)

include_directories("${CMAKE_CURRENT_SOURCE_DIR}/include")
add_executable(VexRobot ${SOURCES} ${HEADERS} src/a.cpp src/drive.cpp include/move.h include/auton.h src/auton.cpp include/auton.h src/tilter.cpp src/tilter.h src/globals.cpp include/globals.h)

#[[
# Headers/include path
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
include_directories(${CMAKE_CURRENT_SOURCE_DIR}/src)

# my_executagle is executable build target, *.cpp are files required
#https://www.jetbrains.com/help/clion/quick-cmake-tutorial.html
#add_executable (my_executable my_source1.cpp my_source2.cpp)



# SEE: https://stackoverflow.com/questions/6921695/how-can-i-build-a-c-project-with-multiple-interdependent-subdirectories
# HELPFUL: https://mirkokiefer.com/cmake-by-example-f95eb47d45b1
file(GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.c")
file(GLOB_RECURSE SOURCES "${CMAKE_CURRENT_SOURCE_DIR}/src/*.cpp")
file(GLOB_RECURSE HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.h")
file(GLOB_RECURSE HEADERS "${CMAKE_CURRENT_SOURCE_DIR}/src/*.hpp")
# IMPORTANT ^^^^^^^^^^^^^^^^^^^ .CPP for c++ etc...

set (INCLUDE_DIRS "")
foreach (_headerFile ${HEADERS})
    get_filename_component(_dir ${_headerFile} PATH)
    list (APPEND INCLUDE_DIRS ${_dir})
endforeach()

list(REMOVE_DUPLICATES INCLUDE_DIRS)


add_executable(VexRobot ${SOURCES} ${HEADERS})
target_include_directories(VexRobot PRIVATE ${INCLUDE_DIRS})

# Tell pros to build the project
#execute_process(COMMAND pros make)
]]#