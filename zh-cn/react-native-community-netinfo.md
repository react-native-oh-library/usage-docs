> 模板版本：v0.2.2

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
export default App;
```

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/netinfo": "file:../../node_modules/@react-native-oh-tpl/netinfo/harmony/netinfo.har"
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

### 3.配置 CMakeLists 和引入 RNCNetInfoPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/netinfo/src/main/cpp" ./netinfo)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_netinfo)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNCNetInfoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNCNetInfoPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 NetInfoPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {NetInfoPackage} from '@react-native-oh-tpl/netinfo/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new NetInfoPackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/netinfo Releases](https://github.com/react-native-oh-library/react-native-netinfo/releases)


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### NetInfoStateType

| Name        | Description                                                | Type   | Required | Platform    | HarmonyOS Support |
|-------------|------------------------------------------------------------|--------|----------|-------------|-------------------|
| `none`      | No network connection is active                            | String | no       | iOS Android | yes               |
| `unknown`   | The network state could not or has yet to be be determined | String | no       | iOS Android | yes               |
| `cellular`  | Active network over cellular                               | String | no       | iOS Android | yes               |
| `wifi`      | Active network over Wifi                                   | String | no       | iOS Android | yes               |
| `bluetooth` | Active network over Bluetooth                              | String | no       | Android     | no                |
| `ethernet`  | Active network over wired ethernet                         | String | no       | iOS Android | yes               |
| `wimax`     | Active network over WiMax                                  | String | no       | Android     | no                |
| `vpn`       | Active network over VPN                                    | String | no       | Android     | yes               |
| `other`     | Active network over another type of network                | String | no       | iOS Android | yes               |

#### NetInfoCellularGeneration

| Name   | Description                                                                                                       | Type   | Required | Platform    | HarmonyOS Support |
|--------|-------------------------------------------------------------------------------------------------------------------|--------|----------|-------------|-------------------|
| `null` | Either we are not currently connected to a cellular network or type could not be determined                       | String | no       | iOS Android | yes               |
| `2g`   | Currently connected to a 2G cellular network. Includes CDMA, EDGE, GPRS, and IDEN type connections                | String | no       | iOS Android | yes               |
| `3g`   | Currently connected to a 3G cellular network. Includes EHRPD, EVDO, HSPA, HSUPA, HSDPA, and UTMS type connections | String | no       | iOS Android | yes               |
| `4g`   | Currently connected to a 4G cellular network. Includes HSPAP and LTE type connections                             | String | no       | iOS Android | yes               |
| `5g`   | Currently connected to a 5G cellular network. Includes NRNSA (iOS only) and NR type connections                   | String | no       | iOS Android | yes               |

#### NetInfoState

| Name                  | Description                                                                                                                                                                                                                                                                                                                                                | Type             | Required | Platform    | HarmonyOS Support |
|-----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------|----------|-------------|-------------------|
| `type`                | The type of the current connection.                                                                                                                                                                                                                                                                                                                        | NetInfoStateType | yes      | iOS Android | yes               |
| `isConnected`         | If there is an active network connection.<br/>Defaults to null on most platforms for unknown networks.<br/>Note: Web browsers report network type unknown for many otherwise valid networks (https://caniuse.com/netinfo),<br/>so isConnected may be true or false and represent a real connection status even for unknown network types in certain cases. | boolean, null    | yes      | iOS Android | yes               |
| `isInternetReachable` | If the internet is reachable with the currently active network connection.<br/>If unknown defaults to null                                                                                                                                                                                                                                                 | boolean, null    | yes      | iOS Android | yes               |
| `isWifiEnabled`       | (Android only) Whether the device's WiFi is ON or OFF.                                                                                                                                                                                                                                                                                                     | boolean          | yes      | iOS Android | yes               |
| `details`             | The value depends on the type value. See below.                                                                                                                                                                                                                                                                                                            | object           | yes      | iOS Android | yes               |

### Details

#### Type is wifi

| Name                    | Description                                                                                                                                                                                                                                                                                                                                                                                                                    | Type    | Required | Platform    | HarmonyOS Support |
|-------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------|----------|-------------|-------------------|
| `isConnectionExpensive` | If the network connection is considered "expensive".<br/>This could be in either energy or monetary terms.                                                                                                                                                                                                                                                                                                                     | boolean | yes      | iOS Android | yes               |
| `ssid`                  | The SSID of the network. <br/>May not be present, null, or an empty string if it cannot be determined. <br/>On iOS, your app must meet at least one of the following requirements and you must set the shouldFetchWiFiSSID configuration option or no attempt will be made to fetch the SSID. <br/>On Android, you need to have the ACCESS_FINE_LOCATION permission in your AndroidManifest.<br/>xml and accepted by the user. | string  | yes      | iOS Android | yes               |
| `bssid`                 | The BSSID of the network. <br/>May not be present, null, or an empty string if it cannot be determined. <br/>On iOS, make sure your app meets at least one of the following requirements. <br/>On Android, you need to have the ACCESS_FINE_LOCATION permission in your AndroidManifest.<br/>xml and accepted by the user.                                                                                                     | string  | yes      | iOS Android | yes               |
| `strength`              | An integer number from 0 to 100 for the signal strength. <br/>May not be present if the signal strength cannot be determined.                                                                                                                                                                                                                                                                                                  | number  | yes      | Android     | yes               |
| `ipAddress`             | The external IP address. Can be in IPv4 or IPv6 format. <br/>May not be present if it cannot be determined.                                                                                                                                                                                                                                                                                                                    | string  | yes      | iOS Android | yes               |
| `subnet`                | The subnet mask in IPv4 format. <br/>May not be present if it cannot be determined.                                                                                                                                                                                                                                                                                                                                            | string  | yes      | iOS Android | yes               |
| `frequency`             | Network frequency. Example: For 2.4 GHz networks, the method will return 2457. <br/>May not be present if it cannot be determined.                                                                                                                                                                                                                                                                                             | number  | yes      | Android     | yes               |
| `linkSpeed`             | The link speed in Mbps.                                                                                                                                                                                                                                                                                                                                                                                                        | number  | yes      | Android     | yes               |
| `rxLinkSpeed`           | The current receive link speed in Mbps.                                                                                                                                                                                                                                                                                                                                                                                        | number  | yes      | Android     | yes               |
| `txLinkSpeed`           | The current transmit link speed in Mbps.                                                                                                                                                                                                                                                                                                                                                                                       | number  | yes      | Android     | yes               |

#### Type is cellular

| Name                    | Description                                                                                                           |           Type            | Required |  Platform   | HarmonyOS Support |
|-------------------------|-----------------------------------------------------------------------------------------------------------------------|:-------------------------:|:--------:|:-----------:|:-----------------:|
| `isConnectionExpensive` | If the network connection is considered "expensive". This could be in either energy or monetary terms.                |          boolean          |   yes    | iOS Android |        yes        |
| `cellularGeneration`    | The generation of the cell network the user is connected to. This can give an indication of speed, but no guarantees. | NetInfoCellularGeneration |   yes    | iOS Android |        yes        |
| `carrier`               | The network carrier name. May not be present or may be empty if none can be determined.                               |          string           |   yes    | iOS Android |        yes        |

#### Type is bluetooth, ethernet, wimax, vpn, or other

| Name                    | Description                                                                                                 |  Type   | Required |  Platform   | HarmonyOS Support |
|-------------------------|-------------------------------------------------------------------------------------------------------------|:-------:|:--------:|:-----------:|:-----------------:|
| `isConnectionExpensive` | If the network connection is considered "expensive". <br/>This could be in either energy or monetary terms. | boolean |   yes    | iOS Android |        yes        |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                                                                                                                                                                                                                                                                                                                                               |   Type   | Required |  Platform   | HarmonyOS Support |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:--------:|:-----------:|:-----------------:|
| `fetch()`              | Returns a Promise that resolves to a NetInfoState object.                                                                                                                                                                                                                                                                                                                                 | function |   yes    | iOS Android |        yes        |
| `refresh()`            | Updates NetInfo's internal state, then returns a Promise that resolves to a NetInfoState object. <br/>This is similar to fetch(), but really only useful on platforms that do not supply internet reachability natively. <br/>For example, you can use it to immediately re-run an internet reachability test if a network request fails unexpectedly.                                    | function |   yes    | iOS Android |        yes        |
| `addEventListener()`   | Subscribe to connection information. <br/>The callback is called with a parameter of type NetInfoState whenever the connection state changes. <br/>Your listener will be called with the latest information soon after you subscribe and then with any subsequent changes afterwards. <br/>You should not assume that the listener is called in the same way across devices or platforms. | function |   yes    | iOS Android |        yes        |
| `useNetInfo()`         | A React Hook which can be used to get access to the latest state from the global instance. <br/>It returns a hook with the NetInfoState type.                                                                                                                                                                                                                                             | function |   yes    | iOS Android |        yes        |
| `useNetInfoInstance()` | A React Hook which can be used to create and manage an isolated instance of a network manager class. <br/>It returns a refresh function and the current NetInfoState.                                                                                                                                                                                                                     | function |   yes    | iOS Android |        yes        |

## 遗留问题

- [ ] bluetooth接口属性未适配: [issue#14](https://github.com/react-native-oh-library/react-native-netinfo/issues/14)
- [ ] wimax接口属性未适配: [issue#15](https://github.com/react-native-oh-library/react-native-netinfo/issues/15)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-netinfo/react-native-netinfo/blob/master/LICENSE) ，请自由地享受和参与开源。
