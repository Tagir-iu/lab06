cmake_minimum_required(VERSION 3.10)
project(lab06)

option(BUILD_TESTS "Build tests" OFF)

# 1. Подключаем абсолютно все подпапки твоего репозитория
add_subdirectory(banking)
add_subdirectory(formatter_lib)
add_subdirectory(formatter_ex)
add_subdirectory(hello_world)
add_subdirectory(solver_lib)
add_subdirectory(solver)

# 2. Настройка тестов (исправлены дефисы в путях third-party)
if(BUILD_TESTS)
    enable_testing()
    add_subdirectory(third-party/gtest)
    add_executable(check tests/test_account.cpp tests/test_transaction.cpp)
    target_link_libraries(check banking gtest gtest_main pthread)
    target_include_directories(check PRIVATE banking third-party/googletest/include)
    add_test(NAME check COMMAND check)
endif()

# 3. КРИТИЧЕСКИ ВАЖНО ДЛЯ HOMEWORK: 
# Говорим CMake, какие именно исполняемые файлы нужно упаковать в пакеты!
install(TARGETS solver hello_world formatter_ex RUNTIME DESTINATION bin)

# 4. Подключаем конфигурацию CPack в самом конце
include(CPackConfig.cmake)
