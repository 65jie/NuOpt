cmake_minimum_required (VERSION 3.8)

set(TARGET_NAME SampleTest)

file(GLOB C_SRC1_FILES "*.cpp")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/include)

set(EXECUTABLE_OUTPUT_PATH ${CMAKE_CURRENT_SOURCE_DIR}/../bin)

link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../bin)
if(WIN32)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/win)
elseif(APPLE)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/mac)
elseif(UNIX)
link_directories(${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/linux)
endif(WIN32)

add_executable (${TARGET_NAME} ${C_SRC1_FILES} )

set(SAMPLE_LIB optimized SampleLib debug SampleLib_d)
target_link_libraries(${TARGET_NAME} gtest gtest_main ${SAMPLE_LIB})
set_target_properties(${TARGET_NAME} PROPERTIES DEBUG_POSTFIX ${CMAKE_DEBUG_POSTFIX})

# copy files after building
if(WIN32)
    add_custom_command(TARGET ${TARGET_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    #gtest
    ${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/win/gtest.dll
    ${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/win/gtest_main.dll
    #dest
    $<TARGET_FILE_DIR:${TARGET_NAME}>)
elseif(APPLE)
add_custom_command(TARGET ${TARGET_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    #gtest
    ${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/mac/libgtest.dylib
    ${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/mac/libgtest_main.dylib
    #dest
    $<TARGET_FILE_DIR:${TARGET_NAME}>)
elseif(UNIX)
add_custom_command(TARGET ${TARGET_NAME} POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy_if_different
    #gtest
    ${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/linux/libgtest.so
    ${CMAKE_CURRENT_SOURCE_DIR}/../3rd-party/gtest/lib/linux/libgtest_main.so
    $<TARGET_FILE_DIR:${TARGET_NAME}>)
endif(WIN32)