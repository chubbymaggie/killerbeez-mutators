cmake_minimum_required (VERSION 2.8.8)
project (mutators_repo)

SET ( BUILD_DIRECTORY ${CMAKE_SOURCE_DIR}/../build )

if (WIN32)
	SET( WINDOWS_BUILD_PATH ${BUILD_DIRECTORY}/${CMAKE_C_COMPILER_ARCHITECTURE_ID}/${CMAKE_BUILD_TYPE} )
	SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${WINDOWS_BUILD_PATH}/mutators/ )
	SET( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${WINDOWS_BUILD_PATH}/mutators/ )
	SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${WINDOWS_BUILD_PATH}/mutators/ )
	LINK_DIRECTORIES(${WINDOWS_BUILD_PATH}/killerbeez/)
	add_definitions(-D_CRT_SECURE_NO_WARNINGS -D_DEPRECATION_DISABLE -D_CRT_NONSTDC_NO_DEPRECATE -DUTILS_NO_IMPORT -DJANSSON_NO_IMPORT)
else (WIN32)
	SET( CMAKE_RUNTIME_OUTPUT_DIRECTORY ${BUILD_DIRECTORY}/mutators/ )
	SET( CMAKE_LIBRARY_OUTPUT_DIRECTORY ${BUILD_DIRECTORY}/mutators/ )
	SET( CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${BUILD_DIRECTORY}/mutators/ )
	LINK_DIRECTORIES(${BUILD_DIRECTORY}/killerbeez/)
endif (WIN32)

include_directories (${CMAKE_SOURCE_DIR}/../killerbeez-utils/jansson/)
include_directories (${CMAKE_SOURCE_DIR}/../killerbeez-utils/utils/)

add_subdirectory(${CMAKE_SOURCE_DIR}/../killerbeez-utils/ ${CMAKE_BINARY_DIR}/killerbeez-utils/)

# The general mutator library with the common functionality
add_subdirectory(mutators)

# The various mutators
add_subdirectory(afl_mutator)
add_subdirectory(bit_flip_mutator)
add_subdirectory(arithmetic_mutator)
add_subdirectory(dictionary_mutator)
add_subdirectory(havoc_mutator)
add_subdirectory(honggfuzz_mutator)
add_subdirectory(interesting_value_mutator)
add_subdirectory(manager_mutator)
add_subdirectory(ni_mutator)
add_subdirectory(nop_mutator)
add_subdirectory(splice_mutator)
add_subdirectory(radamsa_mutator)

# The mutator test program
add_subdirectory(mutator_tester)

