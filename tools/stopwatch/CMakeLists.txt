# Targets

    add_library(carlsim-stopwatch STATIC
        stopwatch.cpp
    )

# Properties

    # Since we build shared library enable position independent code
    set_property(TARGET carlsim-stopwatch PROPERTY
        POSITION_INDEPENDENT_CODE TRUE)

# Includes

    target_include_directories(carlsim-stopwatch
        PUBLIC
            .
    )

# Linking

    target_link_libraries(carlsim-stopwatch
        PRIVATE
            carlsim-interface
    )

# Installation

    install(FILES stopwatch.h DESTINATION include)
