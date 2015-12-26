set(SRCS date.c uprint.c uprint.h)

foreach(e ${SRCS})
	set(DATE_SRCS "${DATE_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(DATE_SRCS "${DATE_SRCS}" PARENT_SCOPE)