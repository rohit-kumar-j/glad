cmake_minimum_required(VERSION 3.5)
project(GLAD_PROJECT LANGUAGES CXX)

set(GLAD_HEADERS
	${CMAKE_CURRENT_SOURCE_DIR}/include/glad/glad.h
	${CMAKE_CURRENT_SOURCE_DIR}/include/KHR/khrplatform.h
)
set(GLAD_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/src/glad.c)

add_library(glad STATIC ${GLAD_SOURCES} ${GLAD_HEADERS})
target_include_directories(glad PUBLIC ${GLAD_HEADERS})

install(TARGETS glad EXPORT glad DESTINATION lib)
install(FILES ${GLAD_HEADERS} DESTINATION include/glad)
