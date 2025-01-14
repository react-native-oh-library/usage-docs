> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-ble-plx)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-ble-plx Releases](https://github.com/react-native-oh-library/react-native-ble-plx/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-ble-plx": "file:../../node_modules/@react-native-oh-tpl/react-native-ble-plx/harmony/rn_bleplx.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.在 ArkTs 侧引入 BlePlxPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-ble-plx Releases](https://github.com/react-native-oh-library/react-native-ble-plx/releases)

### 权限要求

- 由于此库涉及蓝牙系统控制功能，使用对应接口时则需要配置对应的权限，权限需配置在entry/src/main目录下module.json5文件中。其中部分权限需弹窗向用户申请授权。具体权限配置见文档：[程序访问控制](https://gitee.com/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/Readme-CN.md#/openharmony/docs/blob/master/zh-cn/application-dev/security/AccessToken/app-permission-mgmt-overview.md)。

- 此库部分功能与接口需要normal权限：ohos.permission.ACCESS_BLUETOOTH。

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 遗留问题

- [ ] cancelTransaction(transactionId: string)接口harmony暂不支持: [issue#2](https://github.com/react-native-oh-library/react-native-ble-plx/issues/2)
- [ ] setLogLevel(logLevel: string)接口harmony暂不支持: [issue#3](https://github.com/react-native-oh-library/react-native-ble-plx/issues/3)
- [ ] logLevel()接口harmony暂不支持: [issue#4](https://github.com/react-native-oh-library/react-native-ble-plx/issues/4)
- [ ] requestConnectionPriorityForDevice(deviceId: string, connectionPriority: number,transactionId: string)接口harmony暂不支持: [issue#5](https://github.com/react-native-oh-library/react-native-ble-plx/issues/5)

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/dotintent/react-native-ble-plx/blob/master/LICENSE) ，请自由地享受和参与开源。
