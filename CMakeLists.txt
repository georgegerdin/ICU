project(ICU)

cmake_minimum_required(VERSION 2.8.8)

file(READ "${CMAKE_CURRENT_LIST_DIR}/common/unicode/uvernum.h" UVERNUM_H)
string (REGEX REPLACE ".*U_ICU_VERSION_MAJOR_NUM ([0-9]+).*" "\\1" ICU_VERSION_MAJOR ${UVERNUM_H})
string (REGEX REPLACE ".*U_ICU_VERSION_MINOR_NUM ([0-9]+).*" "\\1" ICU_VERSION_MINOR ${UVERNUM_H})
set(VERSION_STRING "${ICU_VERSION_MAJOR}${ICU_VERSION_MINOR}")

message(STATUS "ICU library version: ${ICU_VERSION_MAJOR}.${ICU_VERSION_MINOR}" )
message(STATUS "Version string: ${VERSION_STRING}" )

option(BUILD_SHARED "build shared library" ON)
option(BUILD_STATIC "build static library" ON)
option(LINK_SHARED "links executables to shared libraries" ON)

set(CMAKE_DEBUG_POSTFIX "d")

set(COMMON_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/common")
set(I18N_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/i18n")
set(IO_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/io")
set(TOOLUTIL_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/tools/toolutil")

if(MSVC)
	add_definitions("-D_CRT_SECURE_NO_DEPRECATE")
endif()

add_subdirectory(common)
add_subdirectory(stubdata)
add_subdirectory(samples)
add_subdirectory(i18n)
add_subdirectory(tools)
add_subdirectory(io)


include_directories(	${COMMON_INCLUDE_DIR} 
						${I18N_INCLUDE_DIR}
						${IO_INCLUDE_DIR}
						${TOOLUTIL_INCLUDE_DIR}
					)

if(BUILD_SHARED)
endif()

if(BUILD_STATIC)
endif()

set(ICU_I18N_LIBRARY icuin)
set(ICU_COMMON_LIBRARY icuuc)
set(ICU_IO_LIBRARY io)
set(ICU_TOOLUTIL_LIBRARY toolutil)

if(NOT LINK_SHARED)
	set(ICU_I18N_LIBRARY "s${ICU_I18N_LIBRARY}")
	set(ICU_COMMON_LIBRARY "s${ICU_COMMON_LIBRARY}")
	set(ICU_IO_LIBRARY "s${ICU_IO_LIBRARY}")
	set(ICU_TOOLUTIL_LIBRARY "s${ICU_TOOLUTIL_LIBRARY}")
endif()

add_executable(cal ${CAL_SRCS})
target_link_libraries(cal ${ICU_I18N_LIBRARY})
add_executable(date	${DATE_SRCS})
target_link_libraries(date ${ICU_I18N_LIBRARY} ${ICU_COMMON_LIBRARY})
add_executable(derb ${DERB_SRCS})
target_link_libraries(derb ${ICU_IO_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
add_executable(genrb ${GENRB_SRCS})
target_link_libraries(genrb ${ICU_IO_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
add_executable(genbrk ${GENBRK_SRCS})
target_link_libraries(genbrk ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
add_executable(genccode ${GENCCODE_SRCS})
target_link_libraries(genccode ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})

