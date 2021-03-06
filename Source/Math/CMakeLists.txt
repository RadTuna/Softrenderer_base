cmake_minimum_required(VERSION 3.1)

project(Math)

################################################################################
# Source files
################################################################################
file(GLOB COMMON_FILES
       ${PROJECT_SOURCE_DIR}/*.cpp
       ${PROJECT_SOURCE_DIR}/*.h
       ${PROJECT_SOURCE_DIR}/*.hpp
)

set(ALL_FILES
    ${COMMON_FILES}
	)
	
foreach(FILE ${ALL_FILES})
    # make rel path
	file(RELATIVE_PATH REL_PATH "${PROJECT_SOURCE_DIR}" "${FILE}")
	set(ALL_FILES_REL ${ALL_FILES_REL} ${REL_PATH})
endforeach()	

set_source_files_properties(${ALL_FILES_REL} PROPERTIES HEADER_FILE_ONLY FALSE)

foreach(FILE ${ALL_FILES_REL})
    # get the base path
    get_filename_component(BASE_PATH "${FILE}" PATH)

    # changes /'s to \\'s
    string(REPLACE "/" "\\" GROUP "${BASE_PATH}")

    source_group("${GROUP}" FILES "${FILE}")
endforeach()

################################################################################
# Include directory
################################################################################
include_directories(
    ${PROJECT_SOURCE_DIR}
	)

################################################################################
# Library Output Setting
################################################################################
add_library(${PROJECT_NAME} STATIC ${ALL_FILES})

set_target_properties(${PROJECT_NAME} PROPERTIES
	PREFIX ""
	OUTPUT_NAME ${PROJECT_NAME}
	ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_SOURCE_DIR}/Output/Library
)
	

################################################################################
# Import Library
################################################################################
#target_link_libraries(${PROJECT_NAME} )


