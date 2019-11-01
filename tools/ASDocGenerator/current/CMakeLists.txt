cmake_minimum_required(VERSION 2.8)

project(ASDocGenerator)

set(SOURCE_FILES 
	src/CDocGenerator.h					src/CDocGenerator.cpp
	src/utility/CEscapeSequences.h		src/utility/CEscapeSequences.cpp
	src/utility/CString.h				src/utility/CString.cpp
	src/utility/Logging.h				src/utility/Logging.cpp
	src/utility/Platform.h				src/utility/Platform.cpp
	src/utility/StringUtils.h			src/utility/StringUtils.cpp
	src/utility/Utility.h				src/utility/Utility.cpp
	src/utility/CMemory.h
	src/utility/Shareddefs.h
	src/keyvalues/CKeyvalue.h				src/keyvalues/CKeyvalue.cpp
	src/keyvalues/CKeyvalueBlock.h			src/keyvalues/CKeyvalueBlock.cpp
	src/keyvalues/CKeyvalueNode.h			src/keyvalues/CKeyvalueNode.cpp
	src/keyvalues/CKeyvaluesLexer.h			src/keyvalues/CKeyvaluesLexer.cpp
	src/keyvalues/CKeyvaluesParser.h		src/keyvalues/CKeyvaluesParser.cpp
	src/keyvalues/CKeyvaluesWriter.h		src/keyvalues/CKeyvaluesWriter.cpp
	src/keyvalues/Keyvalues.h
	src/keyvalues/KeyvaluesConstants.h
	src/keyvalues/KVForward.h
	src/html/CHTMLBody.h			src/html/CHTMLBody.cpp
	src/html/CHTMLComposite.h		src/html/CHTMLComposite.cpp
	src/html/CHTMLDocument.h		src/html/CHTMLDocument.cpp
	src/html/CHTMLElement.h			src/html/CHTMLElement.cpp
	src/html/CHTMLHeader.h			src/html/CHTMLHeader.cpp
	src/html/CHTMLShared.h			src/html/CHTMLShared.cpp
	src/html/IHTMLObject.h
	src/Main.cpp
)


if(MSVC)
	# compile using the static runtime
	set(CMAKE_CXX_FLAGS_RELEASE "${CMAKE_CXX_FLAGS_RELEASE} /MT")
	set(CMAKE_CXX_FLAGS_DEBUG "${CMAKE_CXX_FLAGS_DEBUG} /MTd")
	
	# disable some warnings
	set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} /wd4244 /wd4018 /wd4267 /wd4996")
	
elseif(CMAKE_CXX_COMPILER_ID STREQUAL "GNU" OR CMAKE_CXX_COMPILER_ID STREQUAL "Clang")
	set(CMAKE_CXX_FLAGS "-std=c++11 -Wall -Wno-unused -Wno-unused-result -Wno-sign-compare")
	set(CMAKE_CXX_FLAGS_DEBUG "-g -O0")
	set(CMAKE_CXX_FLAGS_RELEASE "-Os")
else()
	message(WARNING "Unknown compiler, no flags set")
endif()

include_directories(src)
include_directories(angelscript/angelscript/include)

add_executable(ASDocGenerator ${SOURCE_FILES})