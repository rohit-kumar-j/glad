cmake_minimum_required(VERSION 3.5)
project(GLAD_PROJECT)

set(GLAD_HEADERS
	${CMAKE_CURRENT_SOURCE_DIR}/include/glad/glad.h
	${CMAKE_CURRENT_SOURCE_DIR}/include/KHR/khrplatform.h
)
set(GLAD_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/src/glad.c)

add_library(glad STATIC ${GLAD_SOURCES} ${GLAD_HEADERS})
target_include_directories(glad PUBLIC ${GLAD_HEADERS})

set_target_properties(glad PROPERTIES LINKER_LANGUAGE CXX)

install(TARGETS glad EXPORT glad DESTINATION lib)
install(FILES ${GLAD_HEADERS} DESTINATION include/glad)
