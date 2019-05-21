cmake_minimum_required (VERSION 3.10)
project (cursordriver)

add_library(easybmp
    src/EasyBMP.cpp
)

add_executable(sample
    sample/EasyBMPsample.cpp
)

set_target_properties(easybmp PROPERTIES ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/lib)
set_target_properties(sample PROPERTIES RUNTIME_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/bin)

target_include_directories(sample
    PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}/src
)
target_link_libraries(sample
    PRIVATE
        ${CMAKE_CURRENT_LIST_DIR}/lib/easybmp.lib
)

add_custom_command(
    TARGET sample POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        ${CMAKE_CURRENT_LIST_DIR}/sample/EasyBMPbackground.bmp
        ${CMAKE_CURRENT_LIST_DIR}/bin/EasyBMPbackground.bmp)

add_custom_command(
    TARGET sample POST_BUILD
    COMMAND ${CMAKE_COMMAND} -E copy
        ${CMAKE_CURRENT_LIST_DIR}/sample/EasyBMPtext.bmp
        ${CMAKE_CURRENT_LIST_DIR}/bin/EasyBMPtext.bmp)

set_property(TARGET easybmp PROPERTY CXX_STANDARD 17)
set_property(TARGET sample PROPERTY CXX_STANDARD 17)

if(MSVC)
    # Force MSVC standards conformance mode to detect non-portable code
    add_compile_options(/permissive-)
    add_definitions(/D_CRT_SECURE_NO_WARNINGS /D_CRT_NONSTDC_NO_WARNINGS)
endif()
