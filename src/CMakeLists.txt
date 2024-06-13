# Copyright (c) 2020-2021, AthenaPK Collaboration. All rights reserved.
# Licensed under the 3-Clause License (the "LICENSE");

# Set up the AresPK library
# For first commit, we use version 1.0.0
project(ares_lib VERSION 1.0.0 DESCRIPTION "Physics Packages in Ares")

add_library(ares_lib STATIC 
                     hydro/hydro.cpp
                     network/network.cpp
                     pgen/blast.cpp      
                     pgen/gas_sphere.cpp  
                     pgen/linear_wave.cpp  
                     pgen/sod.cpp
                     pgen/burn_tube.cpp  
                     pgen/kh.cpp          
                     pgen/rt.cpp           
                     pgen/white_dwarf.cpp
                     refinement/gradient.cpp
                     refinement/other.cpp
                     utils/utils.cpp)
set_target_properties(ares_lib PROPERTIES VERSION ${PROJECT_VERSION})
target_link_libraries(ares_lib PRIVATE parthenon)
target_link_libraries(ares_lib PRIVATE plog)
target_link_libraries(ares_lib PRIVATE singularity-eos)

add_executable(
    ares
        main.cpp
        ares_driver.cpp
)

add_subdirectory(pgen)

target_link_libraries(ares PRIVATE plog)
target_link_libraries(ares PRIVATE parthenon)
target_link_libraries(ares PRIVATE singularity-eos)
target_link_libraries(ares PUBLIC ares_lib)
