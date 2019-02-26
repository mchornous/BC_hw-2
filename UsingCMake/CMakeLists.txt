cmake_minimum_required(VERSION 3.0)
set(CMAKE_CXX_STANDARD 11)
set(CMAKE_BUILD_TYPE Release)
set(USE_LIB ON)
set(LIB_DIR build/lib)
#project(useCalculator)
set(PROJECT_NAME "useCalculator")
project(${PROJECT_NAME} VERSION 1.0.0 LANGUAGES CXX)
set(CMAKE_CXX_STANDARD 14)
set(CMAKE_CXX_STANDARD_REQUIRED TRUE)
set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -Wall -Wextra -Wpedantic -Wshadow -Wundef -Wno-missing-field-initializers")

include_directories(${CMAKE_CURRENT_SOURCE_DIR}/include)
message(ST1  "${CMAKE_CURRENT_SOURCE_DIR}")
#add_subdirectory (lib)


file(GLOB SOURCES "src/modules/*.cpp")
message(ST2  "${SOURCES}")




if(USE_LIB )#USE_LIB
	if(NOT EXISTS $(LIB_DIR) )
		file(MAKE_DIRECTORY ${LIB_DIR})
	endif()
	link_directories(lib)#${CMAKE_SOURCE_DIR}/
	set(PROJECT_LINK_LIBS libmyLibrary.so)
#	link_directories(${CMAKE_CURRENT_SOURCE_DIR}/${LIB_DIR})
	add_library(myLibrary SHARED ${SOURCES})

#	install(TARGETS "myLibrary" DESTINATION ${CMAKE_CURRENT_SOURCE_DIR}/${LIB_DIR})

#	add_custom_target(build-time-make-directory ALL   COMMAND ${CMAKE_COMMAND} -E make_directory( ${LIB_DIR}))

message(ST3Lib  "${SOURCES}")
message(ST4Lib  "${PROJECT_LINK_LIBS}")
	add_executable(${PROJECT_NAME} "src/useCalculator.cpp")
	target_link_libraries(useCalculator myLibrary) #${PROJECT_LINK_LIBS}
else()
message(ST3  "${SOURCES}")
	add_executable(${PROJECT_NAME} "src/useCalculator.cpp" ${SOURCES}) # 
endif()

#file(GLOB SOURCES "src/*.cpp")
#message(${SOURCES})
#add_executable(${PROJECT_NAME} ${SOURCES})


