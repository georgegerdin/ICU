set(SRCS cal.c uprint.c uprint.h)

foreach(e ${SRCS})
	set(CAL_SRCS "${CAL_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(CAL_SRCS "${CAL_SRCS}" PARENT_SCOPE)