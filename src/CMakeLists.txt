

file (GLOB_RECURSE HEADER_LIST ${PROJECT_SOURCE_DIR}/include/*.hpp)
file (GLOB SOURCE_LIST ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

### SHARED ###
add_library (&{root} SHARED ${SOURCE_LIST} ${HEADER_LIST})




target_compile_definitions (&{root}
  PRIVATE   
    $<$<CONFIG:Debug>:Debug>
    $<$<CONFIG:Release>:Release>
  INTERFACE
    $<INSTALL_INTERFACE:USING_&{root}>
)

target_include_directories (&{root} PUBLIC ${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})


target_include_directories(&{root}
    PUBLIC
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>

    PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/&{root}>
        $<INSTALL_INTERFACE:include/&{root}>
)



ph_precompile (TARGET &{root} PRIVATE PCH ${std_pch})








