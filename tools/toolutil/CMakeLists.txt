# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set(SRCS collationinfo.cpp denseranges.cpp filestrm.c filetools.cpp flagparser.c 
	package.cpp pkg_genc.c pkg_gencmn.c pkg_icu.cpp pkgitems.cpp ppucd.cpp swapimpl.cpp 
	toolutil.cpp ucbuf.c ucm.c ucmstate.c unewdata.c uoptions.c uparse.c writesrc.c 
	xmlparser.cpp dbgutil.cpp udbgutil.cpp ucln_tu.cpp collationinfo.h denseranges.h 
	filestrm.h filetools.h flagparser.h package.h pkg_genc.h pkg_gencmn.h pkg_icu.h 
	pkg_imp.h ppucd.h swapimpl.h toolutil.h ucbuf.h ucm.h unewdata.h uoptions.h 
	uparse.h writesrc.h xmlparser.h dbgutil.h udbgutil.h )

foreach(e ${SRCS})
	set(TOOLUTIL_SRCS "${TOOLUTIL_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

add_definitions("-DU_TOOLUTIL_IMPLEMENTATION")
include_directories(${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})

if(BUILD_SHARED)
	add_library(toolutil SHARED ${TOOLUTIL_SRCS})
	target_link_libraries(toolutil icuuc icuin)
	set_target_properties(toolutil PROPERTIES OUTPUT_NAME "icutu${ICU_VERSION_MAJOR}")
	install(TARGETS toolutil RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
if(BUILD_STATIC)
	add_library(stoolutil ${TOOLUTIL_SRCS})
	set_target_properties(stoolutil PROPERTIES COMPILE_DEFINITIONS "U_STATIC_IMPLEMENTATION")
	target_link_libraries(stoolutil sicuuc sicuin)
	set_target_properties(stoolutil PROPERTIES OUTPUT_NAME "sicutu${ICU_VERSION_MAJOR}")
	install(TARGETS stoolutil RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()