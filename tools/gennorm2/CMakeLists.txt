set(SRCS gennorm2.cpp n2builder.cpp n2builder.h)

foreach(e ${SRCS})
	set(GENNORM2_SRCS "${GENNORM2_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(GENNORM2_SRCS "${GENNORM2_SRCS}" PARENT_SCOPE)