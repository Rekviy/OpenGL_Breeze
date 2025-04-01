project(Breeze)

set(HEADERS 

)
set(SRCS 
)
list(APPEND OT_SRC ${OT_HEADER})

add_subdirectory(external ${PROJECT_BINARY_DIR}/external)
target_include_directories(Breeze PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/op)

target_compile_definitions(Breeze PRIVATE
    "$<$<CONFIG:Debug>:OT_DEBUG>"
)

set_target_properties(Breeze PROPERTIES
                    RUNTIME_OUTPUT_DIRECTORY "${CMAKE_BINARY_DIR}/bin"
                    FOLDER "Internal"
                    )


if(${CMAKE_VERSION} VERSION_GREATER "3.16.0")
    message("CMake 3.16 target_precompile_headers")
    target_precompile_headers(overtime PRIVATE src/pch.h)
endif()
