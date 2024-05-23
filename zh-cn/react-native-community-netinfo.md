> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-native-community/netinfo</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-netinfo/react-native-netinfo">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20windows%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-netinfo/react-native-netinfo/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-netinfo)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/netinfo Releases](https://github.com/react-native-oh-library/react-native-netinfo/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/netinfo@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/netinfo@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Text } from "react-native";
import NetInfo, { useNetInfo } from "@react-native-community/netinfo";

const App = () => {
  const [fetchInfo, setFetchInfo] = React.useState("");
  const [refreshInfo, setRefreshInfo] = React.useState("");
  const netInfo = useNetInfo();

  NetInfo.fetch().then((state) => {
    setFetchInfo(JSON.stringify(state));
  });
  NetInfo.refresh().then((state) => {
    setRefreshInfo(JSON.stringify(state));
  });

  return (
    <View>
      <Text>Type: {netInfo.type}</Text>
      <Text>Is Connected? {netInfo.isConnected?.toString()}</Text>
      <Text style={{ fontSize: 16, fontWeight: "600" }}>fetch():</Text>
      <Text>{fetchInfo}</Text>
      <Text style={{ fontSize: 16, fontWeight: "600" }}>refresh():</Text>
      <Text>{refreshInfo}</Text>
    </View>
  );
};
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "rnoh-netinfo": "file:../../node_modules/@react-native-oh-tpl/netinfo/harmony/netinfo.har"
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

### 配置 CMakeLists 和引入 RNCNetInfoPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-netinfo/src/main/cpp" ./netinfo)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_netinfo)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNCNetInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNCNetInfoPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 NetInfoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {NetInfoPackage} from 'rnoh-netinfo/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new NetInfoPackage(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/netinfo Releases](https://github.com/react-native-oh-library/react-native-netinfo/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### NetInfoStateType

| Name        | Description                                                | Type   | Required | Platform     | HarmonyOS Support |
| ----------- | ---------------------------------------------------------- | ------ | -------- | ------------ | ----------------- |
| `none`      | No network connection is active                            | String | no       | All          | yes               |
| `unknown`   | The network state could not or has yet to be be determined | String | no       | All          | yes               |
| `cellular`  | Active network over cellular                               | String | no       | All          | no                |
| `wifi`      | Active network over Wifi                                   | String | no       | All          | yes               |
| `bluetooth` | Active network over Bluetooth                              | String | no       | Android, Web | no                |
| `ethernet`  | Active network over wired ethernet                         | String | no       | All          | no                |
| `wimax`     | Active network over WiMax                                  | String | no       | Android, Web | no                |
| `vpn`       | Active network over VPN                                    | String | no       | Android      | no                |
| `other`     | Active network over another type of network                | String | no       | All          | no                |

#### NetInfoCellularGeneration

| Name   | Description                                                                                                       | Type   | Required | Platform              | HarmonyOS Support |
| ------ | ----------------------------------------------------------------------------------------------------------------- | ------ | -------- | --------------------- | ----------------- |
| `null` | Either we are not currently connected to a cellular network or type could not be determined                       | String | no       | Android, iOS, Windows | no                |
| `2g`   | Currently connected to a 2G cellular network. Includes CDMA, EDGE, GPRS, and IDEN type connections                | String | no       | Android, iOS, Windows | no                |
| `3g`   | Currently connected to a 3G cellular network. Includes EHRPD, EVDO, HSPA, HSUPA, HSDPA, and UTMS type connections | String | no       | Android, iOS, Windows | no                |
| `4g`   | Currently connected to a 4G cellular network. Includes HSPAP and LTE type connections                             | String | no       | Android, iOS, Windows | no                |
| `5g`   | Currently connected to a 5G cellular network. Includes NRNSA (iOS only) and NR type connections                   | String | no       | Android, iOS, Windows | no                |

#### NetInfoState

