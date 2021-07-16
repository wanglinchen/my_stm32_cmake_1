# 获取当前目录名
# remove last end of "/"
string(REGEX REPLACE "/$" "" CURRENT_FOLDER_ABSOLUTE ${CMAKE_CURRENT_SOURCE_DIR})
get_filename_component(CURRENT_FOLDER ${CURRENT_FOLDER_ABSOLUTE} NAME)
message(STATUS "enter folder:${CURRENT_FOLDER}")

#获取当前目录的所有源文件
file(GLOB CURRENT_DIR_FILES RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} "${CMAKE_CURRENT_SOURCE_DIR}/*")

#指定可执行文件
foreach(FILE ${CURRENT_DIR_FILES})
    if(FILE MATCHES "main*")
        add_executable(${TARGET_ELF} ${CURRENT_DIR_FILES})
        set(EXECUTABLE_OUTPUT_PATH ${PROJECT_BINARY_DIR}/bin)
    else(FILE)
        message(STATUS "please create main.c or man.cpp in ${CURRENT_FOLDER}")
    endif(FILE)
endforeach(FILE)

#验证链接是否有效
set(STD_LIB "-lc -lm -lnosys")

#把其他的库文件链接到执行文件
#target_link_libraries(${TARGET_ELF} PUBLIC rtos application business modular hardware ${STD_LIB})
#file(GLOB LIB_NAMES )
#指定目标文件搜索的头文件目录
target_include_directories(${TARGET_ELF} PRIVATE 
${PROJECT_SOURCE_DIR}/application
${PROJECT_SOURCE_DIR}/rtos
)