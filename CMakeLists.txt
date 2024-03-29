cmake_minimum_required(VERSION 3.13 FATAL_ERROR)

if(NOT TARGET score_lib_base)
  include("${SCORE_SOURCE_DIR}/cmake/ScoreExternalAddon.cmake")
endif()

project(score_addon_my_process LANGUAGES CXX)

# General initialization
score_common_setup()

# Creation of the library
add_library(score_addon_my_process
    MyProcess/Executor.hpp
    MyProcess/Metadata.hpp
    MyProcess/Presenter.hpp
    MyProcess/Process.hpp
    MyProcess/View.hpp
    MyProcess/Layer.hpp
    MyProcess/CommandFactory.hpp

    score_addon_my_process.hpp

    MyProcess/Executor.cpp
    MyProcess/Presenter.cpp
    MyProcess/Process.cpp
    MyProcess/View.cpp
    MyProcess/CommandFactory.cpp

    score_addon_my_process.cpp
)

# Scan for commands which creates necessary files
# Second argument must be a CMake list of all headers containing commands 

score_generate_command_list_file(
  score_addon_my_process
  "MyProcess/CommandFactory.hpp" 
)

# Link
target_link_libraries(score_addon_my_process PUBLIC score_plugin_engine)

# Target-specific options
setup_score_plugin(score_addon_my_process)
