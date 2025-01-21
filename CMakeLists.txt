# build with: (cd build; emcmake cmake .. && emmake make)
cmake_minimum_required(VERSION 3.29)

# Define Emscripten compiler
set(CMAKE_C_COMPILER emcc)
set(CMAKE_CXX_COMPILER em++)
set(CMAKE_CXX_STANDARD 20)

# set(CMAKE_SHARED_LIBRARY_SUFFIX ".js")
# add_link_options(
#         "-s WASM=1"
#         "-s EXPORTED_FUNCTIONS=["Compute"]"  # functions to export
#         "-s EXPORTED_RUNTIME_METHODS=['ccall', 'cwrap']"
#         "-s MODULARIZE=1"  # Encapsulate library in a module
#         -s EXPORT_NAME="GlideRatioComputer"  # Name of the exported module
#     )


project(glideRatio_wasm)

# Define source directory
set(SRC_DIR ${CMAKE_CURRENT_SOURCE_DIR}/src)
# Add the source directory to the include directories
include_directories(
    ${SRC_DIR} 
    ${SRC_DIR}/unix # For the Unix specific headers otherwise it will not compile
    ${SRC_DIR}/Engine # For the Engine specific headers otherwise it will not compile
    )

add_library(glideRatio_wasm SHARED
src/Computer/GlideRatioComputer.cpp )
