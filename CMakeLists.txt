cmake_minimum_required(VERSION 3.0.0)
project(lemontext VERSION 0.1.0)

find_package(PkgConfig)

pkg_check_modules(GTKMM gtkmm-3.0)

######################
# TARGET DEFINITIONS #
######################
add_subdirectory(src)

if(CMAKE_COMPILER_IS_GNUCXX)
    message(STATUS "GCC detected, adding compile flags")
    set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++17 -Wall -Wextra")
endif(CMAKE_COMPILER_IS_GNUCXX)

#############
# PACKAGING #
#############
install(TARGETS lemontext DESTINATION lemontext_destination)

install(DIRECTORY resources DESTINATION lemontext_destination)

set(CPACK_PROJECT_NAME ${PROJECT_NAME})
set(CPACK_PROJECT_VERSION ${PROJECT_VERSION})

set(CPACK_MONOLITHIC_INSTALL 1)

include(CPack)