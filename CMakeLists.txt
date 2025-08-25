# =====================================
# Preamble
# =====================================

cmake_minimum_required( VERSION 4.0 )

project( ImGui-CMake 
   VERSION     1.0.0
   DESCRIPTION "Restructuring of Dear ImGui source file for use with CMake"
   LANGUAGES   CXX
)

# =====================================
# Project Wide Setup
# =====================================

set( CMAKE_CXX_STANDARD 23 )
set( CMAKE_CXX_STANDARD_REQUIRED YES )
set( CMAKE_CXX_EXTENSIONS NO )


# =====================================
# Main Targets Built By This Project
# =====================================

add_subdirectory( src )