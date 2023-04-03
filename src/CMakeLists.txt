cmake_minimum_required (VERSION 3.8)

set(TARGET_NAME SampleLib)

file(GLOB C_SRC1_FILES "*.cpp")

set(VERSION_RC "${CMAKE_CURRENT_SOURCE_DIR}/Resources.rc")
configure_file(
  ${CMAKE_CURRENT_SOURCE_DIR}/Resources.rc.in
  ${CMAKE_CURRENT_SOURCE_DIR}/Resources.rc
  @ONLY)

set(LIBRARY_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../bin)
add_library(${TARGET_NAME} SHARED ${C_SRC1_FILES} ${VERSION_RC})

set_target_properties(${TARGET_NAME} PROPERTIES DEBUG_POSTFIX ${CMAKE_DEBUG_POSTFIX})
set_target_properties(${TARGET_NAME} PROPERTIES VERSION "${PROJECT_VERSION_MAJOR}.${PROJECT_VERSION_MINOR}.${PROJECT_VERSION_PATCH}")
set_target_properties(${TARGET_NAME} PROPERTIES CLEAN_DIRECT_OUTPUT 1)

enable_testing()
add_test(SampleTest ${PROJECT_BINARY_DIR}/SampleTest)
