cmake_minimum_required(VERSION 2.8.8)

project(ICU)

# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)


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

set(BASE_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}")
set(COMMON_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/common")
set(I18N_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/i18n")
set(IO_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/io")
set(TOOLUTIL_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/tools/toolutil")
set(LAYOUT_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/layout")
set(LAYOUTEX_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/layoutex")
set(CTESTFW_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/tools/ctestfw")

if(MSVC)
	add_definitions("-D_CRT_SECURE_NO_DEPRECATE")
	add_definitions("-DUCONFIG_ENABLE_PLUGINS")
endif()

add_subdirectory(common)
add_subdirectory(stubdata)
add_subdirectory(samples)
add_subdirectory(i18n)
add_subdirectory(tools)
add_subdirectory(io)
add_subdirectory(layout)
add_subdirectory(layoutex)
add_subdirectory(extra)
add_subdirectory(test)

include_directories(	${BASE_INCLUDE_DIR}
						${COMMON_INCLUDE_DIR} 
						${I18N_INCLUDE_DIR}
						${IO_INCLUDE_DIR}
						${TOOLUTIL_INCLUDE_DIR}
						${CTESTFW_INCLUDE_DIR}
						${LAYOUT_INCLUDE_DIR}
						${LAYOUTEX_INCLUDE_DIR}
					)

if(BUILD_SHARED)
endif()

if(BUILD_STATIC)
endif()

set(LIBRARIES I18N COMMON IO TOOLUTIL CTESTFW LAYOUT LAYOUTEX)

set(ICU_I18N_SHARED_LIBRARY icuin)
set(ICU_COMMON_SHARED_LIBRARY icuuc)
set(ICU_IO_SHARED_LIBRARY io)
set(ICU_TOOLUTIL_SHARED_LIBRARY toolutil)
set(ICU_CTESTFW_SHARED_LIBRARY ctestfw)
set(ICU_LAYOUT_SHARED_LIBRARY layout)
set(ICU_LAYOUTEX_SHARED_LIBRARY layoutex)

foreach(lib ${LIBRARIES})
	set(ICU_${lib}_LIBRARY "${ICU_${lib}_SHARED_LIBRARY}")
	set(ICU_${lib}_STATIC_LIBRARY "s${ICU_${lib}_SHARED_LIBRARY}")
	if(LINK_SHARED)
		set(ICU_${lib}_LIBRARY "${ICU_${lib}_SHARED_LIBRARY}")
	else()
		set(ICU_${lib}_LIBRARY "${ICU_${lib}_STATIC_LIBRARY}")
	endif()
	if(BUILD_SHARED)
		set(FULL_LIBRARIES ${FULL_LIBRARIES} "${ICU_${lib}_SHARED_LIBRARY}")
	endif()
	if(BUILD_STATIC)
		set(FULL_LIBRARIES ${FULL_LIBRARIES} "${ICU_${lib}_STATIC_LIBRARY}")
	endif()
endforeach()

add_executable(cal ${CAL_SRCS})
add_executable(date	${DATE_SRCS})
add_executable(derb ${DERB_SRCS})
add_executable(genrb ${GENRB_SRCS})
add_executable(genbrk ${GENBRK_SRCS})
add_executable(genccode ${GENCCODE_SRCS})
add_executable(gencfu ${GENCFU_SRCS})
add_executable(gencmn ${GENCMN_SRCS})
add_executable(gencnval ${GENCNVAL_SRCS})
add_executable(gendict ${GENDICT_SRCS})
add_executable(gennorm2 ${GENNORM2_SRCS})
add_executable(gensprep ${GENSPREP_SRCS})
add_executable(gentest ${GENTEST_SRCS})
add_executable(icuinfo ${ICUINFO_SRCS})
add_executable(icupkg ${ICUPKG_SRCS})
add_executable(makeconv ${MAKECONV_SRCS})
add_executable(pkgdata ${PKGDATA_SRCS})
add_library(testplug SHARED ${TESTPLUG_SRCS})
add_executable(uconv ${UCONV_SRCS})
add_executable(cintltst ${CINTLTST_SRCS})
add_executable(intltest ${INTLTEST_SRCS})
add_executable(iotest ${IOTEST_SRCS})
add_executable(letest ${LETEST_SRCS})

target_link_libraries(cal ${ICU_I18N_LIBRARY})
target_link_libraries(date ${ICU_I18N_LIBRARY} ${ICU_COMMON_LIBRARY})
target_link_libraries(derb ${ICU_IO_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(genrb ${ICU_IO_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(genbrk ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(genccode ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gencfu ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gencmn ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gencnval ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gendict ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gennorm2 ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gensprep ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(gentest ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(icuinfo ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(icupkg ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(makeconv ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(pkgdata ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(testplug ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(uconv ${ICU_COMMON_LIBRARY} ${ICU_TOOLUTIL_LIBRARY})
target_link_libraries(cintltst ${ICU_COMMON_LIBRARY} ${ICU_CTESTFW_LIBRARY})
target_link_libraries(intltest ${ICU_COMMON_LIBRARY} ${ICU_CTESTFW_LIBRARY})
target_link_libraries(iotest ${ICU_COMMON_LIBRARY} ${ICU_IO_LIBRARY} ${ICU_CTESTFW_LIBRARY})
target_link_libraries(letest ${ICU_COMMON_LIBRARY} ${ICU_LAYOUT_LIBRARY} ${ICU_LAYOUTEX_LIBRARY} ${ICU_CTESTFW_LIBRARY})

file(GLOB LAYOUT_HDRS "${LAYOUTEX_INCLUDE_DIR}/layout/*.h")
file(GLOB UNICODE_HDRS "${COMMON_INCLUDE_DIR}/unicode/*.h" "${I18N_INCLUDE_DIR}/unicode/*.h")

set(MORE_LAYOUT_HDRS LayoutEngine.h LEFontInstance.h LEGlyphFilter.h LEGlyphStorage.h LEInsertionList.h LELanguages.h LEScripts.h LESwaps.h LETypes.h loengine.h)
foreach(e ${MORE_LAYOUT_HDRS})
	set(LAYOUT_HDRS "${LAYOUT_HDRS}" "${LAYOUT_INCLUDE_DIR}/${e}")
endforeach()

set(BINARIES cal date derb genrb genbrk genccode gencfu gencmn gencnval gendict
	gennorm2 gensprep gentest icuinfo icupkg makeconv pkgdata testplug uconv
	cintltst intltest iotest)

install(FILES ${LAYOUT_HDRS} DESTINATION ${CMAKE_INSTALL_FULL_INCLUDEDIR}/layout)
install(FILES ${UNICODE_HDRS} DESTINATION ${CMAKE_INSTALL_FULL_INCLUDEDIR}/unicode)
install(TARGETS ${BINARIES} RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})

