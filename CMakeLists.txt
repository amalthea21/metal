cmake_minimum_required(VERSION 3.16)
project(metal VERSION 0.1.0 LANGUAGES C ASM)

if(WIN32 OR CYGWIN OR MSYS)
    message(FATAL_ERROR
            "Platform ${CMAKE_SYSTEM_NAME} is not supported.\n"
            "This project requires a Unix-like Environment. (Linux, macOS, BSD)"
    )
endif()

            set(CMAKE_C_STANDARD 23)
set(CMAKE_C_STANDARD_REQUIRED ON)

add_compile_options(-Wall -Wextra -Wpedantic)

set(CMAKE_C_FLAGS_DEBUG "${CMAKE_C_FLAGS_DEBUG} -g")

file(GLOB_RECURSE SOURCES "src/*.c")
file(GLOB_RECURSE HEADERS "include/*.h")

message("SOURCES: ${SOURCES}")
message("HEADERS: ${HEADERS}")

add_executable(${PROJECT_NAME} ${SOURCES} ${HEADERS})

target_link_libraries(${PROJECT_NAME} PRIVATE)
target_include_directories(${PROJECT_NAME} PRIVATE
        ${CMAKE_CURRENT_SOURCE_DIR}/include
        ${CMAKE_CURRENT_SOURCE_DIR}
)