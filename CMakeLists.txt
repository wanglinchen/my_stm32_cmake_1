#提示
message(STATUS "enter folder:${CMAKE_CURRENT_SOURCE_DIR}")

#################################################自定义函数######################################
#设置cmake版本要求
function(SET_CMAKE_VERSION CMAKE_VER)
    cmake_minimum_required (VERSION ${CMAKE_VER})
endfunction()

#设置工程名
function(SET_PROJECT_NAME PROJECT_NAME)
    # remove last end of "/"
    string(REGEX REPLACE "/$" "" CURRENT_FOLDER_ABSOLUTE ${CMAKE_CURRENT_SOURCE_DIR})
    # 获取当前目录名
    get_filename_component(CURRENT_FOLDER ${CURRENT_FOLDER_ABSOLUTE} NAME)
    set(PROJECT_NAME ${CURRENT_FOLDER})
    #设置工程名
    project (${PROJECT_NAME})
    message(STATUS "Building project: ${PROJECT_NAME}")
endfunction(SET_PROJECT_NAME)

#设置目标文件
function(SET_TARGET_NAME TARGET_NAME)
    #设置目标文件名
    set(TARGET_ELF ${TARGET_NAME}.elf)
    set(TARGET_HEX ${TARGET_NAME}.hex)
    set(TARGET_BIN ${TARGET_NAME}.bin)
    message(STATUS "TARGET_NAME:${TARGET_NAME}")
endfunction(SET_TARGET_NAME)

#设置编译类型
function(SET_BUILD_TYPE BUILD_TYPE)
    # 设置编译类型
    if(NOT BUILD_TYPE) 
    set(BUILD_TYPE debug)
    endif(NOT BUILD_TYPE)

    if(BUILD_TYPE MATCHES debug)
    message(STATUS "Build type: debug")
    elseif(BUILD_TYPE MATCHES release)
    message(STATUS "Build type: release")
    endif()
endfunction(SET_BUILD_TYPE)

#添加编译子目录
function(ADD_SUB_DIRS CUR_DIR)
    file(GLOB SUB_DIR_FILES RELATIVE ${CUR_DIR} ${CUR_DIR}/*)
    message(STATUS "SUB_DIR_FILES:${SUB_DIR_FILES}")
    set(SUB_DIR_LIST "")
    foreach(FILE ${SUB_DIR_FILES})
        if(IS_DIRECTORY ${CUR_DIR}/${FILE})
            if(EXISTS ${CUR_DIR}/${FILE}/CMakeLists.txt)
                list(APPEND SUB_DIR_LIST ${FILE})
            endif()
        endif()
    endforeach(FILE)
    message(STATUS "SUB_DIR_LIST:${SUB_DIR_LIST}")
    foreach(SUB_DIR ${SUB_DIR_LIST})
        message(STATUS "add SUB_DIR:${SUB_DIR}")
        add_subdirectory(${SUB_DIR})
    endforeach(SUB_DIR)
endfunction(ADD_SUB_DIRS)

#设置编译工具链和编译参数
function(SET_BUILD_TOOL)
    #包含工具链和编译参数以及MCU定义
    include(${PROJECT_SOURCE_DIR}/tool/cmake/compile-tool-chains.cmake)
    include(${PROJECT_SOURCE_DIR}/tool/cmake/compile-mcu-def.cmake)
    include(${PROJECT_SOURCE_DIR}/tool/cmake/compile-flags.cmake)
endfunction(SET_BUILD_TOOL)

#######################################################函数调用#################################################
SET_CMAKE_VERSION(3.0)

SET_PROJECT_NAME(hello)

message(STATUS "PROJECT_NAME: ${PROJECT_NAME}")

SET_TARGET_NAME(${PROJECT_NAME})

SET_BUILD_TYPE(debug)

SET_BUILD_TOOL()

ADD_SUB_DIRS(${CMAKE_CURRENT_SOURCE_DIR})



file(GLOB CURRENT_DIR_SRCS RELATIVE ${CMAKE_CURRENT_SOURCE_DIR} 
    ${CMAKE_CURRENT_SOURCE_DIR}/*.c
    ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp
    ${CMAKE_CURRENT_SOURCE_DIR}/*.h
    ${CMAKE_CURRENT_SOURCE_DIR}/*.hpp
)
message(STATUS "CURRENT_DIR_SRCS:${CURRENT_DIR_SRCS}")
























