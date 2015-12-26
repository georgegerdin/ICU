set(SRCS cfonts.cpp cletest.c cmaps.cpp FontTableCache.cpp 
	letest.cpp letsutil.cpp PortableFontInstance.cpp 
	SimpleFontInstance.cpp xmlreader.cpp cfonts.h cmaps.h 
	FontTableCache.h letest.h letsutil.h PortableFontInstance.h 
	sfnt.h SimpleFontInstance.h xmlreader.h )
	
foreach(e ${SRCS})
	set(LETEST_SRCS "${LETEST_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(LETEST_SRCS "${LETEST_SRCS}" PARENT_SCOPE)