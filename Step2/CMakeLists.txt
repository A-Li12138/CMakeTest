cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(Tutorial VERSION 3.0)

# 设置c++版本
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

option(USE_MY_MATH "自己的数学库" ON)

if (USE_MY_MATH)
    # 包含二级目录
    add_subdirectory(MathFunctions)
    list(APPEND EXTRA_LIBS MathFunctions)
    list(APPEND EXTRA_INCLUDES ${CMAKE_SOURCE_DIR}/MathFunctions)
endif()


# 添加执行文件
add_executable(Tutorial tutorial.cxx)

#
configure_file(TutorialConfig.h.in TutorialConfig.h)
if(MSVC)
    target_compile_options(
        Tutorial PUBLIC 
        "/Zc:__cplusplus"
        )
endif()


# 连接静态库
target_link_libraries(
    Tutorial PUBLIC 
    ${EXTRA_LIBS}
)

# 将文件添加到生成树中
target_include_directories(
    Tutorial PUBLIC 
    ${PROJECT_BINARY_DIR}
    ${EXTRA_INCLUDES}
    )
 