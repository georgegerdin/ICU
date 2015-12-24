project(ICU)

cmake_minimum_required(VERSION 2.8.8)

file(READ "${CMAKE_SOURCE_DIR}/common/unicode/uvernum.h" UVERNUM_H)
string (REGEX REPLACE ".*U_ICU_VERSION_MAJOR_NUM ([0-9]+).*" "\\1" ICU_VERSION_MAJOR ${UVERNUM_H})
string (REGEX REPLACE ".*U_ICU_VERSION_MINOR_NUM ([0-9]+).*" "\\1" ICU_VERSION_MINOR ${UVERNUM_H})

message(STATUS "ICU library version: ${ICU_VERSION_MAJOR}.${ICU_VERSION_MINOR}" )

option(BUILD_SHARED "build shared library" ON)
option(BUILD_STATIC "build static library" ON)

set(CMAKE_DEBUG_POSTFIX "d")

add_subdirectory(common)

message(STATUS ${ICUUC_SRCS})

if(MSVC)
	add_definitions("-D_CRT_SECURE_NO_DEPRECATE")
endif()

add_definitions("-DU_COMMON_IMPLEMENTATION")

add_library(icuuc SHARED ${ICUUC_SRCS})
add_library(icuuc_static SHARED ${ICUUC_SRCS})
