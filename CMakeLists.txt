cmake_minimum_required( VERSION 2.6 )
set (PROJECT_NAME CommSerial)

project(${PROJECT_NAME})

set(HEADER_DIR ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}/include/)
set(SOURCE_DIR ${CMAKE_CURRENT_SOURCE_DIR}/${PROJECT_NAME}/src/)

include_directories(SYSTEM ${HEADER_DIR})

set(CS_HEADERS
	${HEADER_DIR}/Parser.h
	${HEADER_DIR}/Serial.h
	${HEADER_DIR}/WinSerial.h)
	
set(CS_SOURCES
	${SOURCE_DIR}/Parser.cpp
	${SOURCE_DIR}/Source.cpp
	${SOURCE_DIR}/WinSerial.cpp)
	
if (WIN32)
	if (${CMAKE_CXX_COMPILER_ID} STREQUAL "MSVC")
		add_definitions(-DPAUSE)
		source_group("Header" FILES ${CS_HEADERS})
		source_group("Source" FILES ${CS_SOURCES})
		set_property(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR} PROPERTY VS_STARTUP_PROJECT ${PROJECT_NAME})
	endif()
endif()

set(CS_GLOB
	${CS_HEADERS}
	${CS_SOURCES})

add_executable(${PROJECT_NAME} ${CS_GLOB})

set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD 11)
set_property(TARGET ${PROJECT_NAME} PROPERTY CXX_STANDARD_REQUIRED 11)