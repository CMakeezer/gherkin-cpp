cmake_minimum_required(VERSION 2.8)
project(gherkin-cpp)

set(CMAKE_CXX_STANDARD 14)

find_package(gherkin REQUIRED)
find_package(fmem REQUIRED)

file(GLOB LIBRARY_SOURCES
       ${PROJECT_SOURCE_DIR}/src/*.cpp)

add_library(gherkin-cpp ${LIBRARY_SOURCES})
target_link_libraries(gherkin-cpp PUBLIC gherkin::gherkin fmem::fmem)
target_include_directories(gherkin-cpp PUBLIC
        "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>")


############ Installation section ############

install(
        TARGETS gherkin-cpp
        EXPORT gherkin-cpp-cmake
        ARCHIVE DESTINATION lib/
        LIBRARY DESTINATION lib/
        RUNTIME DESTINATION bin/
        INCLUDES DESTINATION include/gherkin-cpp)

install(
        DIRECTORY "${PROJECT_SOURCE_DIR}/include/"
        DESTINATION include/gherkin-cpp
        FILES_MATCHING PATTERN "*.*hpp")

install(
        EXPORT gherkin-cpp-cmake
        FILE gherkin-cpp-config.cmake
        NAMESPACE gherkin-cpp::
        DESTINATION share/gherkin-cpp/cmake)
