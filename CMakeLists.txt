cmake_minimum_required(VERSION 3.13)

# Initialize the SDK
include(pico_sdk_import.cmake)

# Set the project name
project(pico_rp_mts C CXX ASM)
set(CMAKE_C_STANDARD 11)
set(CMAKE_CXX_STANDARD 17)

# Initialize the SDK
pico_sdk_init()

add_executable(mts_fw)

# Find all source files in the src directory
file(GLOB_RECURSE SOURCES
    ${CMAKE_CURRENT_LIST_DIR}/src/*.cpp
    # ${CMAKE_CURRENT_LIST_DIR}/src/*.c
)

# Add the sources to the target
target_sources(mts_fw PUBLIC ${SOURCES})

# define which controller side is being compiled - LEFT_SIDE or RIGHT_SIDE
target_compile_definitions(mts_fw PRIVATE RIGHT_SIDE)

# Make sure TinyUSB can find tusb_config.h
target_include_directories(mts_fw PUBLIC
        ${CMAKE_CURRENT_LIST_DIR}/include)

# In addition to pico_stdlib required for common PicoSDK functionality, add dependency on tinyusb_device
# for TinyUSB device support and tinyusb_board for the additional board support library used by the example
target_link_libraries(mts_fw PUBLIC 
    pico_stdlib 
    # pico_unique_id 
    # tinyusb_device 
    # tinyusb_board 
    )

pico_add_extra_outputs(mts_fw)
