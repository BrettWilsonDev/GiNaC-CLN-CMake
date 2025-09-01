cmake_minimum_required(VERSION 3.14)
project(GiNaCBuild LANGUAGES CXX)

# Force static libraries
set(BUILD_SHARED_LIBS OFF CACHE BOOL "Build shared libs" FORCE)

# Add GiNaC (CLN is handled inside GiNaC's CMakeLists.txt)
add_subdirectory(${CMAKE_CURRENT_LIST_DIR}/GiNaC)
