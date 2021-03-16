add_executable (&{root}_test test.cpp)

ph_fetch (catch2)

target_link_libraries (&{root}_test PRIVATE &{root} Catch2::Catch2)

ph_precompile (TARGET &{root}_test 
  PUBLIC 
  PCH 
    ${std_pch} 
)

add_test (
    NAME test_shared
    COMMAND $<TARGET_FILE:&{root}>
)


add_test (
    NAME test 
    COMMAND $<TARGET_FILE:phime_test> --success
)










#cmake -Wno-dev -DCMAKE_CONFIGURATION_TYPES="Debug;Release;Kuk" -S . -B xbuild -GXcode && cmake --open xbuild