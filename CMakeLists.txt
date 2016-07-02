cmake_minimum_required(VERSION 2.8.8)

project(ICU)

# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/lib)
set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/bin)

file(READ "${CMAKE_CURRENT_LIST_DIR}/common/unicode/uvernum.h" UVERNUM_H)
file(WRITE "${CMAKE_CURRENT_BINARY_DIR}/dummy.c" "int main(int argc, char* argv[]) {return 0;}")
string (REGEX REPLACE ".*U_ICU_VERSION_MAJOR_NUM ([0-9]+).*" "\\1" ICU_VERSION_MAJOR ${UVERNUM_H})
string (REGEX REPLACE ".*U_ICU_VERSION_MINOR_NUM ([0-9]+).*" "\\1" ICU_VERSION_MINOR ${UVERNUM_H})
set(VERSION_STRING "${ICU_VERSION_MAJOR}${ICU_VERSION_MINOR}")

message(STATUS "ICU library version: ${ICU_VERSION_MAJOR}.${ICU_VERSION_MINOR}" )
message(STATUS "Version string: ${VERSION_STRING}" )

option(BUILD_SHARED "build shared library" ON)
option(BUILD_STATIC "build static library" OFF)
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

if(UNIX)
	set(UNIX_MATH_LIB "m")
	set(UNIX_THREAD_LIB "pthread")
	add_definitions("-DU_HAVE_ELF_H=1")
	add_definitions("-DU_HAVE_ATOMIC=1")
	add_definitions("-DUDATA_SO_SUFFIX=\".so\"")
else()
	add_definitions("-DUDATA_SO_SUFFIX=\".dll\"")
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

set(ICU_I18N_SHARED_LIBRARY i18n)
set(ICU_COMMON_SHARED_LIBRARY common)
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

if(BUILD_SHARED)
	add_library(common SHARED ${COMMON_SRCS})
	add_library(i18n SHARED ${I18N_SRCS})
	add_library(io SHARED ${IO_SRCS})
	add_library(toolutil SHARED ${TOOLUTIL_SRCS})
	add_library(ctestfw SHARED ${CTESTFW_SRCS})
	add_library(stubdata SHARED ${STUBDATA_SRCS})
	add_library(layout SHARED ${LAYOUT_SRCS})
	add_library(layoutex SHARED ${LAYOUTEX_SRCS})
		
	target_include_directories(i18n			PRIVATE ${COMMON_INCLUDE_DIR})
	target_include_directories(io			PRIVATE ${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})
	target_include_directories(toolutil		PRIVATE ${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})
	target_include_directories(ctestfw		PRIVATE ${COMMON_INCLUDE_DIR} ${TOOLUTIL_INCLUDE_DIR})
	target_include_directories(common		PRIVATE ${COMMON_INCLUDE_DIR})
	target_include_directories(layout		PRIVATE ${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})
	target_include_directories(layoutex		PRIVATE ${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR} ${BASE_INCLUDE_DIR})
	
	target_link_libraries(common			stubdata ${CMAKE_DL_LIBS})
	target_link_libraries(i18n 				common)
	target_link_libraries(io 				common i18n)
	target_link_libraries(toolutil 			common i18n)
	target_link_libraries(ctestfw 			common toolutil)
