cmake_minimum_required(VERSION 3.14)
project(GiNaCBuild LANGUAGES CXX)

set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build shared libs" FORCE)

add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/GiNaC)

# Wrapper library
add_library(GiNaCBuild INTERFACE)
target_link_libraries(GiNaCBuild INTERFACE ginac)

# Include copy folder
set(GINAC_WRAPPER_INCLUDE_DIR ${CMAKE_CURRENT_BINARY_DIR}/include)

# Make sure build/include exists
file(MAKE_DIRECTORY ${GINAC_WRAPPER_INCLUDE_DIR})

# Copy headers using custom target so it runs before consumers build
add_custom_target(copy_ginac_headers ALL
    COMMAND ${CMAKE_COMMAND} -E copy_directory
            ${CMAKE_CURRENT_LIST_DIR}/GiNaC/ginac
            ${GINAC_WRAPPER_INCLUDE_DIR}/ginac
    COMMENT "Copying GiNaC headers to build folder"
)

# Add include directories **after copy**
add_dependencies(GiNaCBuild copy_ginac_headers)
target_include_directories(GiNaCBuild INTERFACE
    ${GINAC_WRAPPER_INCLUDE_DIR}
)

# Alias
add_library(GiNaCBuild::ginac ALIAS GiNaCBuild)
