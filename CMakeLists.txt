cmake_minimum_required(VERSION 2.8)

set(PROJECT_NAME Automata)
project(${PROJECT_NAME})

set(CMAKE_CXX_FLAGS "-g -Wall")
@@ -15,26 +15,26 @@ set(CMAKE_CXX_FLAGS "-g -Wall")
#----------------------------------------------------------------------------
set(COMMON_INCLUDES ${PROJECT_SOURCE_DIR}/include)
include_directories(${COMMON_INCLUDES})
set(TEST_SRC_FILES1 ${PROJECT_SOURCE_DIR})
file(GLOB TEST_SRC_FILES ${PROJECT_SOURCE_DIR}/test/*.cpp)
add_subdirectory(ext/gtest-1.8.0)
include_directories(ext/gtest-1.8.0/googletest/include)

set(SRC_FILES ${PROJECT_SOURCE_DIR}
        include/Automata.h
        src/AutomataOptions.cpp
        )
set(CMAKE_CXX_STANDARD 11)
add_executable(automata_run src/main.cpp ${SRC_FILES})
add_executable(tests_run test/tests.cpp ${TEST_SRC_FILES1} ${SRC_FILES})

target_link_libraries(tests_run gtest gtest_main)
################################
# Testing
@@ -45,7 +45,6 @@ option(BUILD_TESTS "Build all tests." OFF) # Makes boolean 'test' available.

if (BUILD_TESTS)
  # This adds another subdirectory, which has 'project(gtest)'.
  enable_testing()
  @@ -56,11 +55,12 @@ if (BUILD_TESTS)
  ##############
  # Unit Tests
  ##############
    add_executable(runUnitTests ${TEST_SRC_FILES} ${SRC_FILES})

  # Standard linking to gtest stuff.
  target_link_libraries(runUnitTests gtest gtest_main)


  # Extra linking for the project.
  #target_link_libraries(runUnitTests task1_lib task2_lib task3_lib)

add_test(UnitTests runUnitTests)
  set(CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/.travis/cmake)
  if (CMAKE_BUILD_TYPE STREQUAL "Coverage")
    include(CodeCoverage)
    setup_target_for_coverage(${PROJECT_NAME}_coverage runUnitTests coverage)
    SET(CMAKE_CXX_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
    SET(CMAKE_C_FLAGS "-g -O0 -fprofile-arcs -ftest-coverage")
  endif() #CMAKE_BUILD_TYPE STREQUAL "Coverage"
endif()