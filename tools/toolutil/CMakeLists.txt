﻿set(SRCS collationinfo.cpp denseranges.cpp filestrm.c filetools.cpp flagparser.c 
	package.cpp pkg_genc.c pkg_gencmn.c pkg_icu.cpp pkgitems.cpp ppucd.cpp swapimpl.cpp 
	toolutil.cpp ucbuf.c ucm.c ucmstate.c unewdata.c uoptions.c uparse.c writesrc.c 
	xmlparser.cpp dbgutil.cpp udbgutil.cpp ucln_tu.cpp collationinfo.h denseranges.h 
	filestrm.h filetools.h flagparser.h package.h pkg_genc.h pkg_gencmn.h pkg_icu.h 
	pkg_imp.h ppucd.h swapimpl.h toolutil.h ucbuf.h ucm.h unewdata.h uoptions.h 
	uparse.h writesrc.h xmlparser.h dbgutil.h udbgutil.h )

foreach(e ${SRCS})
	set(TOOLUTIL_SRCS "${TOOLUTIL_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(TOOLUTIL_SRCS ${TOOLUTIL_SRCS} PARENT_SCOPE)



