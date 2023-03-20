cmake_minimum_required(VERSION 3.5)
project(GLAD_PROJECT CXX)

include(FetchContent)
FetchContent_Declare(glfw GIT_REPOSITORY https://github.com/glfw/glfw)
FetchContent_GetProperties(glfw)

if(NOT glfw_POPULATED)
	FetchContent_Populate(glfw)
	add_subdirectory(${glfw_SOURCE_DIR} ${glfw_BINARY_DIR} EXCLUDE_FROM_ALL)
endif()

execute_process(COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/include/glad/glad.h ${CMAKE_CURRENT_SOURCE_DIR})
execute_process(COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/include/KHR/khrplatform.h ${CMAKE_CURRENT_SOURCE_DIR})
execute_process(COMMAND ${CMAKE_COMMAND} -E copy_if_different ${CMAKE_CURRENT_SOURCE_DIR}/src/glad.c ${CMAKE_CURRENT_SOURCE_DIR})

file(GLOB_RECURSE GLAD_HEADERS ${CMAKE_CURRENT_SOURCE_DIR}/*.h)
file(GLOB_RECURSE GLAD_SOURCES ${CMAKE_CURRENT_SOURCE_DIR}/*.c)

add_library(glad STATIC ${GLAD_SOURCES} ${GLAD_HEADERS})
target_include_directories(glad

	# PRIVATE
	# ${glfw_INCLUDEDIR}
	PUBLIC
		${GLAD_HEADERS}
)

# target_link_libraries(glad PRIVATE glfw)
set_target_properties(glad PROPERTIES LINKER_LANGUAGE CXX)
install(TARGETS glad EXPORT glad DESTINATION lib)
install(FILES ${GLAD_HEADERS} DESTINATION include/glad)
