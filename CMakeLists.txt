cmake_minimum_required (VERSION 3.10)
project (cursordriver)

#set(CMAKE_MODULE_PATH ${CMAKE_MODULE_PATH} ${CMAKE_CURRENT_LIST_DIR}/cmake)

add_library(easybmp
    src/EasyBmp.cpp
)

set_target_properties(easybmp PROPERTIES ARCHIVE_OUTPUT_DIRECTORY ${CMAKE_CURRENT_LIST_DIR}/lib)

set_property(TARGET easybmp PROPERTY CXX_STANDARD 17)

if(MSVC)
    # Force MSVC standards conformance mode to detect non-portable code
    add_compile_options(/permissive-)
    add_definitions(/D_CRT_SECURE_NO_WARNINGS /D_CRT_NONSTDC_NO_WARNINGS)
endif()
