set(DERB_SRCS ${CMAKE_CURRENT_LIST_DIR}/derb.cpp PARENT_SCOPE)
set(SRCS errmsg.c genrb.cpp parse.cpp prscmnts.cpp rbutil.c read.c 			
	reslist.cpp rle.c ustr.c wrtjava.cpp wrtxml.cpp errmsg.h genrb.h parse.h 
	prscmnts.h rbutil.h read.h reslist.h rle.h ustr.h)
	
foreach(e ${SRCS})
	set(GENRB_SRCS "${GENRB_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(GENRB_SRCS "${GENRB_SRCS}" PARENT_SCOPE)