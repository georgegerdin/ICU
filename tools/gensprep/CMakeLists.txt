set(SRCS gensprep.c gensprep.h store.c)

foreach(e ${SRCS})
	set(GENSPREP_SRCS "${GENSPREP_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(GENSPREP_SRCS "${GENSPREP_SRCS}" PARENT_SCOPE)