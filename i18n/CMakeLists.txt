# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set(SRCS
	region.cpp uregion.cpp alphaindex.cpp bocsu.cpp coleitr.cpp coll.cpp collation.cpp collationbuilder.cpp 
	collationcompare.cpp collationdata.cpp collationdatabuilder.cpp collationdatareader.cpp collationdatawriter.cpp 
	collationfastlatin.cpp collationfastlatinbuilder.cpp collationfcd.cpp collationiterator.cpp collationkeys.cpp 
	collationroot.cpp collationrootelements.cpp collationruleparser.cpp collationsets.cpp collationsettings.cpp 
	collationtailoring.cpp collationweights.cpp rulebasedcollator.cpp search.cpp sortkey.cpp stsearch.cpp tzfmt.cpp 
	tzgnames.cpp tznames.cpp tznames_impl.cpp ucol.cpp ucol_res.cpp ucol_sit.cpp ucoleitr.cpp affixpatternparser.cpp 
	decimfmtimpl.cpp digitaffix.cpp digitaffixesandpadding.cpp digitformatter.cpp digitgrouping.cpp digitinterval.cpp 
	pluralaffix.cpp precision.cpp smallintformatter.cpp valueformatter.cpp visibledigits.cpp 
	uitercollationiterator.cpp usearch.cpp astro.cpp basictz.cpp buddhcal.cpp calendar.cpp cecal.cpp chnsecal.cpp 
	choicfmt.cpp compactdecimalformat.cpp coptccal.cpp curramt.cpp currfmt.cpp currpinf.cpp currunit.cpp dangical.cpp 
	datefmt.cpp dcfmtsym.cpp decContext.c decfmtst.cpp decimalformatpattern.cpp decimfmt.cpp decNumber.c digitlst.cpp 
	dtfmtsym.cpp dtitvfmt.cpp dtitvinf.cpp dtptngen.cpp dtrule.cpp ethpccal.cpp fmtable.cpp fmtable_cnv.cpp 
	format.cpp fphdlimp.cpp fpositer.cpp gender.cpp gregocal.cpp gregoimp.cpp hebrwcal.cpp identifier_info.cpp 
	indiancal.cpp islamcal.cpp japancal.cpp locdspnm.cpp measfmt.cpp measunit.cpp measure.cpp msgfmt.cpp nfrs.cpp 
	nfrule.cpp nfsubs.cpp numfmt.cpp numsys.cpp olsontz.cpp persncal.cpp plurfmt.cpp plurrule.cpp 
	quantityformatter.cpp rbnf.cpp rbtz.cpp reldatefmt.cpp reldtfmt.cpp scientificnumberformatter.cpp 
	sharedbreakiterator.cpp selfmt.cpp simpletz.cpp scriptset.cpp smpdtfmt.cpp smpdtfst.cpp taiwncal.cpp timezone.cpp 
	tmunit.cpp tmutamt.cpp tmutfmt.cpp tzrule.cpp tztrans.cpp ucal.cpp ucurr.cpp udat.cpp udateintervalformat.cpp 
	udatpg.cpp ufieldpositer.cpp ulocdata.c umsg.cpp unum.cpp unumsys.cpp upluralrules.cpp utf16collationiterator.cpp 
	utf8collationiterator.cpp utmscale.c vtzone.cpp vzone.cpp windtfmt.cpp winnmfmt.cpp wintzimpl.cpp zonemeta.cpp 
	zrule.cpp ztrans.cpp ucln_in.cpp regexcmp.cpp regeximp.cpp regexst.cpp regextxt.cpp rematch.cpp repattrn.cpp 
	uregex.cpp uregexc.cpp anytrans.cpp brktrans.cpp casetrn.cpp cpdtrans.cpp esctrn.cpp funcrepl.cpp name2uni.cpp 
	nortrans.cpp nultrans.cpp quant.cpp rbt.cpp rbt_data.cpp rbt_pars.cpp rbt_rule.cpp rbt_set.cpp remtrans.cpp 
	strmatch.cpp strrepl.cpp titletrn.cpp tolowtrn.cpp toupptrn.cpp translit.cpp transreg.cpp tridpars.cpp 
	unesctrn.cpp uni2name.cpp utrans.cpp csdetect.cpp csmatch.cpp csr2022.cpp csrecog.cpp csrmbcs.cpp csrsbcs.cpp 
	csrucode.cpp csrutf8.cpp inputext.cpp ucsdet.cpp uspoof.cpp uspoof_build.cpp uspoof_conf.cpp uspoof_impl.cpp 
	uspoof_wsconf.cpp unicode/alphaindex.h bocsu.h unicode/coleitr.h unicode/coll.h unicode/search.h 
	unicode/sortkey.h unicode/stsearch.h unicode/tblcoll.h unicode/ucol.h affixpatternparser.h 
	decimalformatpatternimpl.h decimfmtimpl.h digitaffix.h digitaffixesandpadding.h digitformatter.h digitgrouping.h 
	digitinterval.h pluralaffix.h precision.h significantdigitinterval.h smallintformatter.h valueformatter.h 
	visibledigits.h collation.h collationbuilder.h collationcompare.h collationdata.h collationdatabuilder.h 
	collationdatareader.h collationdatawriter.h collationfastlatin.h collationfastlatinbuilder.h collationfcd.h 
	collationiterator.h collationkeys.h collationroot.h collationrootelements.h collationruleparser.h collationsets.h 
	collationsettings.h collationtailoring.h collationweights.h dcfmtimp.h numsys_impl.h region_impl.h selfmtimpl.h 
	tzgnames.h tznames_impl.h ucol_imp.h unicode/ucoleitr.h unicode/usearch.h unicode/tzfmt.h unicode/tznames.h 
	uitercollationiterator.h unicode/region.h unicode/uregion.h usrchimp.h astro.h unicode/basictz.h buddhcal.h 
	unicode/calendar.h cecal.h chnsecal.h unicode/choicfmt.h unicode/compactdecimalformat.h coptccal.h 
	unicode/curramt.h currfmt.h unicode/currpinf.h unicode/currunit.h dangical.h unicode/datefmt.h unicode/dcfmtsym.h 
	decContext.h decfmtst.h decimalformatpattern.h unicode/decimfmt.h decNumber.h decNumberLocal.h digitlst.h 
	unicode/dtfmtsym.h dtitv_impl.h unicode/dtitvfmt.h unicode/dtitvinf.h unicode/dtptngen.h dtptngen_impl.h 
	unicode/dtrule.h ethpccal.h unicode/fieldpos.h unicode/fmtable.h unicode/uformattable.h unicode/format.h 
	fphdlimp.h unicode/fpositer.h unicode/gender.h unicode/ugender.h unicode/gregocal.h gregoimp.h hebrwcal.h 
	indiancal.h islamcal.h japancal.h unicode/locdspnm.h unicode/measfmt.h unicode/measunit.h unicode/measure.h 
	unicode/msgfmt.h msgfmt_impl.h nfrlist.h nfrs.h nfrule.h nfsubs.h unicode/numfmt.h unicode/numsys.h olsontz.h 
	persncal.h unicode/plurfmt.h unicode/plurrule.h plurrule_impl.h quantityformatter.h sharedbreakiterator.h 
	sharedcalendar.h shareddateformatsymbols.h sharednumberformat.h sharedpluralrules.h unicode/rbnf.h unicode/rbtz.h 
	unicode/reldatefmt.h reldtfmt.h unicode/scientificnumberformatter.h unicode/selfmt.h unicode/simpletz.h 
	unicode/smpdtfmt.h smpdtfst.h taiwncal.h unicode/timezone.h unicode/tmunit.h unicode/tmutamt.h unicode/tmutfmt.h 
	unicode/tzrule.h unicode/tztrans.h unicode/ucal.h unicode/ucurr.h ucurrimp.h unicode/udat.h 
	unicode/udateintervalformat.h unicode/udatpg.h unicode/udisplaycontext.h unicode/ufieldpositer.h 
	unicode/uldnames.h unicode/ulocdata.h unicode/umsg.h umsg_imp.h unicode/unum.h unicode/unumsys.h 
	unicode/upluralrules.h unicode/utmscale.h unicode/vtzone.h utf16collationiterator.h utf8collationiterator.h 
	vzone.h windtfmt.h winnmfmt.h wintzimpl.h zonemeta.h zrule.h ztrans.h ucln_in.h unicode/regex.h regexcmp.h 
	regexcst.h regeximp.h regexst.h regextxt.h unicode/uregex.h anytrans.h brktrans.h casetrn.h cpdtrans.h esctrn.h 
	funcrepl.h name2uni.h nortrans.h nultrans.h quant.h rbt.h rbt_data.h rbt_pars.h rbt_rule.h rbt_set.h remtrans.h 
	strmatch.h strrepl.h titletrn.h tolowtrn.h toupptrn.h unicode/translit.h transreg.h tridpars.h unesctrn.h 
	uni2name.h unicode/unirepl.h unicode/utrans.h csdetect.h csmatch.h csr2022.h csrecog.h csrmbcs.h csrsbcs.h 
	csrucode.h csrutf8.h inputext.h unicode/ucsdet.h unicode/uspoof.h identifier_info.h scriptset.h uspoof_conf.h 
	uspoof_impl.h uspoof_wsconf.h )
	
foreach(e ${SRCS})
	set(ICUIN_SRCS "${ICUIN_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

add_definitions("-DU_I18N_IMPLEMENTATION")
include_directories(${COMMON_INCLUDE_DIR})

if(BUILD_SHARED)
	add_library(icuin SHARED ${ICUIN_SRCS})
	target_link_libraries(icuin icuuc)
	set_target_properties(icuin PROPERTIES OUTPUT_NAME "icuin${ICU_VERSION_MAJOR}")
	install(TARGETS icuin RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
if(BUILD_STATIC)
	add_library(sicuin ${ICUIN_SRCS})
	set_target_properties(sicuin PROPERTIES COMPILE_DEFINITIONS "U_STATIC_IMPLEMENTATION")
	set_target_properties(sicuin PROPERTIES OUTPUT_NAME "sicuin${ICU_VERSION_MAJOR}")
	target_link_libraries(sicuin sicuuc)
	install(TARGETS sicuin RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
