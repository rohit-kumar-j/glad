cmake_minimum_required(VERSION 3.5)
project(GLAD_PROJECT)

execute_process(COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/include/glad/glad.h ${CMAKE_CURRENT_SOURCE_DIR})
execute_process(COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/include/KHR/khrplatform.h ${CMAKE_CURRENT_SOURCE_DIR})
execute_process(COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/src/glad.c ${CMAKE_CURRENT_SOURCE_DIR})

set(GLAD_HEADERS
	${CMAKE_CURRENT_SOURCE_DIR}/glad.h
	${CMAKE_CURRENT_SOURCE_DIR}/khrplatform.h
)
set(GLAD_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/glad.c)

add_library(glad STATIC ${GLAD_SOURCES} ${GLAD_HEADERS})
target_include_directories(glad PUBLIC ${GLAD_HEADERS})

set_target_properties(glad PROPERTIES LINKER_LANGUAGE CXX)

install(TARGETS glad EXPORT glad DESTINATION lib)
install(FILES ${GLAD_HEADERS} DESTINATION include/glad)
install(FILES ${GLAD_SOURCES} DESTINATION include/glad)
