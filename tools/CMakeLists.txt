add_subdirectory(genrb)
add_subdirectory(toolutil)
add_subdirectory(gennorm2)
add_subdirectory(gensprep)

set(GENBRK_SRCS ${CMAKE_CURRENT_LIST_DIR}/genbrk/genbrk.cpp PARENT_SCOPE)
set(GENCCODE_SRCS "${CMAKE_CURRENT_LIST_DIR}/geencode/genccode.c" PARENT_SCOPE)
set(GENCFU_SRCS ${CMAKE_CURRENT_LIST_DIR}/gencfu/gencfu.c PARENT_SCOPE)
set(GENCMN_SRCS ${CMAKE_CURRENT_LIST_DIR}/gencmn/gencmn.c PARENT_SCOPE)
set(GENCNVAL_SRCS ${CMAKE_CURRENT_LIST_DIR}/gencnval/gencnval.c PARENT_SCOPE)
set(GENDICT_SRCS ${CMAKE_CURRENT_LIST_DIR}/gendict/gendict.cpp PARENT_SCOPE)

set(DERB_SRCS ${DERB_SRCS} PARENT_SCOPE)
set(GENRB_SRCS ${GENRB_SRCS} PARENT_SCOPE)