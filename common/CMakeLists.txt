SET(SRCS
	filteredbrk.cpp ubidi.c ubidi_props.c ubidiln.c ubidiwrt.c uloc_keytype.cpp ushape.cpp brkeng.cpp 
	brkiter.cpp dictbe.cpp pluralmap.cpp rbbi.cpp rbbidata.cpp rbbinode.cpp rbbirb.cpp rbbiscan.cpp rbbisetb.cpp 
	rbbistbl.cpp rbbitblb.cpp dictionarydata.cpp ubrk.cpp ucol_swp.cpp propsvec.c uarrsort.c uenum.c uhash.c 
	uhash_us.cpp ulist.c ustack.cpp ustrenum.cpp utrie.cpp utrie2.cpp utrie2_builder.cpp uvector.cpp uvectr32.cpp 
	uvectr64.cpp errorcode.cpp icudataver.c locmap.c putil.cpp umath.c umutex.cpp utrace.c utypes.c wintz.c ucnv.c 
	ucnv2022.cpp ucnv_bld.cpp ucnv_cb.c ucnv_cnv.c ucnv_ct.c ucnv_err.c ucnv_ext.cpp ucnv_io.cpp ucnv_lmb.c 
	ucnv_set.c ucnv_u16.c ucnv_u32.c ucnv_u7.c ucnv_u8.c ucnvbocu.cpp ucnvdisp.c ucnvhz.c ucnvisci.c ucnvlat1.c 
	ucnvmbcs.cpp ucnvscsu.c ucnvsel.cpp cmemory.c ucln_cmn.cpp ucmndata.c udata.cpp udatamem.c udataswp.c uinit.cpp 
	umapfile.c uobject.cpp dtintrv.cpp parsepos.cpp ustrfmt.c util.cpp util_props.cpp punycode.cpp uidna.cpp uts46.cpp 
	locavailable.cpp locbased.cpp locdispnames.cpp locid.cpp loclikely.cpp locresdata.cpp locutil.cpp resbund.cpp 
	resbund_cnv.cpp ucat.c uloc.cpp uloc_tag.c ures_cnv.c uresbund.cpp uresdata.c caniter.cpp filterednormalizer2.cpp 
	loadednormalizer2impl.cpp normalizer2.cpp normalizer2impl.cpp normlzr.cpp unorm.cpp unormcmp.cpp bmpset.cpp 
	patternprops.cpp propname.cpp ruleiter.cpp ucase.cpp uchar.c unames.cpp unifiedcache.cpp unifilt.cpp unifunct.cpp 
	uniset.cpp uniset_closure.cpp uniset_props.cpp unisetspan.cpp uprops.cpp usc_impl.c uscript.c uscript_props.cpp 
	uset.cpp uset_props.cpp usetiter.cpp icuplug.cpp serv.cpp servlk.cpp servlkf.cpp servls.cpp servnotf.cpp servrbf.cpp 
	servslkf.cpp usprep.cpp appendable.cpp bytestream.cpp bytestrie.cpp bytestriebuilder.cpp bytestrieiterator.cpp 
	chariter.cpp charstr.cpp cstring.c cwchar.c messagepattern.cpp schriter.cpp stringpiece.cpp stringtriebuilder.cpp 
	simplepatternformatter.cpp ucasemap.cpp ucasemap_titlecase_brkiter.cpp ucharstrie.cpp ucharstriebuilder.cpp 
	ucharstrieiterator.cpp uchriter.cpp uinvchar.c uiter.cpp unistr.cpp unistr_case.cpp unistr_case_locale.cpp 
	unistr_cnv.cpp unistr_props.cpp unistr_titlecase_brkiter.cpp ustr_cnv.cpp ustr_titlecase_brkiter.cpp ustr_wcs.cpp 
	ustrcase.cpp ustrcase_locale.cpp ustring.cpp ustrtrns.cpp utext.cpp utf_impl.c listformatter.cpp ulistformatter.cpp 
	unicode/ubidi.h localsvc.h msvcres.h pluralmap.h propname_data.h ubidi_props.h ubidiimp.h unicode/ushape.h brkeng.h 
	unicode/brkiter.h unicode/dbbi.h dictbe.h unicode/rbbi.h rbbidata.h rbbinode.h rbbirb.h rbbirpt.h rbbiscan.h 
	rbbisetb.h rbbitblb.h dictionarydata.h unicode/ubrk.h ubidi_props_data.h ubrkimpl.h ucase_props_data.h 
	uchar_props_data.h ucol_data.h ucol_swp.h unistrappender.h hash.h propsvec.h unicode/strenum.h uarrsort.h 
	unicode/uenum.h uelement.h uenumimp.h uhash.h ulist.h unicode/enumset.h unicode/filteredbrk.h ustrenum.h utrie.h 
	utrie2.h utrie2_impl.h utypeinfo.h uvector.h uvectr32.h uvectr64.h cpputils.h unicode/docmain.h unicode/errorcode.h 
	unicode/icudataver.h locmap.h mutex.h unicode/platform.h unicode/ptypes.h unicode/putil.h putilimp.h unicode/std_string.h 
	uassert.h unicode/uconfig.h unicode/umachine.h umutex.h uposixdefs.h unicode/urename.h unicode/utrace.h utracimp.h 
	unicode/utypes.h unicode/uvernum.h unicode/uversion.h wintz.h unicode/ucnv.h ucnv_bld.h unicode/ucnv_cb.h ucnv_cnv.h 
	unicode/ucnv_err.h ucnv_ext.h ucnv_imp.h ucnv_io.h ucnvmbcs.h unicode/ucnvsel.h cmemory.h unicode/localpointer.h 
	unicode/uclean.h ucln.h ucln_cmn.h ucln_imp.h ucmndata.h unicode/udata.h udatamem.h udataswp.h umapfile.h unicode/uobject.h 
	unicode/dtintrv.h unicode/parseerr.h unicode/parsepos.h unicode/umisc.h ustrfmt.h util.h unicode/idna.h punycode.h unicode/uidna.h 
	locbased.h unicode/locid.h locutil.h unicode/resbund.h sharedobject.h sharedobject.cpp simplepatternformatter.h unicode/ucat.h 
	unicode/uloc.h ulocimp.h unicode/ures.h unifiedcache.h uresdata.h uresimp.h ureslocs.h unicode/caniter.h norm2allmodes.h 
	unicode/normalizer2.h normalizer2impl.h unicode/normlzr.h unicode/unorm.h unicode/unorm2.h unormimp.h bmpset.h messageimpl.h
	patternprops.h propname.h ruleiter.h unicode/symtable.h ucase.h unicode/uchar.h unicode/unifilt.h unicode/unifunct.h unicode/unimatch.h 
	unicode/uniset.h unisetspan.h uprops.h usc_impl.h unicode/uscript.h unicode/uset.h uset_imp.h unicode/usetiter.h unicode/icuplug.h icuplugimp.h 
	serv.h servloc.h servnotf.h sprpimpl.h unicode/usprep.h unicode/appendable.h unicode/bytestream.h unicode/bytestrie.h 
	unicode/bytestriebuilder.h unicode/chariter.h charstr.h cstring.h cwchar.h unicode/messagepattern.h unicode/rep.h unicode/schriter.h 
	unicode/stringpiece.h unicode/stringtriebuilder.h unicode/ucasemap.h unicode/ucharstrie.h unicode/ucharstriebuilder.h 
	unicode/uchriter.h uinvchar.h unicode/uiter.h unicode/unistr.h unicode/urep.h ustr_cnv.h ustr_imp.h unicode/ustring.h 
	unicode/ustringtrie.h unicode/utext.h unicode/utf.h unicode/utf16.h unicode/utf32.h unicode/utf8.h unicode/utf_old.h 
	unicode/listformatter.h unicode/ulistformatter.h )
	
foreach(e ${SRCS})
	set(ICUUC_SRCS ${ICUUC_SRCS} "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()
	
set(COMMON_SRCS ${ICUUC_SRCS} PARENT_SCOPE)
