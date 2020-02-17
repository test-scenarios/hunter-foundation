cmake_minimum_required(VERSION 3.15)

if (NOT DEFINED FOUNDATION_PROJECT)
    message(FATAL_ERROR "please define the variable FOUNDATION_PROJECT to be the path to your cmake project source directory")
endif()

if (NOT DEFINED CMAKE_TOOLCHAIN_FILE)
    message(WARNING "You should probably specify a CMAKE_TOOLCHAIN_FILE")
endif()

include(cmake/HunterGate.cmake)

HunterGate(
        URL "https://github.com/cpp-pm/hunter/archive/v0.23.248.tar.gz"
        SHA1 "a637ec52a1b82beb5f55ab4aa75fac30bcee8904"
)

project(HunterFoundation)

#
# Define the dependencies to be built from source
#
hunter_add_package(Boost COMPONENTS system thread)
hunter_add_package(OpenSSL)

#
# link to the subordinate project and build it
#
if(NOT EXISTS "${CMAKE_CURRENT_LIST_DIR}/project")
    message(STATUS "[Foundation] Setting project symlink to [${FOUNDATION_PROJECT}]")
    execute_process(COMMAND ${CMAKE_COMMAND} -E create_symlink "${FOUNDATION_PROJECT}" "${CMAKE_CURRENT_LIST_DIR}/project")
else()
    get_filename_component(real_project "${CMAKE_CURRENT_LIST_DIR}/project" REALPATH)
    message(STATUS "[Foundation] Using existing project symlink to [${FOUNDATION_PROJECT}]")
endif()
add_subdirectory("project")
