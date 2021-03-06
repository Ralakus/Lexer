cmake_minimum_required(VERSION 3.1..3.12)

if(${CMAKE_VERSION} VERSION_LESS 3.12)

    cmake_policy(VERSION ${CMAKE_MAJOR_VERSION}.${CMAKE_MINOR_VERSION})

endif()

project(CodeNameOne VERSION 0.1.0
                    DESCRIPTION "A part of the CodeNameOne library"
                    LANGUAGES C)

include_directories(
    ${PROJECT_SOURCE_DIR}/src
)

file(GLOB_RECURSE all_c_src
    "${PROJECT_SOURCE_DIR}/src/*.c"
)

add_executable(CDOLexer ${all_c_src})
set_property(TARGET CDOLexer PROPERTY C_STANDARD 11)

add_subdirectory(lib/LabyrinthLexer)
target_include_directories(CDOLexer PUBLIC lib/LabyrinthLexer/src)
target_link_libraries(CDOLexer PUBLIC LabLexer)

if(CMAKE_SIZEOF_VOID_P EQUAL 8)     # 64 bit

    target_compile_definitions(CDOLexer PUBLIC CDO_64_BIT)

elseif(CMAKE_SIZEOF_VOID_P EQUAL 4) # 32 bit

    target_compile_definitions(CDOLexer PUBLIC CDO_32_BIT)

endif()