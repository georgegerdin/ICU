set( SRCS ctest.c datamap.cpp testdata.cpp tstdtmod.cpp ucln_ct.c 
	uperf.cpp unicode/ctest.h unicode/datamap.h 
	unicode/testdata.h unicode/testlog.h unicode/testtype.h 
	unicode/tstdtmod.h unicode/uperf.h unicode/utimer.h )
	
foreach(e ${SRCS})
	set(CTESTFW_SRCS "${CTESTFW_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(CTESTFW_SRCS ${CTESTFW_SRCS} PARENT_SCOPE)
