cmake_minimum_required(VERSION 3.29)
project(sqlite3)

set(SRC_PATH "${CMAKE_CURRENT_SOURCE_DIR}")
set(SRCS
	"${SRC_PATH}/shell.c"
	"${SRC_PATH}/sqlite3.c"
)
file(GLOB_RECURSE HEADERS "${SRC_PATH}/*.h")
add_library(${PROJECT_NAME} SHARED "${SRCS}" "${HEADERS}")
target_compile_definitions(${PROJECT_NAME} PUBLIC "MGS_DEBUG=$<IF:$<CONFIG:Debug>,1,0>")
target_compile_options(${PROJECT_NAME} PUBLIC /std:c++20 /W4 /GA /GF /GR- /GS- /jumptablerdata /D_HAS_EXCEPTIONS=0 /Zi)
set_target_properties(${PROJECT_NAME} PROPERTIES MSVC_RUNTIME_LIBRARY "MultiThreaded$<$<CONFIG:Debug>:Debug>")
target_include_directories(${PROJECT_NAME} PUBLIC ${SRC_PATH})
