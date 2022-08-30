cmake_minimum_required (VERSION 3.23)

if (POLICY CMP0074)
  cmake_policy(SET CMP0074 NEW)
endif ()

set(PROJECTNAME minercraft)
project(${PROJECTNAME})

set(CMAKE_C_COMPILER gcc)

link_directories(
	${CMAKE_CURRENT_SOURCE_DIR}/lib/
	${CMAKE_CURRENT_SOURCE_DIR}/lib/noise
)

file(GLOB_RECURSE DIR_SRCS
	${PROJECT_SOURCE_DIR}/src/*.c
	${PROJECT_SOURCE_DIR}/src/block/*.c
	${PROJECT_SOURCE_DIR}/src/entity/*.c
	${PROJECT_SOURCE_DIR}/src/gfx/*.c
	${PROJECT_SOURCE_DIR}/src/ui/*.c
	${PROJECT_SOURCE_DIR}/src/util/*.c
	${PROJECT_SOURCE_DIR}/src/world/*.c
	${PROJECT_SOURCE_DIR}/src/world/gen/*.c
)

add_executable(${PROJECTNAME} ${DIR_SRCS})

# message(STATUS ${PROJECT_SOURCE_DIR})
# include header path
target_include_directories(${PROJECTNAME} PUBLIC
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/src/>
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/lib/>
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/lib/cglm/include/>
    $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/lib/noise/>
)

# Link libs
target_link_libraries(${PROJECTNAME} -lglfw)
target_link_libraries(${PROJECTNAME} -lpthread)
target_link_libraries(${PROJECTNAME} -ldl)
target_link_libraries(${PROJECTNAME} -lGL)
target_link_libraries(${PROJECTNAME} -lm)
target_link_libraries(${PROJECTNAME} -lnoise)
