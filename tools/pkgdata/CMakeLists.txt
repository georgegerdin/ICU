set(SRCS pkgdata.cpp pkgtypes.c pkgtypes.h)

foreach(e ${SRCS})
	set(PKGDATA_SRCS "${PKGDATA_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(PKGDATA_SRCS "${PKGDATA_SRCS}" PARENT_SCOPE)
