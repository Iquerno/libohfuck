# libOHFUCK
# (public domain)
# to learn how to embed this project, refer to " README.md " in the root folder

# the only reason this file works is because of some
# CMAKE NAMESPACE wizardry that I do not understand

cmake_minimum_required(VERSION 3.4 FATAL_ERROR)
project(libohfuck LANGUAGES C VERSION 1.0.0 DESCRIPTION "convenience library for the OHFUCK project")
set(CMAKE_C_STANDARD 99)

# if debug!!!
if (MSVC)
    add_compile_options(/W4 /Wall)
elseif (GNU)
    add_compile_options(-Wpedantic -W -Wall -Wextra)
elseif (CLANG)
    add_compile_options(-Wpedantic -W -Wall -Wextra)
endif ()

if (WIN32)
    set(CMAKE_SUPPORT_WINDOWS_EXPORT_ALL_SYMBOLS 1)
endif ()

add_library(libohfuck) # shared/static library choice is determined by BUILD_SHARED_LIBS
target_sources(libohfuck PRIVATE
        src/ohfuck.c
        )
target_include_directories(libohfuck
        PRIVATE
            src # for internal library stuff
        PUBLIC
            $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include> # for top level projects
            $<INSTALL_INTERFACE:${CMAKE_INSTALL_INCLUDEDIR}> # for external projects
        ) #    #include "../include/ohfuck.h"     ->     #include <include/ohfuck.h>
set_target_properties(libohfuck PROPERTIES
        VERSION ${PROJECT_VERSION}
        PUBLIC_HEADER include/ohfuck.h
        DEBUG_POSTFIX "__DEBUG"
        )
include(GNUInstallDirs)
install(TARGETS libohfuck
        EXPORT libohfuckTargets
        PUBLIC_HEADER DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}/libohfuck
        INCLUDES DESTINATION ${CMAKE_INSTALL_INCLUDEDIR}
        )

# generate libohfuckConfig.cmake
include(CMakePackageConfigHelpers)
install(EXPORT libohfuckTargets
        FILE libohfuckTargets.cmake
        NAMESPACE libohfuck::
        DESTINATION cmake
        )
write_basic_package_version_file(
        "${CMAKE_CURRENT_BINARY_DIR}/libohfuckConfigVersion.cmake"
        VERSION "${PROJECT_VERSION}"
        COMPATIBILITY AnyNewerVersion
        )
configure_package_config_file(${CMAKE_CURRENT_SOURCE_DIR}/Config.cmake.in
        "${CMAKE_CURRENT_BINARY_DIR}/libohfuckConfig.cmake"
        INSTALL_DESTINATION cmake
        )
install(FILES
        "${CMAKE_CURRENT_BINARY_DIR}/libohfuckConfig.cmake"
        "${CMAKE_CURRENT_BINARY_DIR}/libohfuckConfigVersion.cmake"
        DESTINATION cmake
        )
export(EXPORT "libohfuckTargets"
        FILE "${CMAKE_CURRENT_BINARY_DIR}/cmake/libohfuckTargets.cmake"
        NAMESPACE libohfuck::
        )