set(SRCS
	filetst.c iotest.cpp stream.cpp
	strtst.c trnstst.c iotest.h )
	
	
foreach(e ${SRCS})
	set(IOTEST_SRCS "${IOTEST_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(IOTEST_SRCS ${IOTEST_SRCS} PARENT_SCOPE)
