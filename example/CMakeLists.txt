#=============================
# Define Targets
#=============================

add_executable( SDL3_Backend_Example )

target_sources( SDL3_Backend_Example
   PRIVATE
      main.cpp
)

target_link_libraries( SDL3_Backend_Example
   PRIVATE
      SDL3::SDL3
      ImGui::ImGui
)