cmake_minimum_required (VERSION 3.0)
project(usd2glb)
include(${CMAKE_BINARY_DIR}/conanbuildinfo.cmake)
conan_basic_setup()

set (SOURCES
crc64/crc64.cpp
main.cpp
Image.h
)

set (INCLUDE_DIR
${CONAN_INCLUDE_DIRS_TINYUSDZ}/tinyusdz
${CONAN_INCLUDE_DIRS_TINYUSDZ}/tinyusdz/external
${CONAN_INCLUDE_DIRS_TINYUSDZ}/tinyusdz/external/jsonhpp/nlohmann
glm/glm
crc64
.
)

set(CMAKE_CXX_STANDARD 17)
if (WIN32) 
set (DEFINES  ${DEFINES}
-D"_CRT_SECURE_NO_DEPRECATE"  
-D"_SCL_SECURE_NO_DEPRECATE" 
-D"_CRT_SECURE_NO_WARNINGS"
)
else()
add_compile_options(-fPIC)
endif()

include_directories(${INCLUDE_DIR})
add_definitions(${DEFINES})
add_executable(usd2glb ${SOURCES})
target_link_libraries(usd2glb ${CONAN_LIBS}) 

