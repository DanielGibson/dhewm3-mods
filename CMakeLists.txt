# this CMakeLists.txt is supposed to live in (dhewm3/) neo/mods/ and is supposed
# to be used (via add_subdirectory()) by neo/CMakeLists.txt
#
# it just adds all mod subdirectories, so they're built if something like
#   cmake -DMODS=ON /path/to/dhewm3/neo
# is used to create the makefiles

# all the source files used by mods (like from the SDK)
# src_game and src_d3xp are defined in neo/CMakeLists.txt
string(REPLACE "game/" "" src_game_mods "${src_game}")
string(REPLACE "d3xp/" "" src_d3xp_mods "${src_d3xp}")

# this macro wraps all the settings that need to be done per mod
macro(SETUP_MOD name srclist compile_defs)
	add_library(${name} SHARED ${srclist})
	set_target_properties(${name} PROPERTIES PREFIX "")

	# stuff used in #ifdef's in the code
	set_target_properties(${name} PROPERTIES COMPILE_DEFINITIONS ${compile_defs})

	# ${CMAKE_SOURCE_DIR} == neo/ - so #includes of idlib/ etc work properly
	# ${CMAKE_CURRENT_SOURCE_DIR} is the dir this is called from,
	# e.g. /path/to/dhewm3/neo/mods/dentonmod/
	set_target_properties(${name} PROPERTIES COMPILE_FLAGS "-I${CMAKE_SOURCE_DIR} -I${CMAKE_CURRENT_SOURCE_DIR}")
	set_target_properties(${name} PROPERTIES LINK_FLAGS "${ldflags}")
	set_target_properties(${name} PROPERTIES INSTALL_NAME_DIR "@executable_path")

	# library output dir = ../.. => the ${name}.so/dll/dylib will be next to
	# dhewm3 and base.so/dll/dylib when compiled from dhewm3
	# (without this it'd be mods/${name}/${name}.so and we don't want that)
	set_target_properties(${name} PROPERTIES LIBRARY_OUTPUT_DIRECTORY "../..")

	target_link_libraries(${name} idlib)

	if(NOT APPLE AND NOT WIN32)
		install(TARGETS ${name}
			RUNTIME DESTINATION "${bindir}"
			LIBRARY DESTINATION "${libdir}"
			ARCHIVE DESTINATION "${libdir}"
		)
	endif()
endmacro(SETUP_MOD)


# add all suitable subdirectories (that contain CMakeLists.txt)
# e.g. neo/mods/dentonmod/
file(GLOB children *)
foreach(child ${children})
	if(IS_DIRECTORY ${child} AND EXISTS ${child}/CMakeLists.txt)
		add_subdirectory(${child})
	endif()
endforeach()


