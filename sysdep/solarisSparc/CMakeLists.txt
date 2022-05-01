foreach(input_file
	"${CMAKE_CURRENT_SOURCE_DIR}/GC.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/FPCATCH.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/FPHAND.c"
	"${CMAKE_CURRENT_SOURCE_DIR}/get_pointers.s"
	"${CMAKE_CURRENT_SOURCE_DIR}/flush.s"
	)
	get_filename_component(input_file_name ${input_file} NAME)
	add_custom_target(copy-${input_file_name}
		ALL
		DEPENDS
		"${CMAKE_SOURCE_DIR}/src/${NAME}"
	)
	add_custom_command(OUTPUT
		"${CMAKE_SOURCE_DIR}/src/${input_file_name}"
		COMMAND
		${CMAKE_COMMAND} -E copy "${input_file}" "${CMAKE_SOURCE_DIR}/src/${input_file_name}"
		DEPENDS
		"${input_file_name}"
	)
	add_dependencies(saclib_objects copy-${input_file_name})
endforeach()

add_custom_target(copy-sysdep
	ALL
	DEPENDS
	"${CMAKE_SOURCE_DIR}/include/sysdep.h"
)
add_custom_command(OUTPUT
	"${CMAKE_SOURCE_DIR}/include/sysdep.h"
	COMMAND
	${CMAKE_COMMAND} -E copy "${CMAKE_CURRENT_SOURCE_DIR}/sysdep.h" "${CMAKE_SOURCE_DIR}/include/sysdep.h"
	DEPENDS
	"${CMAKE_CURRENT_SOURCE_DIR}/sysdep.h"
)

add_dependencies(saclib_objects copy-GC copy-sysdep)
