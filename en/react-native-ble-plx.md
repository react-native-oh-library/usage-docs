> Template version: v0.2.2

<p align="center">
  <h1 align="center"><code>react-native-ble-plx</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/dotintent/react-native-ble-plx">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/dotintent/react-native-ble-plx/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-ble-plx)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-ble-plx Releases](https://github.com/react-native-oh-library/react-native-ble-plx/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-ble-plx
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-ble-plx
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {
  BleError,
  BleErrorCode,
  BleManager,
  Device,
  State as BluetoothState,
  LogLevel,
  type DeviceId,
  type TransactionId,
  type UUID,
  type Characteristic,
  type Base64,
  type Subscription
} from 'react-native-ble-plx'

class BLEServiceInstance {
  manager: BleManager
  device: Device | null

  constructor() {
    this.device = null
    this.manager = new BleManager()
  }

  scanDevices = async (onDeviceFound: (device: Device) => void, UUIDs: UUID[] | null = null) => {
    this.manager.startDeviceScan(UUIDs, null, (error, device) => {
      if (error) {
        console.error(error.message)
        this.manager.stopDeviceScan()
        return
      }
      if (device) {
        onDeviceFound(device)
      }
    })
  }

  connectToDevice = (deviceId: DeviceId) =>
    new Promise<Device>((resolve, reject) => {
      this.manager.stopDeviceScan()
      this.manager
        .connectToDevice(deviceId)
        .then(device => {
          this.device = device
          resolve(device)
        })
        .catch(error => {
          if (error.errorCode === BleErrorCode.DeviceAlreadyConnected && this.device) {
            resolve(this.device)
          } else {
            console.error(error.message)
            reject(error)
          }
        })
    })

  discoverAllServicesAndCharacteristicsForDevice = async () =>
    new Promise<Device>((resolve, reject) => {
      if (!this.device) {
        reject(new Error(deviceNotConnectedErrorText))
        return
      }
      this.manager
        .discoverAllServicesAndCharacteristicsForDevice(this.device.id)
        .then(device => {
          resolve(device)
          this.device = device
        })
        .catch(error => {
          reject(error)
        })
    })

  readCharacteristicForDevice = async (serviceUUID: UUID, characteristicUUID: UUID) =>
    new Promise<Characteristic>((resolve, reject) => {
      if (!this.device) {
        reject(new Error(deviceNotConnectedErrorText))
        return
      }
      this.manager
        .readCharacteristicForDevice(this.device.id, serviceUUID, characteristicUUID)
        .then(characteristic => {
          resolve(characteristic)
        })
        .catch(error => {
          console.error(error.message)
        })
    })

