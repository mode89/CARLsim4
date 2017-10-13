# Dependencies

    find_package(CUDA REQUIRED)

# Includes

    set(CARLSIM_KERNEL_CUDA_INCLUDE_DIRS
        ${CARLSIM_KERNEL_INCLUDE_DIR}
        ${CUDA_INCLUDE_DIRS}
        ${CUDA_TOOLKIT_ROOT_DIR}/samples/common/inc
        ${CUDA_SAMPLES_INCLUDE_DIR}
    )

    cuda_include_directories(
        ${CARLSIM_KERNEL_CUDA_INCLUDE_DIRS}
    )

# Definitions

    set(CARLSIM_KERNEL_CUDA_COMPILE_DEFINITIONS
        -D__CUDA${CUDA_VERSION_MAJOR}__
    )

    add_definitions(
        ${CARLSIM_KERNEL_CUDA_COMPILE_DEFINITIONS}
    )

# Targets

    cuda_add_library(carlsim-kernel-cuda
        snn_gpu_module.cu
        OPTIONS
            -Xcompiler -fPIC
            -gencode arch=compute_30,code=sm_30
    )

# Target definitions

    target_compile_definitions(carlsim-kernel-cuda
        PUBLIC
            ${CARLSIM_KERNEL_CUDA_COMPILE_DEFINITIONS}
    )

# Target includes

    target_include_directories(carlsim-kernel-cuda
        PUBLIC
            ${CARLSIM_KERNEL_CUDA_INCLUDE_DIRS}
    )

# Linking

    target_link_libraries(carlsim-kernel-cuda
        ${CUDA_curand_LIBRARY}
    )
