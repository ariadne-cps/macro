cmake_minimum_required(VERSION 3.15)

project(Macro VERSION 1.0 LANGUAGES CXX)

find_package(Git REQUIRED)

if(NOT EXISTS "${CMAKE_CURRENT_SOURCE_DIR}/ss/configuration/cmake/ProjectOptions.cmake")
    execute_process(
        COMMAND "${GIT_EXECUTABLE}" -C "${CMAKE_CURRENT_SOURCE_DIR}"
                submodule update --init -- ss/configuration
        ERROR_VARIABLE _configuration_error
        RESULT_VARIABLE _configuration_result
    )
    if(NOT _configuration_result EQUAL 0)
        message(FATAL_ERROR
            "Cannot initialize configuration submodule: ${_configuration_error}")
    endif()
endif()

include("${CMAKE_CURRENT_SOURCE_DIR}/ss/configuration/cmake/ProjectOptions.cmake")

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
