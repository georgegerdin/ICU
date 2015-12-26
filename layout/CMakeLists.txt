# Required modules
include(GNUInstallDirs)
include(CheckIncludeFiles)

set(SRCS AlternateSubstSubtables.cpp AnchorTables.cpp 
	ArabicLayoutEngine.cpp ArabicShaping.cpp CanonData.cpp 
	CanonShaping.cpp ClassDefinitionTables.cpp 
	ContextualGlyphInsertionProc2.cpp 
	ContextualGlyphSubstProc.cpp ContextualGlyphSubstProc2.cpp 
	ContextualSubstSubtables.cpp CoverageTables.cpp 
	CursiveAttachmentSubtables.cpp DeviceTables.cpp 
	ExtensionSubtables.cpp Features.cpp GDEFMarkFilter.cpp 
	GlyphDefinitionTables.cpp GlyphIterator.cpp 
	GlyphLookupTables.cpp GlyphPositionAdjustments.cpp 
	GlyphPositioningTables.cpp GlyphPosnLookupProc.cpp 
	GlyphSubstitutionTables.cpp GlyphSubstLookupProc.cpp 
	GXLayoutEngine.cpp GXLayoutEngine2.cpp HangulLayoutEngine.cpp 
	HanLayoutEngine.cpp IndicClassTables.cpp 
	IndicLayoutEngine.cpp IndicRearrangementProcessor.cpp 
	IndicRearrangementProcessor2.cpp IndicReordering.cpp 
	KernTable.cpp KhmerLayoutEngine.cpp KhmerReordering.cpp 
	LayoutEngine.cpp LEFontInstance.cpp LEGlyphStorage.cpp 
	LEInsertionList.cpp LigatureSubstProc.cpp 
	LigatureSubstProc2.cpp LigatureSubstSubtables.cpp 
	loengine.cpp LookupProcessor.cpp Lookups.cpp LookupTables.cpp 
	MarkArrays.cpp MarkToBasePosnSubtables.cpp 
	MarkToLigaturePosnSubtables.cpp MarkToMarkPosnSubtables.cpp 
	MirroredCharData.cpp MorphTables.cpp MorphTables2.cpp 
	MPreFixups.cpp MultipleSubstSubtables.cpp 
	NonContextualGlyphSubstProc.cpp 
	NonContextualGlyphSubstProc2.cpp OpenTypeLayoutEngine.cpp 
	OpenTypeUtilities.cpp PairPositioningSubtables.cpp 
	ScriptAndLanguage.cpp ScriptAndLanguageTags.cpp 
	SegmentArrayProcessor.cpp SegmentArrayProcessor2.cpp 
	SegmentSingleProcessor.cpp SegmentSingleProcessor2.cpp 
	ShapingTypeData.cpp SimpleArrayProcessor.cpp 
	SimpleArrayProcessor2.cpp SinglePositioningSubtables.cpp 
	SingleSubstitutionSubtables.cpp SingleTableProcessor.cpp 
	SingleTableProcessor2.cpp StateTableProcessor.cpp 
	StateTableProcessor2.cpp SubstitutionLookups.cpp 
	SubtableProcessor.cpp SubtableProcessor2.cpp 
	ThaiLayoutEngine.cpp ThaiShaping.cpp ThaiStateTables.cpp 
	TibetanLayoutEngine.cpp TibetanReordering.cpp 
	TrimmedArrayProcessor.cpp TrimmedArrayProcessor2.cpp 
	ValueRecords.cpp AlternateSubstSubtables.h AnchorTables.h 
	ArabicLayoutEngine.h ArabicShaping.h 
	AttachmentPosnSubtables.h CanonShaping.h 
	CharSubstitutionFilter.h ClassDefinitionTables.h 
	ContextualGlyphInsertion.h ContextualGlyphInsertionProc2.h 
	ContextualGlyphSubstitution.h ContextualGlyphSubstProc.h 
	ContextualGlyphSubstProc2.h ContextualSubstSubtables.h 
	CoverageTables.h CursiveAttachmentSubtables.h 
	DefaultCharMapper.h DeviceTables.h ExtensionSubtables.h 
	GDEFMarkFilter.h GlyphDefinitionTables.h GlyphIterator.h 
	GlyphLookupTables.h GlyphPositionAdjustments.h 
	GlyphPositioningTables.h GlyphPosnLookupProc.h 
	GlyphSubstitutionTables.h GlyphSubstLookupProc.h 
	GXLayoutEngine.h GXLayoutEngine2.h HangulLayoutEngine.h 
	HanLayoutEngine.h ICUFeatures.h IndicLayoutEngine.h 
	IndicRearrangement.h IndicRearrangementProcessor.h 
	IndicRearrangementProcessor2.h IndicReordering.h KernTable.h 
	KhmerLayoutEngine.h KhmerReordering.h LayoutEngine.h 
	LayoutTables.h LEFontInstance.h LEGlyphFilter.h 
	LEGlyphStorage.h LEInsertionList.h LELanguages.h LEScripts.h 
	LESwaps.h LETypes.h LigatureSubstitution.h 
	LigatureSubstProc.h LigatureSubstProc2.h 
	LigatureSubstSubtables.h loengine.h LookupProcessor.h 
	Lookups.h LookupTables.h MarkArrays.h 
	MarkToBasePosnSubtables.h MarkToLigaturePosnSubtables.h 
	MarkToMarkPosnSubtables.h MorphStateTables.h MorphTables.h 
	MPreFixups.h MultipleSubstSubtables.h 
	NonContextualGlyphSubst.h NonContextualGlyphSubstProc.h 
	NonContextualGlyphSubstProc2.h OpenTypeLayoutEngine.h 
	OpenTypeTables.h OpenTypeUtilities.h 
	PairPositioningSubtables.h ScriptAndLanguage.h 
	ScriptAndLanguageTags.h SegmentArrayProcessor.h 
	SegmentArrayProcessor2.h SegmentSingleProcessor.h 
	SegmentSingleProcessor2.h SimpleArrayProcessor.h 
	SimpleArrayProcessor2.h SinglePositioningSubtables.h 
	SingleSubstitutionSubtables.h SingleTableProcessor.h 
	SingleTableProcessor2.h StateTableProcessor.h 
	StateTableProcessor2.h StateTables.h SubstitutionLookups.h 
	SubtableProcessor.h SubtableProcessor2.h ThaiLayoutEngine.h 
	ThaiShaping.h TibetanLayoutEngine.h TibetanReordering.h 
	TrimmedArrayProcessor.h TrimmedArrayProcessor2.h 
	ValueRecords.h )
	
