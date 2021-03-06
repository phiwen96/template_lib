cmake_minimum_required (VERSION 3.19.4)

project (&{root}
	VERSION 1.0
	LANGUAGES CXX C
    DESCRIPTION "Very nice project"
)

add_subdirectory (cmake/phake)

if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
	set (CMAKE_CXX_STANDARD 20)
	set (CMAKE_CXX_STANDARD_REQUIRED ON)
    set (CMAKE_CXX_EXTENSIONS        ON)
	set_property (GLOBAL PROPERTY USE_FOLDERS YES)

    include (GNUInstallDirs)
    set (CMAKE_ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
    set (CMAKE_LIBRARY_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_LIBDIR})
    set (CMAKE_RUNTIME_OUTPUT_DIRECTORY ${CMAKE_BINARY_DIR}/${CMAKE_INSTALL_BINDIR})

    # Offer the user the choice of overriding the installation directories
    set (INSTALL_LIBDIR ${CMAKE_INSTALL_LIBDIR} CACHE PATH "Installation directory for libraries")
    set (INSTALL_BINDIR ${CMAKE_INSTALL_BINDIR} CACHE PATH "Installation directory for executables")
    set (INSTALL_INCLUDEDIR ${CMAKE_INSTALL_INCLUDEDIR} CACHE PATH "Installation directory for header files")

    if (WIN32 AND NOT CYGWIN)
        set (DEF_INSTALL_CMAKEDIR CMake)
    else ()
        set (DEF_INSTALL_CMAKEDIR share/cmake/${PROJECT_NAME})
    endif ()

    set (INSTALL_CMAKEDIR ${DEF_INSTALL_CMAKEDIR} CACHE PATH "Installation directory for CMake files")

    # Report to user
    foreach (p LIB BIN INCLUDE CMAKE)
        file (TO_NATIVE_PATH ${CMAKE_INSTALL_PREFIX}/${INSTALL_${p}DIR} _path )
        # message (STATUS "Installing ${p} components to ${_path}")
        unset (_path)
    endforeach ()
endif ()



add_subdirectory (src)
add_subdirectory (apps)


if (CMAKE_PROJECT_NAME STREQUAL PROJECT_NAME)
    include (CTest)
    enable_testing ()
    add_subdirectory (tests)
endif ()











