set (mblktree_sources
  main-mbtree.C)

set (mblktree_depends_on
    SAMRAI_hier
    SAMRAI_geom
    SAMRAI_mesh
    SAMRAI_tbox)

blt_add_executable(
  NAME mblktree
  SOURCES ${mblktree_sources}
  DEPENDS_ON
    ${mblktree_depends_on})

target_compile_definitions(mblktree PUBLIC TESTING=1)

file (GLOB test_inputs ${CMAKE_CURRENT_SOURCE_DIR}/test_inputs/*.input)
file (GLOB test_baselines ${CMAKE_CURRENT_SOURCE_DIR}/test_inputs/*baseline*)

execute_process(COMMAND mkdir -p ${CMAKE_CURRENT_BINARY_DIR}/test_inputs)
execute_process(COMMAND ln -s ${test_baselines} ${CMAKE_CURRENT_BINARY_DIR}/test_inputs)

samrai_add_tests(
  NAME mblktree
  EXECUTABLE mblktree
  INPUTS ${test_inputs}
  PARALLEL FALSE)