foreach(e ${SRCS})
	set(LAYOUT_SRCS "${LAYOUT_SRCS}" "${CMAKE_CURRENT_LIST_DIR}/${e}")
endforeach()

add_definitions("-DU_LAYOUT_IMPLEMENTATION")
include_directories(${COMMON_INCLUDE_DIR} ${I18N_INCLUDE_DIR})

if(BUILD_SHARED)
	add_library(layout SHARED ${LAYOUT_SRCS})
	target_link_libraries(layout icuuc icuin)
	set_target_properties(layout PROPERTIES OUTPUT_NAME "icule${ICU_VERSION_MAJOR}")
	install(TARGETS layout RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()
if(BUILD_STATIC)
	add_library(slayout ${LAYOUT_SRCS})
	set_target_properties(slayout PROPERTIES OUTPUT_NAME "sicule${ICU_VERSION_MAJOR}")
	set_target_properties(slayout PROPERTIES COMPILE_DEFINITIONS "U_STATIC_IMPLEMENTATION")
	target_link_libraries(slayout sicuuc sicuin)
	install(TARGETS slayout RUNTIME DESTINATION ${CMAKE_INSTALL_BINDIR} LIBRARY DESTINATION ${CMAKE_INSTALL_LIBDIR} ARCHIVE DESTINATION ${CMAKE_INSTALL_LIBDIR} FRAMEWORK DESTINATION ${CMAKE_INSTALL_LIBDIR})
endif()