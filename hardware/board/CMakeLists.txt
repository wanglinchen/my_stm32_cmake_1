# 获取当前目录名
# remove last end of "/"
string(REGEX REPLACE "/$" "" CURRENT_FOLDER_ABSOLUTE ${CMAKE_CURRENT_SOURCE_DIR})
get_filename_component(CURRENT_FOLDER ${CURRENT_FOLDER_ABSOLUTE} NAME)
message(STATUS "enter folder:${CURRENT_FOLDER}")

# 把当前目录名设置为库名
set(CURRENT_LIB_NAME ${CURRENT_FOLDER})

# 查找当前目录下的所有源文件,将名称保存到 CURRENT_DIR_SRCS 变量
aux_source_directory(. CURRENT_DIR_SRCS)

# 指定当前库的名字
add_library(${CURRENT_LIB_NAME} STATIC ${CURRENT_DIR_SRCS})

