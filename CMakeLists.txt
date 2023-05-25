cmake_minimum_required(VERSION 2.8)
project(lgepp C CXX)

if(NOT CMAKE_BUILD_TYPE)
  set(CMAKE_BUILD_TYPE Debug CACHE STRING "" FORCE)
endif()

set(CMAKE_CXX_STANDARD 11)
set (CMAKE_C_FLAGS "${CMAKE_C_FLAGS}")
set (CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS}")

find_package(glfw3 CONFIG REQUIRED)

option(GLFW_BUILD_EXAMPLES "Build the GLFW example programs" OFF)
option(GLFW_BUILD_TESTS "Build the GLFW test programs" OFF)
option(GLFW_BUILD_DOCS "Build the GLFW documentation" OFF)
option(GLFW_INSTALL "Generate installation target" OFF)
option(GLFW_DOCUMENT_INTERNALS "Include internals in documentation" OFF)
include_directories(${GLFW_DIR}/include)

find_package(Vulkan REQUIRED)
set(LIBRARIES "glfw;Vulkan::Vulkan")

include_directories(${GLFW_DIR}/deps)

file(GLOB sources *.cpp)

add_executable(lgepp ${sources})
target_link_libraries(lgepp ${LIBRARIES})
target_compile_definitions(lgepp PUBLIC -DImTextureID=ImU64)
