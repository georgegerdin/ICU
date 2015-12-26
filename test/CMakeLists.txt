add_subdirectory(cintltst)
add_subdirectory(intltest)
add_subdirectory(iotest)
add_subdirectory(letest)

set(CINTLTST_SRCS ${CINTLTST_SRCS} PARENT_SCOPE)
set(INTLTEST_SRCS ${INTLTEST_SRCS} PARENT_SCOPE)
set(IOTEST_SRCS ${IOTEST_SRCS} PARENT_SCOPE)
set(LETEST_SRCS ${LETEST_SRCS} PARENT_SCOPE)