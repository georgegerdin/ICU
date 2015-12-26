# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set(SRCS locbund.cpp sprintf.c sscanf.c ucln_io.cpp 
	ufile.c ufmt_cmn.c uprintf.cpp uprntf_p.c uscanf.c 
	uscanf_p.c ustdio.c ustream.cpp locbund.h ucln_io.h 
	ufile.h ufmt_cmn.h uprintf.h uscanf.h unicode/ustdio.h 
	unicode/ustream.h )
	
foreach(e ${SRCS})
	set(IO_SRCS "${IO_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

add_definitions("-DU_IO_IMPLEMENTATION")
include_directories(${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})

if(BUILD_SHARED)
	add_library(io SHARED ${IO_SRCS})
	target_link_libraries(io icuuc icuin)
	set_target_properties(io PROPERTIES OUTPUT_NAME "icuio${ICU_VERSION_MAJOR}")
	install(TARGETS io RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
if(BUILD_STATIC)
	add_library(sio ${IO_SRCS})
	set_target_properties(sio PROPERTIES OUTPUT_NAME "sicuio${ICU_VERSION_MAJOR}")
	set_target_properties(sio PROPERTIES COMPILE_DEFINITIONS "U_STATIC_IMPLEMENTATION")
	target_link_libraries(sio sicuuc sicuin)
	install(TARGETS sio RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()