cmake_minimum_required(VERSION 3.21)
project(tests)

message("Start making project: " ${PROJECT_NAME})

message(" - Defining basic variables...")
set(CMAKE_CXX_STANDARD 23)

message(" - Setting up make directories...")
set(CMAKE_BINARY_DIR ${CMAKE_SOURCE_DIR}/bin/${CMAKE_BUILD_TYPE}/${PROJECT_NAME}/)
set(EXECUTABLE_OUTPUT_PATH ${CMAKE_BINARY_DIR}/)
set(LIBRARY_OUTPUT_PATH ${CMAKE_BINARY_DIR}/)

##########################
# INCLUDING CATCH2 TESTS #
##########################

message(" - Scanning for test files...")
file(GLOB_RECURSE TESTS ${CMAKE_SOURCE_DIR}/${PROJECT_NAME}/src/*.test.cpp)

include_directories(${CMAKE_SOURCE_DIR}/${PROJECT_NAME}/src/)

message(" - Creating test executable...")
add_executable(${PROJECT_NAME} ${TESTS})

# Including external libraries
target_include_directories(${PROJECT_NAME} PUBLIC ../ntl/src/)

# Adding Catch2
target_link_libraries(${PROJECT_NAME} ntl Catch2::Catch2WithMain)

message("End making project: " ${PROJECT_NAME})