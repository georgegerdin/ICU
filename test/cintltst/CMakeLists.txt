set( SRCS cbididat.c cbiditst.c cbiapts.c cbkittst.c 
	callcoll.c capitst.c ccolltst.c ccurrtst.c cdetst.c 
	cestst.c cfintst.c cfrtst.c cg7coll.c citertst.c cjaptst.c 
	cmsccoll.c cturtst.c encoll.c  usrchtst.c 
	chashtst.c sorttest.c trie2test.c trietest.c uenumtst.c 
	bocu1tst.c ccapitst.c cconvtst.c cctest.c eurocreg.c 
	nccbtst.c ncnvfbts.c ncnvtst.c nucnvtst.c stdnmtst.c 
	ucnvseltst.c ucsdetst.c udatatst.c ccaltst.c 
	cdateintervalformattest.c cdattst.c cdtdptst.c cdtrgtst.c 
	cformtst.c cgendtst.c cmsgtst.c cnmdptst.c cnumtst.c 
	cpluralrulestest.c currtest.c udatpg_test.c utmstest.c 
	cldrtest.c cloctst.c cposxtst.c crestst.c creststn.c 
	calltest.c cintltst.c cutiltst.c hpmufn.c putiltst.c 
	tracetst.c cnormtst.c cucdapi.c cucdtst.c usettest.c 
	cstrcase.c cstrtest.c custrtrn.c custrtst.c utexttst.c 
	utf16tst.c utf8tst.c utransts.c reapits.c idnatest.c 
	nfsprep.c spreptst.c sprpdata.c spooftest.c uregiontest.c 
	ulistfmttest.c cbiditst.h cbiapts.h callcoll.h capitst.h 
	ccolltst.h ccurrtst.h cdetst.h cestst.h cfintst.h cfrtst.h 
	cg7coll.h citertst.h cjaptst.h cturtst.h encoll.h 
	ccapitst.h nccbtst.h ncnvfbts.h nucnvtst.h ucnvseltst.h 
	ccaltst.h cdattst.h cdtdptst.h cdtrgtst.h cformtst.h 
	cmsgtst.h cnmdptst.h cnumtst.h cloctst.h crestst.h 
	creststn.h cintltst.h cnormtst.h cucdapi.h nfsprep.h)
	
foreach(e ${SRCS})
	set(CINTLTST_SRCS "${CINTLTST_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(CINTLTST_SRCS "${CINTLTST_SRCS}" PARENT_SCOPE)