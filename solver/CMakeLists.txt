cmake_minimum_required(VERSION 3.10)
project(solver)

add_executable(solver main.cpp)

# Добавляем пути к инклудам библиотек, чтобы компилятор видел их хедеры
target_include_directories(solver PRIVATE 
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_lib
    ${CMAKE_CURRENT_SOURCE_DIR}/../formatter_ex
    ${CMAKE_CURRENT_SOURCE_DIR}/../solver_lib
)

target_link_libraries(solver PRIVATE solver_lib formatter_ex formatter)
