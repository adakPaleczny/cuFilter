cmake_minimum_required(VERSION 3.12)

project(MyPointCloudProject)

# Find CUDA
find_package(CUDA REQUIRED)
include_directories(${CUDA_INCLUDE_DIRS})

# Find PCL
find_package(PCL REQUIRED)
include_directories(${PCL_INCLUDE_DIRS})
link_directories(${PCL_LIBRARY_DIRS})
add_definitions(${PCL_DEFINITIONS})


# Find Eigen
find_package(Eigen3 REQUIRED)
include_directories(${EIGEN3_INCLUDE_DIR})

include_directories(/usr/include/)
link_directories(/usr/lib/)

# Set the CUDA architecture, adjust according to your GPU
set(CUDA_NVCC_FLAGS ${CUDA_NVCC_FLAGS};-arch=sm_30)

# Set the source files
set(SOURCES main.cpp)

# Add the executable
add_executable(demo ${SOURCES})

# Link libraries
target_link_libraries(demo 
    ${CUDA_LIBRARIES} 
    ${PCL_LIBRARIES}
    ${EIGEN3_LIBRARIES}
    ${CMAKE_SOURCE_DIR}/lib/libcudafilter.so
)
