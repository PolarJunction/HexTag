cmake_minimum_required(VERSION 3.16 FATAL_ERROR)

# Project
project (
    myProject
    VERSION 1.0
    LANGUAGES CXX
)

# Specify the C++ standard
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_CXX_STANDARD_REQUIRED True)
set(CMAKE_EXPORT_COMPILE_COMMANDS ON)

# Add header files
include_directories(include)

# Add source files
set(SOURCES 
    source/fact.cpp)

# Add test source files
set(TEST_SOURCES
    tests/test_main.cpp)

# Add the executable
add_executable("${PROJECT_NAME}" source/main.cpp ${SOURCES})

# Enable Unit Testing
if(ENABLE_TESTING)
    enable_testing()
    find_package(Catch2 REQUIRED)
    add_executable(unit_tests ${SOURCES} ${TEST_SOURCES})
    target_link_libraries(unit_tests Catch2::Catch2)

    include(CTest)
    include(ParseAndAddCatchTests)
    ParseAndAddCatchTests(unit_tests)
endif()

