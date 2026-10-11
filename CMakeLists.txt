cmake_minimum_required(VERSION 3.15)

project(Macro VERSION 1.0 LANGUAGES CXX)

if(NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/submodules/configuration/cmake/ProjectOptions.cmake")
    message(FATAL_ERROR
        "Git submodules are not initialized. "
        "Run 'git submodule update --init --recursive' before configuring the project.")
endif()

include("${CMAKE_CURRENT_SOURCE_DIR}/submodules/configuration/cmake/ProjectOptions.cmake")

require_initialized_submodules()

if(NOT TARGET macro)
    add_library(macro INTERFACE)
    target_compile_features(macro INTERFACE cxx_std_20)
    target_include_directories(macro INTERFACE
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include/ariadne-macro>
    )
endif()

ariadne_register_public_headers(
    TARGET macro
    DIRECTORIES "${PROJECT_SOURCE_DIR}/include/macro"
)

if(CMAKE_SOURCE_DIR STREQUAL PROJECT_SOURCE_DIR)
    ariadne_install_dependency_bundle(
        TARGET macro
        DESTINATION include/ariadne-macro
    )
endif()
