# Targets

    add_executable(benchmark4
        src/main_benchmark4.cpp
    )

# Linking

    target_link_libraries(benchmark4
        PUBLIC
            carlsim
    )
