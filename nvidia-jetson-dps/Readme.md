# nvidia-jetson-dps

Azure IoT PnP application to enable remote interaction and telemetry for DeepStream on Nvidia Jetson Devices using [Device Provisioning Service](https://docs.microsoft.com/en-us/azure/iot-dps/?WT.mc_id=github-deepstreampnp-pdecarlo) for [IoT Central](https://docs.microsoft.com/en-us/azure/iot-central/?WT.mc_id=github-deepstreampnp-pdecarlo)

## Obtaining a DPS ID Scope, DPS symmetric key, and device ID

Install [node.js](https://nodejs.org/) then install dps-keygen utility with:
```
npm i -g dps-keygen
```

Ensure that you have followed the [steps to create an Azure IoT Central application](https://docs.microsoft.com/en-us/azure/iot-central/quick-deploy-iot-central-pnp?toc=/azure/iot-central-pnp/toc.json&bc=/azure/iot-central-pnp/breadcrumb/toc.json?WT.mc_id=github-deepstreampnp-pdecarlo) then follow these [steps to Generate a device key](https://docs.microsoft.com/en-us/azure/iot-central/quick-create-pnp-device-pnp?toc=/azure/iot-central-pnp/toc.json&bc=/azure/iot-central-pnp/breadcrumb/toc.json#generate-device-key?WT.mc_id=github-deepstreampnp-pdecarlo).

[DPS ID Scope] is obtained from the "Administration => Device Connection" section of your IoT Central Application.  

During the steps to Generate a device key, 
```
dps-keygen  -di:jetson-device -mk:{Primary Key from IoT Central}
```

the value used for -di becomes [device ID] and the output of executing the above command becomes [DPS symmetric key]

## Usage

nvidia-jetson-dps [DPS ID Scope] [DPS symmetric key] [device ID]