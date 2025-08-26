# =====================================
# Preamble
# =====================================

cmake_minimum_required( VERSION 4.0 )

project( ImGui-CMake 
   VERSION     1.0.0
   DESCRIPTION "Restructuring of Dear ImGui source files for use with CMake"
   LANGUAGES   CXX
)

# =====================================
# Project Wide Setup
# =====================================

set( CMAKE_CXX_STANDARD 23 )
set( CMAKE_CXX_STANDARD_REQUIRED YES )
set( CMAKE_CXX_EXTENSIONS NO )


# =====================================
# Externally Provided Content
# =====================================

include( dependencies.cmake )


# =====================================
# Main Targets Built By This Project
# =====================================

add_subdirectory( src )
add_subdirectory( example )

#=============================
# Packaging
#=============================

if ( PROJECT_IS_TOP_LEVEL )



endif()


#=============================
# Packaging
#=============================


if ( PROJECT_IS_TOP_LEVEL )

   include( GNUInstallDirs )

   install(
      TARGETS
         ImGui
         SDL3_Backend_Example
      
      EXPORT   ImGui-CMake-Export

      RUNTIME  DESTINATION         ${CMAKE_INSTALL_BINDIR}          # Following options apply to runtime artifacts.
               COMPONENT           ImGui-CMake_Runtime
               
      LIBRARY  DESTINATION         ${CMAKE_INSTALL_LIBDIR}          # Following options apply to library artifacts.
               COMPONENT           ImGui-CMake_Runtime
               NAMELINK_COMPONENT  ImGui-CMake_Development
               
      ARCHIVE  DESTINATION         ${CMAKE_INSTALL_LIBDIR}          # Following options apply to archive artifacts.
               COMPONENT           ImGui-CMake_Development
      
      FILE_SET HEADERS                                              # Following options apply to file set HEADERS.
               COMPONENT           ImGui-CMake_Development
   )


   set( CONFIG_FILES_DEST "share/ImGui/cmake" )

   install(
      EXPORT       ImGui-CMake-Export
      FILE         ImGuiConfig.cmake
      NAMESPACE    "ImGui::"
      DESTINATION  ${CONFIG_FILES_DEST}
   )  

   include( CMakePackageConfigHelpers )

   write_basic_package_version_file( "ImGuiConfigVersion.cmake" 
      VERSION            ${PROJECT_VERSION}
      COMPATIBILITY      SameMajorVersion
      ARCH_INDEPENDENT
   )

   install(
      FILES
         "${PROJECT_BINARY_DIR}/ImGuiConfigVersion.cmake"
      DESTINATION
         "${CONFIG_FILES_DEST}"
   )

endif()