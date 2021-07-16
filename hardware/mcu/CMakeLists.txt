# 获取当前目录名
# remove last end of "/"
string(REGEX REPLACE "/$" "" CURRENT_FOLDER_ABSOLUTE ${CMAKE_CURRENT_SOURCE_DIR})
get_filename_component(CURRENT_FOLDER ${CURRENT_FOLDER_ABSOLUTE} NAME)
message(STATUS "enter folder:${CURRENT_FOLDER}")

# 包含的子模块
add_subdirectory(arm)
add_subdirectory(stm32)
add_subdirectory(stm32_startup)

