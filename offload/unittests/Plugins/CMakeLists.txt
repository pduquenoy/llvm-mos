set(PLUGINS_TEST_COMMON omptarget)
set(PLUGINS_TEST_SOURCES NextgenPluginsTest.cpp)
set(PLUGINS_TEST_INCLUDE ${LIBOMPTARGET_INCLUDE_DIR})

foreach(PLUGIN IN LISTS LIBOMPTARGET_TESTED_PLUGINS)
  message(STATUS "Building plugin unit tests for ${PLUGIN}")
  add_libompt_unittest("${PLUGIN}.unittests" ${PLUGINS_TEST_SOURCES})
  add_dependencies("${PLUGIN}.unittests" ${PLUGINS_TEST_COMMON} ${PLUGIN})
  target_link_libraries("${PLUGIN}.unittests" PRIVATE ${PLUGINS_TEST_COMMON} ${PLUGIN})
  target_include_directories("${PLUGIN}.unittests" PRIVATE ${PLUGINS_TEST_INCLUDE})
endforeach()
