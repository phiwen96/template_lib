

file (GLOB_RECURSE HEADER_LIST ${PROJECT_SOURCE_DIR}/include/*.hpp)
file (GLOB SOURCE_LIST ${CMAKE_CURRENT_SOURCE_DIR}/*.cpp)

### SHARED ###
add_library (phime SHARED ${SOURCE_LIST} ${HEADER_LIST})




target_compile_definitions (phime
  PRIVATE   
    $<$<CONFIG:Debug>:Debug>
    $<$<CONFIG:Release>:Release>
  INTERFACE
    $<INSTALL_INTERFACE:USING_phime>
)

target_include_directories (phime PUBLIC ${CMAKE_CURRENT_BINARY_DIR} ${CMAKE_CURRENT_SOURCE_DIR})


target_include_directories(phime
    PUBLIC
        $<BUILD_INTERFACE:${PROJECT_SOURCE_DIR}/include>
        $<INSTALL_INTERFACE:include>

    PRIVATE
        $<BUILD_INTERFACE:${CMAKE_CURRENT_SOURCE_DIR}/include/phime>
        $<INSTALL_INTERFACE:include/phime>
)



ph_precompile (TARGET phime PRIVATE PCH ${std_pch})








