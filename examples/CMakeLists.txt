cmake_minimum_required(VERSION 3.5)
project(raisim_examples LANGUAGES CXX)

#==
# Dependencies
#==

find_package(raisim CONFIG REQUIRED)
find_package(Eigen3 REQUIRED HINTS ${Eigen3_HINT})
include_directories ( ${EIGEN3_INCLUDE_DIRS} )

set(resource_directory ${CMAKE_CURRENT_SOURCE_DIR}/rsc/)

#==
# Build Targets
#==

function(create_executable app_name file_name)
    add_executable(${app_name} ${file_name})
    target_link_libraries(${app_name} PUBLIC raisim::raisim pthread)
    target_include_directories(${app_name} PUBLIC ${CMAKE_CURRENT_SOURCE_DIR}/include)
    target_compile_definitions(${app_name} PRIVATE "-DEXAMPLE_ROBOT_RESOURCE_DIR=${resource_directory}")
endfunction()

# benchmark examples
create_executable(anymal_speed_test src/benchmark/anymal.cpp)

# server examples
create_executable(primitives src/server/primitives.cpp)
create_executable(meshes src/server/meshes.cpp)
create_executable(anymal src/server/anymal.cpp)
create_executable(balls src/server/balls.cpp)
create_executable(atlas src/server/atlas.cpp)
create_executable(heightmap src/server/heightmap.cpp)
create_executable(hibernate src/server/hibernate.cpp)