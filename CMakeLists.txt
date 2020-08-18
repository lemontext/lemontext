cmake_minimum_required(VERSION 3.0.0)
project(lemontext VERSION 0.1.0)

#################
# FILE GLOBBING #
#################

file(GLOB_RECURSE sources src/main/*.cc src/main/*.hh)
file(GLOB_RECURSE sources_test src/test/*.cc)
file(GLOB_RECURSE data resources/*)

######################
# TARGET DEFINITIONS #
######################

add_executable(lemontext ${sources} ${data})

target_compile_options(lemontext PUBLIC -std=c++17 -Wall -Wfloat-conversion)

target_include_directories(lemontext PUBLIC src/main)

file(COPY ${data} DESTINATION resources)

################
# DEPENDENCIES #
################
find_package(GTest)

if(GTEST_FOUND)
    add_executable(unit_tests ${sources_test} ${sources})

    target_compile_definitions(unit_tests PUBLIC UNIT_TESTS)

    set_target_properties(lemontext PROPERTIES ENABLE_EXPORTS on)

    target_link_libraries(unit_tests PUBLIC
        ${GTEST_BOTH_LIBRARIES}
        lemontext
    )

    target_include_directories(unit_tests PUBLIC
        ${GTEST_INCLUDE_DIRS}
    )
endif()

#############
# PACKAGING #
#############
install(TARGETS lemontext DESTINATION lemontext_destination)

install(DIRECTORY resources DESTINATION lemontext_destination)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

set(CPACK_MONOLITHIC_INSTALL 1)

include(CPack)