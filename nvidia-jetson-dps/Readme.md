# Build the Generated CMake Project on Linux

One of the features VS Code Digital Twin tooling provides is generating stub code based on the Device Capability Model (DCM) you specified.

Follow the steps to use the generated code with the Azure IoT Device C SDK source to compile a device app.

For more details about setting up your development environment for compiling the C Device SDK. Check the [instructions](https://github.com/Azure/azure-iot-sdk-c/blob/master/iothub_client/readme.md#compiling-the-c-device-sdk) for each platform.

## Prerequisite
1. Make sure all dependencies are installed before building the SDK. For Ubuntu, you can use apt-get to install the right packages.
    ```bash
    sudo apt-get update
    sudo apt-get install -y git cmake build-essential curl libcurl4-openssl-dev libssl-dev uuid-dev
    ```

1. Verify that **CMake** is at least version **2.8.12** and **gcc** is at least version **4.4.7**.
    ```bash
    cmake --version
    gcc --version
    ```

## Build with Source Code of Azure IoT Device C SDK
1. Go to the **root folder of your generated app**.
    ```bash
    cd nvidia-jetson-dps
    ```

1. git clone the preview release of the Azure IoT Device C SDK to your app folder using the `public-preview` branch.
    ```bash
    git clone https://github.com/Azure/azure-iot-sdk-c --recursive -b public-preview
    ```
    > The `--recursive` argument instructs git to clone other GitHub repos this SDK depends on. Dependencies are listed [here](https://github.com/Azure/azure-iot-sdk-c/blob/master/.gitmodules).

    NOTE: Or you can copy the source code of Azure IoT Device C SDK to your app folder if you already have a local copy.

1. Create a folder for your CMake build.
    ```bash
    mkdir cmake
    cd cmake
    ```

1. Run CMake to build your app with `azure-iot-sdk-c` source code.
    ```bash
    cd cmake
    cmake .. -Duse_prov_client=ON -Dhsm_type_symm_key:BOOL=ON
    cmake --build .
    ```

1. Once the build has succeeded, you can test it by specifying the DPS info (**Device Id**, **DPS ID Scope**, **DPS Symmetric Key**) as its parameter.
    ```bash
    ./nvidia-jetson-dps [Device Id] [DPS ID Scope] [DPS symmetric key]
    ```