  writeCharacteristicWithResponseForDevice = async (serviceUUID: UUID, characteristicUUID: UUID, time: Base64) => {
    if (!this.device) {
      console.error(deviceNotConnectedErrorText)
      throw new Error(deviceNotConnectedErrorText)
    }
    return this.manager
      .writeCharacteristicWithResponseForDevice(this.device.id, serviceUUID, characteristicUUID, time)
      .catch(error => {
        console.error(error.message)
      })
  }
```

## Use Codegen

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-ble-plx": "file:../../node_modules/@react-native-oh-tpl/react-native-ble-plx/harmony/rn_bleplx.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing  BlePlxPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {BlePlxPackage} from '@react-native-oh-tpl/react-native-ble-plx/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BlePlxPackage(ctx)
  ];
}
```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-ble-plx Releases](https://github.com/react-native-oh-library/react-native-ble-plx/releases)

### Permission Requirements

- 由于此库涉及蓝牙系统控制功能，使用对应接口时则需要配置对应的权限，权限需配置在entry/src/main目录下module.json5文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要normal权限：ohos.permission.ACCESS_BLUETOOTH。

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| createClient(restoreStateIdentifier?: string)  | creat client         | void | yes | iOS/Android      | yes |
| destroyClient()  | remove client         | Promise<void> | yes | iOS/Android      | yes |
| cancelTransaction(transactionId: string)  | cancel transcation         | Promise<void> | yes | iOS/Android      | no |
| setLogLevel(logLevel: string)  | set log level         | Promise<Object> | yes | iOS/Android      | no |
| logLevel()  | show log level         | Promise<Object> | yes | iOS/Android      | no |
| enable(transactionId: string)  | can get transaction Id       | Promise<void> | yes | iOS/Android      | yes |
| disable(transactionId: string)  | cannot get transaction Id        | Promise<void> | yes | iOS/Android      | yes |
| state()  | bluetooth state         | Promise<Object> | yes | iOS/Android      | yes |
| startDeviceScan(filteredUUIDs: string[], options: Object)  | start scan device         | Promise<void>| yes | iOS/Android      | yes |
| stopDeviceScan()  | stop scan device         | Promise<void> | yes | iOS/Android      | yes |
| requestConnectionPriorityForDevice(deviceId: string, connectionPriority: number,transactionId: string) | request connect priority device         | Promise<Object> | yes | iOS/Android      | no |                                     
| readRSSIForDevice(deviceId: string, transactionId: string)  | read RSSI device        | Promise<Object> | yes | iOS/Android      | yes |
| requestMTUForDevice(deviceId: string, mtu: number, transactionId: string)  | request MTU device         | Promise<Object> | yes | iOS/Android      | yes |
| devices(deviceIdentifiers: string[])  | identify devices         | Promise<Object[]> | yes | iOS/Android      | yes |
| connectedDevices(serviceUUIDs: string[])  | connect devices         | Promise<Object[]> | yes | iOS/Android      | yes |
| connectToDevice(deviceId: string, options?: Object)  | option to connect device         | Promise<Object> | yes | iOS/Android      | yes |
| cancelDeviceConnection(deviceId: string)  | cancel device connection        | Promise<Object> | yes | iOS/Android      | yes |
| isDeviceConnected(deviceId: string)  | connected device         | Promise<boolean> | yes | iOS/Android      | yes |
| discoverAllServicesAndCharacteristicsForDevice(deviceId: string, transactionId: string)  | discover all device service and characteristics         | Promise<Object> | yes | iOS/Android      | yes |
| servicesForDevice(deviceId: string)  | device service         | Promise<Object[]> | yes | iOS/Android      | yes |
| characteristicsForDevice(deviceId: string, serviceUUID: string)  | device characteristics         | Promise<Object[]> | yes | iOS/Android      | yes |
| characteristicsForService(serviceIdentifier: number)  | service characteristics         | Promise<Object[]> | yes | iOS/Android      | yes |
| descriptorsForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string): Promise<Object[]>  | device descriptors         | Promise<Object[]> | yes | iOS/Android      | yes |
| descriptorsForService(serviceIdentifier: number, characteristicUUID: string)  | service descriptors       | Promise<Object[]> | yes | iOS/Android        | yes |
| descriptorsForCharacteristic(characteristicIdentifier: number)   |descriptors identifier device characteristic         | Promise<Object[]> | yes | iOS/Android      | yes |
| readCharacteristicForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, transactionId: string)  | read device characteristic         | Promise<Object> | yes | iOS/Android      | yes |
| readCharacteristicForService(serviceIdentifier: number, characteristicUUID: string,transactionId: string)  | read  service charcteristic        | Promise<Object> | yes | iOS/Android      | yes |
| readCharacteristic(characteristicIdentifier: number, transactionId: string)  | read identifier characteristic      | Promise<Object> | yes | iOS/Android      | yes |
| writeCharacteristicForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, valueBase64: string,response: boolean, transactionId: string)  | write device  characteristic      | Promise<Object> | yes | iOS/Android      | yes |
| writeCharacteristicForService(serviceIdentifier: number, characteristicUUID: string, valueBase64: string,response: boolean, transactionId: string)  | write service characteristic       | Promise<Object> | yes | iOS/Android      | yes |
| writeCharacteristic(characteristicIdentifier: number, valueBase64: string, response: boolean,transactionId: string)  |  write  identifier characteristic         | Promise<Object> | yes | iOS/Android      | yes |
| monitorCharacteristicForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string,transactionId: string)  | monitor device  characteristic        | Promise<void> | yes | iOS/Android      | yes |
| monitorCharacteristicForService(serviceIdentifier: number, characteristicUUID: string,transactionId: string)  | monitor service  characteristic         | Promise<void> | yes | iOS/Android      | yes |
| monitorCharacteristic(characteristicIdentifier: number, transactionId: string)  | monitor identifier characteristic        | Promise<void> | yes | iOS/Android      | yes |
| readDescriptorForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, descriptorUUID: string,transactionId: string)  | read device descriptor      | Promise<Object> | yes | iOS/Android      | yes |
| readDescriptorForService(serviceIdentifier: number, characteristicUUID: string, descriptorUUID: string,transactionId: string)  | read service descriptor         | Promise<Object> | yes | iOS/Android      | yes |
| readDescriptorForCharacteristic(characteristicIdentifier: number, descriptorUUID: string,transactionId: string)  | read identifier characteristic descriptor          | Promise<Object> | yes | iOS/Android      | yes |
| readDescriptor(descriptorIdentifier: number, transactionId: string)  | read identifier descriptor         | Promise<Object> | yes | iOS/Android      | yes |
| writeDescriptorForDevice(deviceId: string, serviceUUID: string, characteristicUUID: string, descriptorUUID: string,valueBase64: string, transactionId: string)  | write device descriptor        | Promise<Object> | yes | iOS/Android      | yes |
| writeDescriptorForService(serviceIdentifier: number, characteristicUUID: string, descriptorUUID: string,valueBase64: string, transactionId: string)  | write service descriptor         | Promise<Object> | yes | iOS/Android      | yes |
| writeDescriptorForCharacteristic(characteristicIdentifier: number, descriptorUUID: string, valueBase64: string,transactionId: string)  | write identifier characteristic descriptor          | Promise<Object> | yes | iOS/Android      | yes |
| writeDescriptor(descriptorIdentifier: number, valueBase64: string, transactionId: string)  | write identifier descriptor        | Promise<Object> | yes | iOS/Android      | yes |

## Known Issues

- [ ] cancelTransaction(transactionId: string) is not supported in harmony: [issue#2](https://github.com/react-native-oh-library/react-native-ble-plx/issues/2)
- [ ] setLogLevel(logLevel: string) is not supported in harmony: [issue#3](https://github.com/react-native-oh-library/react-native-ble-plx/issues/3)
- [ ] logLevel() is not supported in harmony: [issue#4](https://github.com/react-native-oh-library/react-native-ble-plx/issues/4)
- [ ] requestConnectionPriorityForDevice(deviceId: string, connectionPriority: number,transactionId: string) is not supported in harmony: [issue#5](https://github.com/react-native-oh-library/react-native-ble-plx/issues/5)

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/dotintent/react-native-ble-plx/blob/master/LICENSE).
