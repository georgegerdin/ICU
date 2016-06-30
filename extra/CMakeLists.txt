file(MAKE_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/../uconv_resources)
file(COPY
	${CMAKE_CURRENT_LIST_DIR}/uconv/resources/root.txt
	${CMAKE_CURRENT_LIST_DIR}/uconv/resources/fr.txt
	DESTINATION ${CMAKE_CURRENT_BINARY_DIR}/../uconv_resources/)
file(REMOVE ${CMAKE_CURRENT_BINARY_DIR}/../uconvpkgdatain.txt)
file(APPEND ${CMAKE_CURRENT_BINARY_DIR}/../uconvpkgdatain.txt "root.res\n")
file(APPEND ${CMAKE_CURRENT_BINARY_DIR}/../uconvpkgdatain.txt "fr.res\n")

	
set(UCONV_SRCS	"${CMAKE_CURRENT_LIST_DIR}/uconv/uconv.cpp"
				"${CMAKE_CURRENT_LIST_DIR}/uconv/uwmsg.c"
#				"${CMAKE_CURRENT_BINARY_DIR}/uconv_resources/root.res"
#				"${CMAKE_CURRENT_BINARY_DIR}/uconv_resources/fr.res"
				PARENT_SCOPE)
				