cmake_minimum_required(VERSION 3.5)
project(GLAD_PROJECT CXX)

set(HEADER_FILES
	${CMAKE_CURRENT_SOURCE_DIR}/include/glad/glad.h
	${CMAKE_CURRENT_SOURCE_DIR}/include/KHR/khrplatform.h)

add_library(glad STATIC
	${CMAKE_CURRENT_SOURCE_DIR}/src/glad.c
)
target_include_directories(glad PUBLIC ${HEADER_FILES})

set_target_properties(glad PROPERTIES LINKER_LANGUAGE CXX)

install(TARGETS glad
		EXPORT glad
		CONFIGURATIONS Release
		LIBRARY DESTINATION lib
)
install(FILES ${HEADER_FILES} DESTINATION include/glad)
