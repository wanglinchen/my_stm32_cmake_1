# 获取当前目录名
# remove last end of "/"
string(REGEX REPLACE "/$" "" CURRENT_FOLDER_ABSOLUTE ${CMAKE_CURRENT_SOURCE_DIR})
get_filename_component(CURRENT_FOLDER ${CURRENT_FOLDER_ABSOLUTE} NAME)
message(STATUS "enter folder:${CURRENT_FOLDER}")

# 查找当前目录下的所有源文件,将名称保存到 CURRENT_DIR_SRCS 变量
aux_source_directory(. CURRENT_DIR_SRCS)

if("${CURRENT_DIR_SRCS}" STREQUAL "")
# 指定当前文件夹名为模块名
set(CURRENT_MOD_NAME ${CURRENT_FOLDER})
message(STATUS "CURRENT_MOD_NAME:${CURRENT_MOD_NAME}")
else()
# 指定源码编译成库文件,库名为当前文件夹的名字
set(CURRENT_LIB_NAME ${CURRENT_FOLDER})
message(STATUS "CURRENT_LIB_NAME:${CURRENT_LIB_NAME}")
add_library(${CURRENT_LIB_NAME} STATIC ${CURRENT_DIR_SRCS})
SET(LIBRARY_OUTPUT_PATH ${PROJECT_BINARY_DIR}/lib)
endif()
