cmake_minimum_required(VERSION 3.13)

project(external)
option(BUILD_LOGGING "Build with spdlog logging" ON)
option(BUILD_IMGUI "Build with imgui" ON)
if(BUILD_LOGGING)
	add_subdirectory(spdlog)
	target_link_libraries(Breeze spdlog)
	set_target_properties(spdlog PROPERTIES FOLDER "External")
endif(BUILD_LOGGING)
if(BUILD_IMGUI)
add_subdirectory(imgui)
target_link_libraries(imgui glfw OpenGL::GL)
target_link_libraries(Breeze imgui)
set_target_properties(imgui PROPERTIES FOLDER "External")
endif(BUILD_IMGUI)

add_subdirectory(glad)
add_subdirectory(glfw)
add_subdirectory(glm)
find_package(OpenGL REQUIRED)

include_directories(${OPENGL_INCLUDE_DIRS})
target_link_libraries(Breeze glfw OpenGL::GL glad glm::glm-header-only)
set_target_properties(glm PROPERTIES FOLDER "External")
set_target_properties(glad PROPERTIES FOLDER "External")


