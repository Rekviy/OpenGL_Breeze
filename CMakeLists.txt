cmake_minimum_required(VERSION 3.13)

# check c/c++ standard
set(CMAKE_C_STANDARD 99)
set(CMAKE_C_STANDARD_REQUIRED ON)

set(CMAKE_CXX_STANDARD 17)
set(CMAKE_CXX_STANDARD_REQUIRED ON)

if (POLICY CMP0141)
  cmake_policy(SET CMP0141 NEW)
  set(CMAKE_MSVC_DEBUG_INFORMATION_FORMAT "$<IF:$<AND:$<C_COMPILER_ID:MSVC>,$<CXX_COMPILER_ID:MSVC>>,$<$<CONFIG:Debug,RelWithDebInfo>:EditAndContinue>,$<$<CONFIG:Debug,RelWithDebInfo>:ProgramDatabase>>")
endif()

project(Breeze)

set(GAME_HEADER

)
set(GAME_SRC
    src/main.cpp
)

list(APPEND GAME_SRC ${GAME_HEADER})

add_executable(Breeze ${GAME_SRC})

add_subdirectory(external ${PROJECT_BINARY_DIR}/external)

target_compile_definitions(Breeze PRIVATE
    "$<$<CONFIG:Debug>:DEBUG>"
)

set_target_properties(Breeze PROPERTIES
                    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
                    FOLDER "Internal"
                    )
