cmake_minimum_required(VERSION 3.25)
project(engine)

set(CMAKE_CXX_STANDARD 20)
# Ack use of experimental features
set(CMAKE_EXPERIMENTAL_CXX_MODULE_CMAKE_API "3c375311-a3c9-4396-a187-3227ef642046")

# Experimental Module support
set(CMAKE_EXPERIMENTAL_CXX_MODULE_DYNDEP 1)

find_package(Catch2 3 REQUIRED)
add_executable(tests tests/test.cpp tests/test_json.cpp)
target_link_libraries(tests PRIVATE Catch2::Catch2WithMain)

add_executable(engine main.cpp modules/print.ixx)



add_library(modules)
target_sources(modules
        PUBLIC
            FILE_SET all_my_modules TYPE CXX_MODULES
        BASE_DIRS ${PROJECT_SOURCE_DIR}
        FILES
        modules/print.ixx
        modules/json.ixx
        )