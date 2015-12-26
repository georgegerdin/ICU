# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set(SRCS LXUtilities.cpp ParagraphLayout.cpp playout.cpp plruns.cpp 
	RunArrays.cpp LXUtilities.h layout/ParagraphLayout.h 
	layout/playout.h layout/plruns.h layout/RunArrays.h )
	
foreach(e ${SRCS})
	set(LAYOUTEX_SRCS "${LAYOUTEX_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

add_definitions("-DU_LAYOUTEX_IMPLEMENTATION")
include_directories(${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR} ${BASE_INCLUDE_DIR})

if(BUILD_SHARED)
	add_library(layoutex SHARED ${LAYOUTEX_SRCS})
	target_link_libraries(layoutex icuuc icuin layout)
	set_target_properties(layoutex PROPERTIES OUTPUT_NAME "iculx${ICU_VERSION_MAJOR}")
	install(TARGETS layoutex RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
if(BUILD_STATIC)
	add_library(slayoutex ${LAYOUTEX_SRCS})
	set_target_properties(slayoutex PROPERTIES OUTPUT_NAME "siculx${ICU_VERSION_MAJOR}")
	set_target_properties(slayoutex PROPERTIES COMPILE_DEFINITIONS "U_STATIC_IMPLEMENTATION")
	target_link_libraries(slayoutex sicuuc sicuin slayout)
	install(TARGETS slayoutex RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
	
endif()