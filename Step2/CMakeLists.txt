cmake_minimum_required(VERSION 3.10)

# 设置项目名称
project(Tutorial VERSION 3.0)

# 设置c++版本
set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED True)

# 包含二级目录
add_subdirectory(MathFunctions)

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
    MathFunctions
)

# 将文件添加到生成树中
target_include_directories(
    Tutorial PUBLIC 
    ${PROJECT_BINARY_DIR}
    ${PROJECT_SOURCE_DIR}/MathFunctions
    )
