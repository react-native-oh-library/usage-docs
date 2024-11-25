> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-netinfo)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/netinfo Releases](https://github.com/react-native-oh-library/react-native-netinfo/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/netinfo
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/netinfo
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
    "@react-native-oh-tpl/netinfo": "file:../../node_modules/@react-native-oh-tpl/netinfo/harmony/netinfo.har"
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

### 3. Configuring CMakeLists and Introducing RNCNetInfoPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing NetInfoPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 5. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/netinfo Releases](https://github.com/react-native-oh-library/react-native-netinfo/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                                                                                                                                                                                                                                                                                                                                                               |   Type   | Required |  Platform   | HarmonyOS Support |
|------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|:--------:|:--------:|:-----------:|:-----------------:|
| `fetch()`              | Returns a Promise that resolves to a NetInfoState object.                                                                                                                                                                                                                                                                                                                                 | function |   yes    | iOS Android |        yes        |
| `refresh()`            | Updates NetInfo's internal state, then returns a Promise that resolves to a NetInfoState object. <br/>This is similar to fetch(), but really only useful on platforms that do not supply internet reachability natively. <br/>For example, you can use it to immediately re-run an internet reachability test if a network request fails unexpectedly.                                    | function |   yes    | iOS Android |        yes        |
| `addEventListener()`   | Subscribe to connection information. <br/>The callback is called with a parameter of type NetInfoState whenever the connection state changes. <br/>Your listener will be called with the latest information soon after you subscribe and then with any subsequent changes afterwards. <br/>You should not assume that the listener is called in the same way across devices or platforms. | function |   yes    | iOS Android |        yes        |
| `useNetInfo()`         | A React Hook which can be used to get access to the latest state from the global instance. <br/>It returns a hook with the NetInfoState type.                                                                                                                                                                                                                                             | function |   yes    | iOS Android |        yes        |
| `useNetInfoInstance()` | A React Hook which can be used to create and manage an isolated instance of a network manager class. <br/>It returns a refresh function and the current NetInfoState.                                                                                                                                                                                                                     | function |   yes    | iOS Android |        yes        |

## Known Issues

- [ ] bluetooth接口属性未适配: [issue#14](https://github.com/react-native-oh-library/react-native-netinfo/issues/14)
- [ ] wimax接口属性未适配: [issue#15](https://github.com/react-native-oh-library/react-native-netinfo/issues/15)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-netinfo/react-native-netinfo/blob/master/LICENSE).
