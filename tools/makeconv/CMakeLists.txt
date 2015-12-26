set(SRCS gencnvex.c genmbcs.cpp makeconv.cpp ucnvstat.c genmbcs.h makeconv.h )

foreach(e ${SRCS})
	set(MAKECONV_SRCS "${MAKECONV_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(MAKECONV_SRCS "${MAKECONV_SRCS}" PARENT_SCOPE)