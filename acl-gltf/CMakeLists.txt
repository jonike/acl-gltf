cmake_minimum_required (VERSION 3.2)
project(acl-gltf CXX)

set(CMAKE_CXX_STANDARD 11)

include_directories("${PROJECT_SOURCE_DIR}/../external/acl/includes")
include_directories("${PROJECT_SOURCE_DIR}/../external/acl/external/rtm/includes")
include_directories("${PROJECT_SOURCE_DIR}/../external/tinygltf")

# Grab all of our source files
file(GLOB_RECURSE ALL_MAIN_SOURCE_FILES LIST_DIRECTORIES false
	${PROJECT_SOURCE_DIR}/sources/*.cpp
	${PROJECT_SOURCE_DIR}/sources/*.h)

# Add every natvis file
file(GLOB_RECURSE NATVIS_FILES LIST_DIRECTORIES false
	${PROJECT_SOURCE_DIR}/../*.natvis)

create_source_groups("${ALL_MAIN_SOURCE_FILES}" ${PROJECT_SOURCE_DIR})

add_executable(${PROJECT_NAME} ${ALL_TEST_SOURCE_FILES} ${ALL_MAIN_SOURCE_FILES} ${NATVIS_FILES})

setup_default_compiler_flags(${PROJECT_NAME})

# Abort on failure, easier to debug issues this way
add_definitions(-DACL_ON_ASSERT_ABORT)
add_definitions(-DRTM_ON_ASSERT_ABORT)

install(TARGETS ${PROJECT_NAME} RUNTIME DESTINATION bin)
