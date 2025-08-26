#=============================
# Define Targets
#=============================

add_library( ImGui )
add_library( ImGui::ImGui ALIAS ImGui )

set ( ImGui_Public_Headers
   ${CMAKE_CURRENT_SOURCE_DIR}/include/ImGui/imgui.h
   ${CMAKE_CURRENT_SOURCE_DIR}/include/ImGui/imconfig.h
   ${CMAKE_CURRENT_SOURCE_DIR}/include/ImGui/imgui_stdlib.h
   ${CMAKE_CURRENT_SOURCE_DIR}/include/ImGui/imgui_impl_sdl3.h
   ${CMAKE_CURRENT_SOURCE_DIR}/include/ImGui/imgui_impl_sdlrenderer3.h
)

target_sources( ImGui 
   PUBLIC
      FILE_SET     HEADERS
      BASE_DIRS    include
      FILES        ${ImGui_Public_Headers}
   
   PRIVATE
      src/imgui_demo.cpp
      src/imgui_draw.cpp
      src/imgui_impl_sdl3.cpp
      src/imgui_impl_sdlrenderer3.cpp
      src/imgui_internal.h
      src/imgui_stdlib.cpp
      src/imgui_tables.cpp
      src/imgui_widgets.cpp
      src/imgui.cpp
      src/imstb_rectpack.h
      src/imstb_textedit.h
      src/imstb_truetype.h
)


target_include_directories( ImGui
   PUBLIC 
      "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include>"
      "$<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}>"
   PRIVATE
      "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/ImGui>"
      "$<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/src>"
)


#=============================
# Packaging
#=============================


if ( PROJECT_IS_TOP_LEVEL )

   include( GNUInstallDirs )

   install(
      TARGETS   ImGui
      EXPORT    ImGui-Export

      FILE_SET  HEADERS
                DESTINATION   ${CMAKE_INSTALL_INCLUDEDIR}
      
      INCLUDES  DESTINATION   ${CMAKE_INSTALL_INCLUDEDIR}
   )

   set( CONFIG_FILES_DEST "share/ImGui/cmake" )

   install(
      EXPORT       ImGui-Export
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