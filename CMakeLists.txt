cmake_minimum_required(VERSION 3.30)
project(LearnOpenGL
        LANGUAGES C CXX)

set(CMAKE_CXX_STANDARD 20)          # C++20
set(CMAKE_CXX_STANDARD_REQUIRED ON) # C++20 required

# ~/OpenGL-Base/dependencies/Library"
set(LIBRARY_DIR "${CMAKE_SOURCE_DIR}/dependencies/Library")

add_executable(LearnOpenGL
        src/glad.c
        src/main.cpp
)

# Add include path for dependencies
target_include_directories(LearnOpenGL PRIVATE
        "${CMAKE_SOURCE_DIR}/dependencies"
)

# Link GLFW static library depending on platform
if(WIN32)
    target_link_libraries(LearnOpenGL
            "${LIBRARY_DIR}/Windows/libglfw3.a"
            opengl32    # searches automatic for the opengl32.dll
    )
elseif(APPLE)
    target_link_libraries(LearnOpenGL
            "${LIBRARY_DIR}/MacOS/libglfw3.a"
            "-framework OpenGL"     # OpenGL.framework      - Provides OpenGL functions
            "-framework Cocoa"      # Cocoa.framework       - Manages the Window (GUI)
            "-framework IOKit"      # IOKit.framework       - Handles Input and peripheral devices
            "-framework CoreVideo"  # CoreVideo.framework   - Handles Display, VSync, and Video Timing
    )
endif()
