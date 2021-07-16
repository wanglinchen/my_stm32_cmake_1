# remove last end of "/"
string(REGEX REPLACE "/$" "" CURRENT_FOLDER_ABSOLUTE ${CMAKE_CURRENT_SOURCE_DIR})
# 获取当前目录名
get_filename_component(CURRENT_FOLDER ${CURRENT_FOLDER_ABSOLUTE} NAME)
message(STATUS "enter folder:${CURRENT_FOLDER}")

set(CURRENT_MOD_NAME ${CURRENT_FOLDER})

add_subdirectory(freertos)

