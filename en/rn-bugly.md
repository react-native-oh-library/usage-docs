> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-bugly</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yz1311/rn-bugly">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/rn-bugly)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/rn-bugly Releases](https://github.com/react-native-oh-library/rn-bugly/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm install @react-native-oh-tpl/rn-bugly@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/rn-bugly@file:#
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import {
    ScrollView,
    View,
    Button
} from 'react-native';
import RNBugly from 'rn-bugly';
export default class BuglyExample extends React.Component {
    _init() {
        RNBugly.init("appid", "appkey");
    }
    _setUserId() {
        RNBugly.setUserId("123456");
    }
    _setDeviceID() {
        RNBugly.setDeviceID("666666677777");
    }
    _setDeviceModel() {
        RNBugly.setDeviceModel("HUAWEI Mate 60 Pro");
    }
    _setAppVersion() {
        RNBugly.setAppVersion("2.0.2");
    }
    _setAppChannel() {
        RNBugly.setAppChannel("HarmonyOS");
    }
    _putUserData() {
        RNBugly.putUserData("name", "xiaoli");
    }
    _postException() {
        RNBugly.postException({ category: 1, errorType: "test", errorMsg: "throw new err" });
    }
    render() {
        return (
            <View
                style={{ flex: 1, backgroundColor: 'green', justifyContent: 'center', alignItems: 'center' }}
            >
                <ScrollView
                    style={{ flex: 1, width: '100%', height: '100%', marginTop: 150 }}
                >
                    <Button title='setAppVersion' onPress={this._setAppVersion} />
                    <Button title='setAppChannel' onPress={this._setAppChannel} />
                    <Button title='setUserId' onPress={this._setUserId} />
                    <Button title='setDeviceID' onPress={this._setDeviceID} />
                    <Button title='setDeviceModel' onPress={this._setDeviceModel} />
                    <Button title='init' onPress={this._init} />
                    <Button title='putUserData' onPress={this._putUserData} />
                    <Button title='postException' onPress={this._postException} />
                </ScrollView>
            </View>
        );
    }
}
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
    "@react-native-oh-tpl/rn-bugly": "file:../../node_modules/@react-native-oh-tpl/rn-bugly/harmony/bugly.har"
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

### 3. Configuring CMakeLists and Introducing RNBuglyPackage Package

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/rn-bugly/src/main/cpp" ./bugly)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_bugly)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNBuglyPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNBuglyPackage>(ctx)
    };
}
```

### 4. Introducing RNBuglyPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNBuglyPackage} from '@react-native-oh-tpl/rn-bugly/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBuglyPackage(ctx),
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/rn-bugly Releases](https://github.com/react-native-oh-library/rn-bugly/releases)



## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |-------- | -------- | ------------------ |
| init | Initialize SDK | function  |Yes | Android | Yes |
| setUserId | Set the current user ID | function  |No       | iOS/Android     | Yes      |
| setAppVersion | Set custom version information | function  |No       | iOS/Android      | Yes      |
| setDeviceID | Set device ID | function  |No | Android | Yes |
| setDeviceModel| Set device model | function  |No | Android | Yes |
| setAppChannel | Set channel name | function  |No | Android | Yes |
| setAppPackage | Set custom package name | function  |No | Android | No |
| setTag | Custom tags | function  |No | iOS/Android | No |
| startCrashReport | Open CrashReport | function  |No | Android | No |
| closeCrashReport| Close CrashReport | function  |No | iOS/Android | No |
| getCurrentTag | Get the current setting label | function  |No | iOS/Android | No |
| getUserData | Obtain key data | function  |No | iOS/Android | No |
| getBuglyVersion | Get the version of SDK | function  |No | iOS/Android | No |
| putUserData | Custom Map parameters can save some custom environment information when a crash occurs | function  |No | iOS/Android | Yes |
| getUpgradeInfo | Retrieve the existing upgrade strategy locally                 | function  |No | Android | No |
| checkUpgrade | Check for version updates | function  |No | Android | No |
| log | Print log | function  |No | Android | No |
| postException | Report custom exceptions | function  |No | iOS/Android | Yes |
## Known Issues

- [ ] setAppPackage not support[issue#1](https://github.com/react-native-oh-library/rn-bugly/issues/1)
- [ ] setTag not support[issue#2](https://github.com/react-native-oh-library/rn-bugly/issues/2)
- [ ] startCrashReport not support[issue#3](https://github.com/react-native-oh-library/rn-bugly/issues/3)
- [ ] closeCrashReport not support[issue#4](https://github.com/react-native-oh-library/rn-bugly/issues/4)
- [ ] getCurrentTag not support[issue#5](https://github.com/react-native-oh-library/rn-bugly/issues/5)
- [ ] getUserData not support[issue#6](https://github.com/react-native-oh-library/rn-bugly/issues/6)
- [ ] getBuglyVersion not support[issue#7](https://github.com/react-native-oh-library/rn-bugly/issues/7)
- [ ] getUpgradeInfo not support[issue#8](https://github.com/react-native-oh-library/rn-bugly/issues/8)
- [ ] checkUpgrade not support[issue#9](https://github.com/react-native-oh-library/rn-bugly/issues/9)
- [ ] log not support[issue#10](https://github.com/react-native-oh-library/rn-bugly/issues/10)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://mit-license.org/).

