find_package(GTest)

if(GTEST_FOUND)
    file(GLOB_RECURSE sources_test *.cc *.hh)
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