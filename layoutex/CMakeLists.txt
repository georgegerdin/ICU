set(SRCS LXUtilities.cpp ParagraphLayout.cpp playout.cpp plruns.cpp 
	RunArrays.cpp LXUtilities.h layout/ParagraphLayout.h 
	layout/playout.h layout/plruns.h layout/RunArrays.h )
	
foreach(e ${SRCS})
	set(LAYOUTEX_SRCS "${LAYOUTEX_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(LAYOUTEX_SRCS ${LAYOUTEX_SRCS} PARENT_SCOPE)
