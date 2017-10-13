# Targets

    add_library(carlsim-kernel
        src/print_snn_info.cpp
        src/snn_cpu_module.cpp
        src/snn_manager.cpp
        src/spike_buffer.cpp
    )

# Properties

    # Since we build shared library enable position independent code
    set_property(TARGET carlsim-kernel PROPERTY
        POSITION_INDEPENDENT_CODE TRUE)

# Definitions

    if(CARLSIM_NO_CUDA)
        target_compile_definitions(carlsim-kernel
            PUBLIC
                -D__NO_CUDA__
        )
    endif()

# Includes

    target_include_directories(carlsim-kernel
        PUBLIC
            inc
    )

# Linking

    if(UNIX)
        target_link_libraries(carlsim-kernel
            PRIVATE
                pthread
        )
    endif()

    if(NOT CARLSIM_NO_CUDA)
        target_link_libraries(carlsim-kernel
            PUBLIC
                carlsim-kernel-cuda
        )
    endif()

# Installation

    install(
        FILES
            inc/cuda_version_control.h
            inc/error_code.h
            inc/snn_datastructures.h
            inc/snn_definitions.h
            inc/snn.h
            inc/spike_buffer.h
        DESTINATION include)

# Subdirectories

    if(NOT CARLSIM_NO_CUDA)
        set(CARLSIM_KERNEL_INCLUDE_DIR "${CMAKE_CURRENT_LIST_DIR}/inc")
        add_subdirectory(src/gpu_module)
    endif()
