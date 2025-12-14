# vivid-ml Tests
# Unit tests for ML operators

cmake_minimum_required(VERSION 3.16)

# Fetch Catch2 v3
include(FetchContent)
FetchContent_Declare(
    Catch2
    GIT_REPOSITORY https://github.com/catchorg/Catch2.git
    GIT_TAG v3.4.0
)
FetchContent_MakeAvailable(Catch2)

# Include Catch2's CMake helpers
list(APPEND CMAKE_MODULE_PATH ${catch2_SOURCE_DIR}/extras)
include(CTest)
include(Catch)

# -----------------------------------------------------------------------------
# Unit Tests
# -----------------------------------------------------------------------------

add_executable(test_vivid_ml
    test_tensor.cpp
    test_pose_detector.cpp
)

target_link_libraries(test_vivid_ml PRIVATE
    Catch2::Catch2WithMain
    vivid-ml
)

target_include_directories(test_vivid_ml PRIVATE
    ${CMAKE_SOURCE_DIR}/include
)

catch_discover_tests(test_vivid_ml)