| Name                  | Description                                                                                                                                                                                                                                                                                                                                    | Type             | Required | Platform | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `type`                | The type of the current connection.                                                                                                                                                                                                                                                                                                            | NetInfoStateType | yes      | All      | yes               |
| `isConnected`         | If there is an active network connection. Defaults to null on most platforms for unknown networks. Note: Web browsers report network type unknown for many otherwise valid networks (https://caniuse.com/netinfo), so isConnected may be true or false and represent a real connection status even for unknown network types in certain cases. | boolean, null    | yes      | All      | yes               |
| `isInternetReachable` | If the internet is reachable with the currently active network connection. If unknown defaults to null                                                                                                                                                                                                                                         | boolean, null    | yes      | All      | yes               |
| `isWifiEnabled`       | (Android only) Whether the device's WiFi is ON or OFF.                                                                                                                                                                                                                                                                                         | boolean          | yes      | All      | yes               |
| `details`             | The value depends on the type value. See below.                                                                                                                                                                                                                                                                                                |                  | yes      | All      | yes               |

### Details

#### Type is none or unknown

`details` is `null`.

#### Type is wifi

| Name                    | Description                                                                                                                                                                                                                                                                                                                                                                                                | Type    | Required | Platform                           | HarmonyOS Support |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ---------------------------------- | ----------------- |
| `isConnectionExpensive` | If the network connection is considered "expensive". This could be in either energy or monetary terms.                                                                                                                                                                                                                                                                                                     | boolean | yes      | All                                | yes               |
| `ssid`                  | The SSID of the network. May not be present, null, or an empty string if it cannot be determined. On iOS, your app must meet at least one of the following requirements and you must set the shouldFetchWiFiSSID configuration option or no attempt will be made to fetch the SSID. On Android, you need to have the ACCESS_FINE_LOCATION permission in your AndroidManifest.xml and accepted by the user. | string  | yes      | Android, iOS (not tvOS), Windows   | yes               |
| `bssid`                 | The BSSID of the network. May not be present, null, or an empty string if it cannot be determined. On iOS, make sure your app meets at least one of the following requirements. On Android, you need to have the ACCESS_FINE_LOCATION permission in your AndroidManifest.xml and accepted by the user.                                                                                                     | string  | yes      | Android, iOS (not tvOS), Windows\* | yes               |
| `strength`              | An integer number from 0 to 100 for the signal strength. May not be present if the signal strength cannot be determined.                                                                                                                                                                                                                                                                                   | number  | yes      | Android, Windows                   | yes               |
| `ipAddress`             | The external IP address. Can be in IPv4 or IPv6 format. May not be present if it cannot be determined.                                                                                                                                                                                                                                                                                                     | string  | yes      | Android, iOS, macOS, Windows       | yes               |
| `subnet`                | The subnet mask in IPv4 format. May not be present if it cannot be determined.                                                                                                                                                                                                                                                                                                                             | string  | yes      | Android, iOS, macOS                | yes               |
| `frequency`             | Network frequency. Example: For 2.4 GHz networks, the method will return 2457. May not be present if it cannot be determined.                                                                                                                                                                                                                                                                              | number  | yes      | Android, Windows\*                 | yes               |
| `linkSpeed`             | The link speed in Mbps.                                                                                                                                                                                                                                                                                                                                                                                    | number  | yes      | Android                            | yes               |
| `rxLinkSpeed`           | The current receive link speed in Mbps.                                                                                                                                                                                                                                                                                                                                                                    | number  | yes      | Android                            | yes               |
| `txLinkSpeed`           | The current transmit link speed in Mbps.                                                                                                                                                                                                                                                                                                                                                                   | number  | yes      | Android                            | yes               |

#### Type is cellular

| Name                    | Description                                                                                                           |           Type            | Required |       Platform        | HarmonyOS Support |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------- | :-----------------------: | :------: | :-------------------: | :---------------: |
| `isConnectionExpensive` | If the network connection is considered "expensive". This could be in either energy or monetary terms.                |          boolean          |   yes    |          All          |        no         |
| `cellularGeneration`    | The generation of the cell network the user is connected to. This can give an indication of speed, but no guarantees. | NetInfoCellularGeneration |   yes    | Android, iOS, Windows |        no         |
| `carrier`               | The network carrier name. May not be present or may be empty if none can be determined.                               |          +string          |   yes    |     Android, iOS      |        no         |

#### Type is bluetooth, ethernet, wimax, vpn, or other

| Name                    | Description                                                                                            |  Type   | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------------------------------------------------ | :-----: | :------: | :------: | :---------------: |
| `isConnectionExpensive` | If the network connection is considered "expensive". This could be in either energy or monetary terms. | boolean |   yes    |   All    |        no         |

## 静态方法

| Name                   | Description                                                                                                                                                                                                                                                                                                                                                                |   Type   | Required | Platform | HarmonyOS Support |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------: | :------: | :------: | :---------------: |
| `fetch()`              | Returns a Promise that resolves to a NetInfoState object.                                                                                                                                                                                                                                                                                                                  | function |   yes    |   All    |        yes        |
| `refresh()`            | Updates NetInfo's internal state, then returns a Promise that resolves to a NetInfoState object. This is similar to fetch(), but really only useful on platforms that do not supply internet reachability natively. For example, you can use it to immediately re-run an internet reachability test if a network request fails unexpectedly.                               | function |   yes    |   All    |        yes        |
| `addEventListener()`   | Subscribe to connection information. The callback is called with a parameter of type NetInfoState whenever the connection state changes. Your listener will be called with the latest information soon after you subscribe and then with any subsequent changes afterwards. You should not assume that the listener is called in the same way across devices or platforms. | function |   yes    |   All    |        yes        |
| `useNetInfo()`         | A React Hook which can be used to get access to the latest state from the global instance. It returns a hook with the NetInfoState type.                                                                                                                                                                                                                                   | function |   yes    |   All    |        yes        |
| `useNetInfoInstance()` | A React Hook which can be used to create and manage an isolated instance of a network manager class. It returns a refresh function and the current NetInfoState.                                                                                                                                                                                                           | function |   yes    |   All    |        yes        |

## 遗留问题

- 涉及非 wifi 环境下的接口属性未适配

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-netinfo/react-native-netinfo/blob/master/LICENSE) ，请自由地享受和参与开源。
