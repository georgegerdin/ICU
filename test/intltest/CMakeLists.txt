set( SRCS bytestrietest.cpp collationtest.cpp colldata.cpp 
	numfmtspectest.cpp regiontst.cpp ucharstrietest.cpp 
	itrbbi.cpp rbbiapts.cpp rbbitst.cpp itspoof.cpp 
	allcoll.cpp alphaindextst.cpp apicoll.cpp currcoll.cpp 
	decoll.cpp encoll.cpp escoll.cpp ficoll.cpp frcoll.cpp 
	g7coll.cpp itercoll.cpp jacoll.cpp lcukocol.cpp 
	mnkytst.cpp regcoll.cpp srchtest.cpp ssearch.cpp 
	svccoll.cpp thcoll.cpp trcoll.cpp tscoll.cpp ucaconf.cpp 
	uvectest.cpp v32test.cpp simplethread.cpp strtest.cpp 
	tsmthred.cpp tsputil.cpp uobjtest.cpp astrotst.cpp 
	calcasts.cpp callimts.cpp calregts.cpp caltest.cpp 
	caltztst.cpp compactdecimalformattest.cpp dadrcal.cpp 
	dadrfmt.cpp datadrivennumberformattestsuite.cpp 
	dcfmapts.cpp dcfmtest.cpp dtfmapts.cpp dtfmrgts.cpp 
	dtfmtrtts.cpp dtfmttst.cpp dtifmtts.cpp dtptngts.cpp 
	fldset.cpp genderinfotest.cpp incaltst.cpp itformat.cpp 
	itrbnf.cpp itrbnfp.cpp itrbnfrt.cpp locnmtst.cpp 
	measfmttest.cpp miscdtfm.cpp msfmrgts.cpp nmfmapts.cpp 
	nmfmtrt.cpp numberformattesttuple.cpp 
	numberformat2test.cpp numfmtst.cpp numrgts.cpp 
	pluralmaptest.cpp plurfmts.cpp plurults.cpp pptest.cpp 
	quantityformattertest.cpp reldatefmttest.cpp 
	scientificnumberformattertest.cpp sdtfmtts.cpp 
	selfmts.cpp tchcfmt.cpp simplepatternformattertest.cpp 
	tfsmalls.cpp tmsgfmt.cpp tsdate.cpp tsdcfmsy.cpp 
	tsdtfmsy.cpp tsnmfmt.cpp tufmtts.cpp tzbdtest.cpp 
	tzfmttst.cpp tzoffloc.cpp tzregts.cpp tzrulets.cpp 
	tztest.cpp unifiedcachetest.cpp windttst.cpp winnmtst.cpp 
	idnaconf.cpp idnaref.cpp nptrans.cpp punyref.c 
	testidn.cpp testidna.cpp uts46test.cpp aliastst.cpp 
	loctest.cpp restest.cpp restsnew.cpp intltest.cpp 
	itmajor.cpp itutil.cpp testutil.cpp textfile.cpp 
	tokiter.cpp winutil.cpp canittst.cpp normconf.cpp 
	tstnorm.cpp tstnrapi.cpp ucdtest.cpp usettest.cpp 
	regextst.cpp icusvtst.cpp citrtest.cpp reptest.cpp 
	sfwdchit.cpp strcase.cpp ustrtest.cpp utxttest.cpp 
	cpdtrtst.cpp ittrans.cpp jamotest.cpp transapi.cpp 
	transrt.cpp transtst.cpp trnserr.cpp convtest.cpp 
	csdetest.cpp bidiconf.cpp listformattertest.cpp 
	colldata.h itrbbi.h rbbiapts.h rbbitst.h itspoof.h 
	allcoll.h alphaindextst.h apicoll.h currcoll.h decoll.h 
	encoll.h escoll.h ficoll.h frcoll.h g7coll.h itercoll.h 
	jacoll.h lcukocol.h mnkytst.h regcoll.h regiontst.h 
	srchtest.h ssearch.h svccoll.h thcoll.h trcoll.h tscoll.h 
	ucaconf.h uvectest.h v32test.h simplethread.h strtest.h 
	tsmthred.h tsputil.h uobjtest.h astrotst.h calcasts.h 
	callimts.h calregts.h caltest.h caltztst.h dadrcal.h 
	dadrfmt.h datadrivennumberformattestsuite.h dcfmapts.h 
	dcfmtest.h dtfmapts.h dtfmrgts.h dtfmtrtts.h dtfmttst.h 
	dtifmtts.h dtptngts.h fldset.h incaltst.h itformat.h 
	itrbnf.h itrbnfp.h itrbnfrt.h locnmtst.h miscdtfm.h 
	msfmrgts.h nmfmapts.h nmfmtrt.h numberformattesttuple.h 
	numfmtst.h numrgts.h plurfmts.h plurults.h pptest.h 
	sdtfmtts.h selfmts.h tchcfmt.h tfsmalls.h tmsgfmt.h 
	tsdate.h tsdcfmsy.h tsdtfmsy.h tsnmfmt.h tufmtts.h 
	tzbdtest.h tzfmttst.h tzoffloc.h tzregts.h tzrulets.h 
	tztest.h windttst.h winnmtst.h idnaconf.h idnaref.h 
	nptrans.h punyref.h testidna.h aliastst.h loctest.h 
	restest.h restsnew.h intltest.h itmajor.h itutil.h 
	testutil.h textfile.h tokiter.h winutil.h canittst.h 
	normconf.h tstnorm.h ucdtest.h usettest.h regextst.h 
	icusvtst.h citrtest.h reptest.h sfwdchit.h ustrtest.h 
	utxttest.h cpdtrtst.h ittrans.h jamotest.h transapi.h 
	transrt.h transtst.h trnserr.h convtest.h csdetest.h 
	listformattertest.h )
	
foreach(e ${SRCS})
	set(INTLTEST_SRCS "${INTLTEST_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

set(INTLTEST_SRCS ${INTLTEST_SRCS} PARENT_SCOPE)