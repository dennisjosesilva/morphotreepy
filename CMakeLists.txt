cmake_minimum_required(VERSION 3.20)

project(morphotreepy)

include_directories("include")

set(CMAKE_CXX_STANDARD 14 CACHE STRING "C++ version selection")  # or 11, 14, 17, 20
set(CMAKE_CXX_STANDARD_REQUIRED ON)  # optional, ensure standard is supported
set(CMAKE_CXX_EXTENSIONS OFF)  # optional, keep compiler extensionsn off


set(BUILD_MORPHOTREE_SHARED ON)
add_subdirectory(morphotree/src)
add_subdirectory(pybind11)

# Setting up morphotree library

#if("${CMAKE_CXX_COMPILER_ID}" STREQUAL "Clang")
#    add_compile_options(-Wnoc++11-narrowing )
#endif()

pybind11_add_module(morphotreepy 
  src/pointpy.cpp  
  src/ctbuilderpy.cpp 
  src/mtreepy.cpp
  src/core/hqueuepy.cpp
  src/tree/treeOfShapes/kgridpy.cpp
  src/tree/treeOfShapes/order_imagepy.cpp
  src/tree/treeOfShapes/tospy.cpp 
  src/attributes/attributeComputerpy.cpp
  src/attributes/bitquads/quadCountComputerpy.cpp
  src/attributes/bitquads/quadCountTreeOfShapesComputerpy.cpp
  src/attributes/smoothnessContourComputerpy.cpp
  src/attributes/volumeComputerpy.cpp
  src/attributes/ExtinctionValuepy.cpp
  src/attributes/boundingBoxComputerpy.cpp
  src/attributes/numberOfDescendantsComputerpy.cpp
  src/attributes/topologicalHeightComputerpy.cpp
  src/attributes/differenceAttributeComputerpy.cpp
  src/filtering/globalOptimiser/globalOptimiserspy.cpp
  src/filtering/lexographicalFilterpy.cpp
  src/filtering/extinctionFilterpy.cpp
  src/filtering/treeFilterRulespy.cpp 
  src/filtering/progressiveDifferenceAttributeFilterpy.cpp
  src/module.cpp)
  
target_link_libraries(morphotreepy PRIVATE morphotree)