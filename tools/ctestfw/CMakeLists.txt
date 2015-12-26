# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set( SRCS ctest.c datamap.cpp testdata.cpp tstdtmod.cpp ucln_ct.c 
	uperf.cpp unicode/ctest.h unicode/datamap.h 
	unicode/testdata.h unicode/testlog.h unicode/testtype.h 
	unicode/tstdtmod.h unicode/uperf.h unicode/utimer.h )
	
foreach(e ${SRCS})
	set(CTESTFW_SRCS "${CTESTFW_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

add_definitions("-DT_CTEST_IMPLEMENTATION")
include_directories(${COMMON_INCLUDE_DIR} ${TOOLUTIL_INCLUDE_DIR})

if(BUILD_SHARED)
	add_library(ctestfw SHARED ${CTESTFW_SRCS})
	target_link_libraries(ctestfw icuuc toolutil)
	set_target_properties(ctestfw PROPERTIES OUTPUT_NAME "icutest${ICU_VERSION_MAJOR}")
	install(TARGETS ctestfw RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
if(BUILD_STATIC)
	add_library(sctestfw ${CTESTFW_SRCS})
	set_target_properties(sctestfw PROPERTIES OUTPUT_NAME "sicutest${ICU_VERSION_MAJOR}")
	set_target_properties(sctestfw PROPERTIES COMPILE_DEFINITIONS "U_STATIC_IMPLEMENTATION")
	target_link_libraries(sctestfw sicuuc )
	install(TARGETS sctestfw RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()