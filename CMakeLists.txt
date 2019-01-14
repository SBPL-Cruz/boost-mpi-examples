cmake_minimum_required(VERSION 2.8)
project(boost_mpi_examples)

set(CMAKE_CXX_FLAGS "${CMAKE_CXX_FLAGS} -std=c++11")

set(examples
        example1-setup
        example2-synccomm
        example3-asynccomm
        example4-broadcast
        example5-gather
        example6-reduce
        example7-reduce
        example8-allreduce
        example9-allreduce
        example10-communicator
        example11-skeleton
        example12-datatype
)

#set(utils_src
#
#)

foreach(example ${examples})
    list(APPEND ${example}_src ${example}.cpp)
    add_executable(${example}
            ${${example}_src}
#            ${utils_src}
    )
endforeach()

set (BOOST_ROOT "/media/aditya/A69AFABA9AFA85D9/Cruzr/code/boost_1_67_0_perch/install")
set (BOOSTROOT "/media/aditya/A69AFABA9AFA85D9/Cruzr/code/boost_1_67_0_perch/install")
set (Boost_INCLUDE_DIR "/media/aditya/A69AFABA9AFA85D9/Cruzr/code/boost_1_67_0_perch/install/include")
set (Boost_LIBRARY_DIR "/media/aditya/A69AFABA9AFA85D9/Cruzr/code/boost_1_67_0_perch/install/lib")
set (Boost_NO_SYSTEM_PATHS ON)
set(Boost_USE_STATIC_LIBS OFF)
set(Boost_USE_MULTITHREADED ON)
set(Boost_USE_STATIC_RUNTIME OFF)
#find_package(Boost 1.67.0 REQUIRED mpi serialization system)
include_directories(${Boost_INCLUDE_DIRS})
set( Boost_LIBRARIES
        ${Boost_LIBRARY_DIR}/libboost_serialization.a
        ${Boost_LIBRARY_DIR}/libboost_mpi.a)

foreach(example ${examples})
    target_link_libraries(${example} ${Boost_LIBRARIES})
endforeach()

#set (MPI_ROOT "/media/aditya/A69AFABA9AFA85D9/Cruzr/code/openmpi-4.0.0/install")
#set (MPI_NO_SYSTEM_PATHS ON)
#find_package(MPI REQUIRED)
#include_directories(${MPI_CXX_INCLUDE_PATH})

include_directories("/media/aditya/A69AFABA9AFA85D9/Cruzr/code/openmpi-4.0.0/install/include/")
include(CMakeForceCompiler)

CMAKE_FORCE_CXX_COMPILER(/media/aditya/A69AFABA9AFA85D9/Cruzr/code/openmpi-4.0.0/install/bin/mpicxx ${CMAKE_CXX_COMPILER_ID})
#set(CMAKE_CXX_COMPILE_FLAGS ${CMAKE_CXX_COMPILE_FLAGS} ${MPI_COMPILE_FLAGS})
#set(CMAKE_CXX_LINK_FLAGS ${CMAKE_CXX_LINK_FLAGS} ${MPI_LINK_FLAGS})

# include_directories(${MPI_INCLUDE_PATH})
#foreach(example ${examples})
#    target_link_libraries(${example} ${MPI_CXX_LIBRARIES})
    #if(MPI_CXX_COMPILE_FLAGS)
    #  set_target_properties(${example} PROPERTIES COMPILE_FLAGS "${MPI_CXX_COMPILE_FLAGS}")
    #endif()
    #if(MPI_CXX_LINK_FLAGS)
    #  set_target_properties(${example} PROPERTIES LINK_FLAGS "${MPI_CXX_LINK_FLAGS}")
    #endif()
#endforeach()
