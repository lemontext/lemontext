file(GLOB_RECURSE sources *.cc *.hh)


link_directories(${GTKMM_LIBRARY_DIRS})
include_directories(${GTKMM_INCLUDE_DIRS})

add_executable(lemontext ${sources})
target_compile_options(lemontext PUBLIC)

target_link_libraries(lemontext ${GTKMM_LIBRARIES})