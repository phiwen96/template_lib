add_executable (phime_test test.cpp)

ph_fetch (catch2)

target_link_libraries (phime_test PRIVATE phime Catch2::Catch2)

ph_precompile (TARGET phime_test 
  PUBLIC 
  PCH 
    ${std_pch} 
)

add_test (
    NAME test_shared
    COMMAND $<TARGET_FILE:phime>
)


add_test (
    NAME test 
    COMMAND $<TARGET_FILE:phime_test> --success
)










#cmake -Wno-dev -DCMAKE_CONFIGURATION_TYPES="Debug;Release;Kuk" -S . -B xbuild -GXcode && cmake --open xbuild