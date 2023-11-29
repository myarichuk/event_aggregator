cmake_minimum_required(VERSION 3.21)

add_executable(runUnitTests event_aggregator_tests.cpp)

find_package(Catch2 REQUIRED)

# Link against the Catch2 testing library AND the parent project
target_link_libraries(runUnitTests PRIVATE Catch2::Catch2WithMain library)

include(CTest)
include(Catch)
catch_discover_tests(runUnitTests)
