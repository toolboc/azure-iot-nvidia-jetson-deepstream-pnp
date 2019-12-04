#Copyright (c) Microsoft. All rights reserved.
#Licensed under the MIT license. See LICENSE file in the project root for full license information.

#this is CMakeLists.txt for nvidia-jetson-dcs

#Compile As C99
if (CMAKE_VERSION VERSION_LESS "3.1")
    if (CMAKE_C_COMPILER_ID STREQUAL "GNU" OR CMAKE_C_COMPILER_ID STREQUAL "Clang")
        set (CMAKE_C_FLAGS "--std=c99 /DWIN32 /D_WINDOWS /W3")
        if (NOT IN_OPENWRT)
            set (CMAKE_CXX_FLAGS "--std=c++11 /DWIN32 /D_WINDOWS /W3 /GR /EHsc")
        endif()
    endif()
else()
    set (CMAKE_C_STANDARD 99)
    set (CMAKE_CXX_STANDARD 11)
endif()

cmake_minimum_required(VERSION 2.8)

set(nvidia-jetson-dcs_h_files
    ./utilities/deviceinfo_interface.h
    ./utilities/thermalzones_interface.h
    ./utilities/deepstream_interface.h
    ./utilities/digitaltwin_client_helper.h
    ./utilities/digitaltwin_serializer.h
    ./jetson_impl.h
    ./pnp_device.h
)

set(nvidia-jetson-dcs_c_files
    ./utilities/deviceinfo_interface.c
    ./utilities/thermalzones_interface.c
    ./utilities/deepstream_interface.c
    ./utilities/digitaltwin_client_helper.c
    ./utilities/digitaltwin_serializer.c
    ./jetson_impl.c
    ./pnp_device.c
    ./main.c
)

# Add source code from azure-iot-sdk-c as a subdirectory
#add_subdirectory(azure-iot-sdk-c)

include_directories(.)
include_directories(${azure_iot_sdks_SOURCE_DIR}/deps/parson ${MQTT_INC_FOLDER} ${SHARED_UTIL_INC_FOLDER} ${UMOCK_C_INC_FOLDER} ${MACRO_UTILS_INC_FOLDER} ${IOTHUB_CLIENT_INC_FOLDER} ${DIGITALTWIN_CLIENT_INC_FOLDER})

add_executable(nvidia-jetson-dcs ${nvidia-jetson-dcs_c_files} ${nvidia-jetson-dcs_h_files})

target_link_libraries(nvidia-jetson-dcs
parson
iothub_client_mqtt_transport
iothub_client
digitaltwin_client
prov_auth_client
aziotsharedutil
umqtt
)