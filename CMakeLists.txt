cmake_minimum_required (VERSION 3.8)
project(glad CXX)

set(HEADER_FILES 
	${CMAKE_CURRENT_SOURCE_DIR}/include/glad/glad.h 
	${CMAKE_CURRENT_SOURCE_DIR}/include/KHR/khrplatform.h)

add_library(glad STATIC 
	${CMAKE_CURRENT_SOURCE_DIR}/src/glad.c
	${HEADER_FILES}
)

target_include_directories(glad PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)

install(TARGETS glad EXPORT glad DESTINATION lib)
install(FILES ${HEADER_FILES} DESTINATION include/glad)
