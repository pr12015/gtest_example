cmake_minimum_required(VERSION 3.10)

project(test)

include(ExternalProject)
ExternalProject_Add(gtest
    GIT_REPOSITORY https://github.com/google/googletest/
    #SVN_REPOSITORY http://googletest.googlecode.com/svn/trunk/
    PREFIX ${CMAKE_CURRENT_BINARY_DIR}/gtest
    INSTALL_COMMAND ""
)
ExternalProject_Get_Property(gtest source_dir binary_dir)

add_executable(gtest_ex gtest_example.cpp)

add_dependencies(gtest_ex gtest)
include_directories(${source_dir}/include)
target_link_libraries(gtest_ex ${binary_dir}/googlemock/gtest/libgtest.a)

enable_testing()
add_test(NAME gtest_ex
         COMMAND gtest_ex)