#	target_link_libraries(stubdata			)
	target_link_libraries(layout 			common i18n)
	target_link_libraries(layoutex 			common i18n layout)
		
	set_target_properties(common 			PROPERTIES OUTPUT_NAME "icuuc${ICU_VERSION_MAJOR}")
	set_target_properties(i18n 				PROPERTIES OUTPUT_NAME "icuin${ICU_VERSION_MAJOR}")
	set_target_properties(io 				PROPERTIES OUTPUT_NAME "icuio${ICU_VERSION_MAJOR}")
	set_target_properties(toolutil 			PROPERTIES OUTPUT_NAME "icutu${ICU_VERSION_MAJOR}")
	set_target_properties(ctestfw 			PROPERTIES OUTPUT_NAME "icutest${ICU_VERSION_MAJOR}")
	set_target_properties(stubdata 			PROPERTIES OUTPUT_NAME "icudt${ICU_VERSION_MAJOR}")
	set_target_properties(layout 			PROPERTIES OUTPUT_NAME "icule${ICU_VERSION_MAJOR}")
	set_target_properties(layoutex 			PROPERTIES OUTPUT_NAME "iculx${ICU_VERSION_MAJOR}")

	target_compile_definitions(common 		PRIVATE U_COMMON_IMPLEMENTATION)
	target_compile_definitions(i18n 		PRIVATE U_I18N_IMPLEMENTATION)
	target_compile_definitions(io			PRIVATE U_IO_IMPLEMENTATION)
	target_compile_definitions(toolutil 	PRIVATE U_TOOLUTIL_IMPLEMENTATION)
	target_compile_definitions(ctestfw		PRIVATE T_CTEST_IMPLEMENTATION)
	target_compile_definitions(stubdata 	PRIVATE STUBDATA_BUILD)
	target_compile_definitions(layout		PRIVATE U_LAYOUT_IMPLEMENTATION)
	target_compile_definitions(layoutex		PRIVATE U_LAYOUTEX_IMPLEMENTATION)

	install(TARGETS common RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS i18n RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS io RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS toolutil RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS ctestfw RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS stubdata RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS layout RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS layoutex RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()

if(BUILD_STATIC)
	add_library(scommon ${COMMON_SRCS})
	add_library(si18n ${I18N_SRCS})
	add_library(sio ${IO_SRCS})
	add_library(stoolutil ${TOOLUTIL_SRCS})
	add_library(sctestfw ${CTESTFW_SRCS})
	add_library(stubdata_static ${STUBDATA_SRCS})
	add_library(slayout ${LAYOUT_SRCS})
	add_library(slayoutex ${LAYOUTEX_SRCS})
		
	target_include_directories(si18n		PRIVATE ${COMMON_INCLUDE_DIR})
	target_include_directories(sio			PRIVATE ${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})
	target_include_directories(stoolutil 	PRIVATE ${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})
	target_include_directories(sctestfw		PRIVATE ${COMMON_INCLUDE_DIR} ${TOOLUTIL_INCLUDE_DIR})
	target_include_directories(scommon		PRIVATE ${COMMON_INCLUDE_DIR})
		
	target_link_libraries(scommon 			stubdata_static ${CMAKE_DL_LIBS})
	target_link_libraries(si18n 			scommon)
	target_link_libraries(sio 				scommon si18n)
	target_link_libraries(stoolutil 		scommon si18n)
	target_link_libraries(sctestfw 			scommon )
	target_link_libraries(slayout 			scommon si18n)
	target_link_libraries(slayoutex 		scommon si18n slayout)
		
	set_target_properties(scommon 			PROPERTIES OUTPUT_NAME "sicuuc${ICU_VERSION_MAJOR}")
	set_target_properties(si18n 			PROPERTIES OUTPUT_NAME "sicuin${ICU_VERSION_MAJOR}")
	set_target_properties(sio 				PROPERTIES OUTPUT_NAME "sicuio${ICU_VERSION_MAJOR}")
	set_target_properties(stoolutil 		PROPERTIES OUTPUT_NAME "sicutu${ICU_VERSION_MAJOR}")
	set_target_properties(sctestfw 			PROPERTIES OUTPUT_NAME "sicutest${ICU_VERSION_MAJOR}")
	set_target_properties(stubdata_static 	PROPERTIES OUTPUT_NAME "sicudt${ICU_VERSION_MAJOR}")
	set_target_properties(slayout 			PROPERTIES OUTPUT_NAME "sicule${ICU_VERSION_MAJOR}")
	set_target_properties(slayoutex 		PROPERTIES OUTPUT_NAME "siculx${ICU_VERSION_MAJOR}")
	
	target_compile_definitions(scommon 		PRIVATE U_STATIC_IMPLEMENTATION U_COMMON_IMPLEMENTATION)
	target_compile_definitions(si18n 		PRIVATE U_STATIC_IMPLEMENTATION U_I18N_IMPLEMENTATION)
	target_compile_definitions(sio 			PRIVATE U_STATIC_IMPLEMENTATION U_IO_IMPLEMENTATION)	
	target_compile_definitions(stoolutil 	PRIVATE U_STATIC_IMPLEMENTATION U_TOOLUTIL_IMPLEMENTATION)
	target_compile_definitions(sctestfw 	PRIVATE U_STATIC_IMPLEMENTATION T_CTEST_IMPLEMENTATION)
	target_compile_definitions(stubdata_static PRIVATE U_STATIC_IMPLEMENTATION STUBDATA_BUILD)
	target_compile_definitions(slayout		PRIVATE U_STATIC_IMPLEMENTATION U_LAYOUT_IMPLEMENTATION)
	target_compile_definitions(slayoutex 	PRIVATE U_STATIC_IMPLEMENTATION U_LAYOUTEX_IMPLEMENTATION)

	install(TARGETS scommon RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS si18n RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS stoolutil RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS sctestfw RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS stubdata_static RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS slayout RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	install(TARGETS slayoutex RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})	
	install(TARGETS sio RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
	

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
add_executable(makedata ${CMAKE_CURRENT_BINARY_DIR}/dummy.c)
add_executable(pkgdata ${PKGDATA_SRCS})
add_library(testplug SHARED ${TESTPLUG_SRCS})
add_executable(uconv ${UCONV_SRCS})
add_executable(cintltst ${CINTLTST_SRCS})
add_executable(intltest ${INTLTEST_SRCS})
add_executable(iotest ${IOTEST_SRCS})
add_executable(letest ${LETEST_SRCS})

target_link_libraries(cal ${ICU_I18N_LIBRARY} ${CMAKE_DL_LIBS})
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
target_link_libraries(cintltst ${ICU_COMMON_LIBRARY} ${ICU_CTESTFW_LIBRARY} ${UNIX_MATH_LIB} ${UNIX_THREAD_LIB})
target_link_libraries(intltest ${ICU_COMMON_LIBRARY} ${ICU_CTESTFW_LIBRARY} ${UNIX_THREAD_LIB})
target_link_libraries(iotest ${ICU_COMMON_LIBRARY} ${ICU_IO_LIBRARY} ${ICU_CTESTFW_LIBRARY})
target_link_libraries(letest ${ICU_COMMON_LIBRARY} ${ICU_LAYOUT_LIBRARY} ${ICU_LAYOUTEX_LIBRARY} ${ICU_CTESTFW_LIBRARY})

if(WIN32)
	set(DLLENDING "dll")
else()
	set(DLLENDING "so")
endif()

if(MSVC)
	set(DLLSUFFIX 
   		$<$<CONFIG:Debug>:d>
    		$<$<CONFIG:RelWithDebInfo>:d>
    		$<$<CONFIG:Release>:> 
    		$<$<CONFIG:MinSizeRel>:>
    	)
else()
	if(CMAKE_BUILD_TYPE MATCHES DEBUG)
		set(DLLSUFFIX "d")
	endif()
endif()

if(MSVC)
	set(RELEASE_HELPER "\"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/\$\(Configuration\)\"")
	set(DEST_PATH "\"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/\$\(Configuration\)/icudt${ICU_VERSION_MAJOR}l\"")
	set(TEST_PATH "\"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/\$\(Configuration\)\"")
else()
	set(RELEASE_HELPER "\"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/\"")
	set(DEST_PATH "\"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/icudt${ICU_VERSION_MAJOR}l\"")
	set(TEST_PATH "\"${CMAKE_RUNTIME_OUTPUT_DIRECTORY}/\"")
endif()

set(UCONV_HELPER "\"${CMAKE_CURRENT_BINARY_DIR}/uconv_resources\"")
set(OUT_TEMP_PATH "\"${CMAKE_CURRENT_BINARY_DIR}/tmp\"")
set(IN_DATA_PATH "\"${CMAKE_CURRENT_LIST_DIR}/data/in/icudt${ICU_VERSION_MAJOR}l.dat\"")
set(OUT_DATA_PATH "\"${CMAKE_CURRENT_BINARY_DIR}/tmp/icudata.lst\"")
set(ICUDTDLL "\"${CMAKE_CURRENT_BINARY_DIR}/icudt${ICU_VERSION_MAJOR}${DLLSUFFIX}.${DLLENDING}\"")


if(WIN32)
	string(REGEX REPLACE "/" "\\\\" RELEASE_HELPER ${RELEASE_HELPER})
	string(REGEX REPLACE "/" "\\\\" UCONV_HELPER ${UCONV_HELPER})
	string(REGEX REPLACE "/" "\\\\" OUT_TEMP_PATH ${OUT_TEMP_PATH})
	string(REGEX REPLACE "/" "\\\\" IN_DATA_PATH ${IN_DATA_PATH})
	string(REGEX REPLACE "/" "\\\\" OUT_DATA_PATH ${OUT_DATA_PATH})
	string(REGEX REPLACE "/" "\\\\" DEST_PATH ${DEST_PATH})
	string(REGEX REPLACE "/" "\\\\" TEST_PATH ${TEST_PATH})
	string(REGEX REPLACE "/" "\\\\" ICUDTDLL ${ICUDTDLL})
endif()

message(STATUS "Release helper: ${RELEASE_HELPER}")
message(STATUS "Uconv helper:   ${UCONV_HELPER}")
message(STATUS "Out temp path:  ${OUT_TEMP_PATH}")
message(STATUS "In data path:   ${IN_DATA_PATH}")
message(STATUS "Out data path:  ${OUT_DATA_PATH}")
message(STATUS "Dest path:      ${DEST_PATH}")
message(STATUS "Test path:      ${TEST_PATH}")
message(STATUS "ICUDTDLL: 		${ICUDTDLL}")

add_custom_command(
	TARGET uconv
	PRE_BUILD
	COMMAND genrb -s uconv_resources -d uconv_resources root.txt
	COMMAND genrb -s uconv_resources -d uconv_resources fr.txt
	COMMAND pkgdata -f -v -m static -c -p uconvmsg -d ${RELEASE_HELPER} -s ${UCONV_HELPER} uconvpkgdatain.txt

	COMMENT Making resource bundle files...
	WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
#	VERBATIM
)

add_custom_command(
	TARGET makedata
	PRE_BUILD
	COMMAND ${CMAKE_COMMAND} -E make_directory ${OUT_TEMP_PATH}
	COMMAND ${CMAKE_COMMAND} -E echo "${PROJECT_BINARY_DIR}/\$\(Configuration\)/your_library.dll"
	COMMAND ${CMAKE_COMMAND} -E echo "${TEST_PATH}"
	COMMAND ${CMAKE_COMMAND} -E echo pkgdata -f -e icudt${ICU_VERSION_MAJOR}${DLLSUFFIX} -v -m dll -c -p icudt${ICU_VERSION_MAJOR}l -T ${OUT_TEMP_PATH} -L icudt${ICU_VERSION_MAJOR} -d . -s ${DEST_PATH} ${OUT_DATA_PATH}
	
	COMMAND icupkg -x * --list ${IN_DATA_PATH} > ${OUT_DATA_PATH}
	COMMAND pkgdata -f -e icudt${ICU_VERSION_MAJOR}${DLLSUFFIX} -v -m dll -c -p icudt${ICU_VERSION_MAJOR}l -T ${OUT_TEMP_PATH} -L icudt${ICU_VERSION_MAJOR} -d ${DEST_PATH} -s . ${OUT_DATA_PATH}
	
	COMMAND ${CMAKE_COMMAND} -E copy_if_different ${ICUDTDLL} ${RELEASE_HELPER}
	COMMENT Building icu data from icudt${ICU_VERSION_MAJOR}l.dat
	WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}
)


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

