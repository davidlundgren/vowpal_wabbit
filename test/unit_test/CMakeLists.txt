add_executable(vw-unit-test.out
  main.cc options_test.cc options_boost_po_test.cc cb_explore_adf_test.cc explore_test.cc
  stable_unique_tests.cc test_common.h
)

# Add the include directories from vw target for testing
target_include_directories(vw-unit-test.out PRIVATE $<TARGET_PROPERTY:vw,INCLUDE_DIRECTORIES>)
target_link_libraries(vw-unit-test.out PRIVATE vw allreduce Boost::unit_test_framework Boost::system)

# Communicate that Boost Unit Test is being statically linked
if(STATIC_LINK_VW)
  target_compile_definitions(vw-unit-test.out PRIVATE STATIC_LINK_VW)
endif()

add_test(
  NAME vw_unit_test
  COMMAND ./vw-unit-test.out
  WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)
