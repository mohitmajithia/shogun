# add test case for each generated example
# (not generated yet so have to fake filenames from META_EXAMPLES list)
FOREACH(META_EXAMPLE ${META_EXAMPLES})
    # assume a structure <target_language>/<category>/listing.sg
    GET_META_EXAMPLE_VARS(${META_EXAMPLE} EXAMPLE_NAME EXAMPLE_REL_DIR EXAMPLE_NAME_WITH_DIR)
    
	add_test(NAME generated_r-${EXAMPLE_NAME_WITH_DIR}
			WORKING_DIRECTORY ${CMAKE_CURRENT_BINARY_DIR}/${EXAMPLE_REL_DIR}
			COMMAND ${R_EXECUTABLE} --no-restore --no-save --no-readline --slave -f ${CMAKE_CURRENT_BINARY_DIR}/${EXAMPLE_REL_DIR}/${EXAMPLE_NAME}.R)
ENDFOREACH()

# For now, the generated examples are not installed in the R library
# When the switch to the example generation is complete, the following lines may be uncommented
#install(FILES ${R_EXAMPLES}
#	DESTINATION ${R_COMPONENT_LIB_PATH}/shogun/demo
#	COMPONENT r)
