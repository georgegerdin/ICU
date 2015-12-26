set(SRCS genres32.c gentest.c gentest.h)

foreach(e ${SRCS})
	set(GENTEST_SRCS "${GENTEST_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(GENTEST_SRCS "${GENTEST_SRCS}" PARENT_SCOPE)