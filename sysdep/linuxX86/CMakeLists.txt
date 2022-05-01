add_custom_target(copy-GC
	ALL
	DEPENDS
	"${CMAKE_SOURCE_DIR}/src/GC.c"
)
add_custom_command(OUTPUT
	"${CMAKE_SOURCE_DIR}/src/GC.c"
	COMMAND
	${CMAKE_COMMAND} -E copy "${CMAKE_CURRENT_SOURCE_DIR}/GC.c" "${CMAKE_SOURCE_DIR}/src/GC.c"
	DEPENDS
	"${CMAKE_CURRENT_SOURCE_DIR}/GC.c"
)
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
