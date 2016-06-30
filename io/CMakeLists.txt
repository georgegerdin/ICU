set(SRCS locbund.cpp sprintf.c sscanf.c ucln_io.cpp 
	ufile.c ufmt_cmn.c uprintf.cpp uprntf_p.c uscanf.c 
	uscanf_p.c ustdio.c ustream.cpp locbund.h ucln_io.h 
	ufile.h ufmt_cmn.h uprintf.h uscanf.h unicode/ustdio.h 
	unicode/ustream.h )
	
foreach(e ${SRCS})
	set(IO_SRCS "${IO_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()


set(IO_SRCS ${IO_SRCS} PARENT_SCOPE)