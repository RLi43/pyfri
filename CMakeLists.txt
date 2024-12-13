#########################################################################
## NOTE: Do not invoke this cmake yourself, use pip install . (see the ##
## README.md file).                                                    ##
#########################################################################

cmake_minimum_required(VERSION 3.16.3)

project(_pyfri)

include(FetchContent)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)
set(FRI_BUILD_EXAMPLES OFF)

add_subdirectory(fri)
find_package(pybind11 REQUIRED)
pybind11_add_module(_pyfri ${CMAKE_CURRENT_SOURCE_DIR}/pyfri/src/wrapper.cpp)

target_include_directories(
    _pyfri
    PRIVATE
    ${CMAKE_CURRENT_SOURCE_DIR}/pyfri/src
)

target_link_libraries(_pyfri PRIVATE FRIClient)
