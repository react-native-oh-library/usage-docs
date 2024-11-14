> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-MJRefresh</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-studio/react-native-MJRefresh">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-studio/react-native-MJRefresh/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-MJRefresh)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-MJRefresh Releases](https://github.com/react-native-oh-library/react-native-MJRefresh/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-mjrefresh
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-mjrefresh
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { Component } from "react";
import { Text, View } from "react-native";
import MJRefresh, { ScrollView } from "react-native-mjrefresh";

export default class MjRefreshDemo extends Component {
  constructor(props) {
    super(props);
  }

  state = {
    text: "Pull to Refresh",
    refreshing: false
  }
  _onRefresh = () => {
    setTimeout(() => {
      this._hw && this._hw.finishRefresh();
    }, 1000);
  }
  render() {
    return (
      <ScrollView
        refreshControl={
          <MJRefresh
            ref={ref => this._mjrefresh = ref}
            onRefresh={
              () => {
                this.setState({
                  text: 'Refreshing'
                })
                console.log('onRefresh')
                setTimeout(() => {
                  this._mjrefresh && this._mjrefresh.finishRefresh();
                }, 1000)
              }
            }
            onRefreshIdle={() => console.log('onRefreshIdle')}
            onReleaseToRefresh={() => {
              this.setState({
                text: 'Release to Refresh'
              })
            }}
            onPulling={e => {
              console.log('cbdtest onPulling:' + e.nativeEvent.percent)
              if (e.nativeEvent.percent < 0.1) {
                this.setState({
                  text: 'Pull to Refresh'
                })
              }
            }}
          >
            <View style={{
              height: 100, backgroundColor: 'red',
              justifyContent: 'center',
              alignItems: 'center', flexDirection: 'row'
            }}>
              <Text>{this.state.text}</Text>
            </View>
          </MJRefresh>
        }
      >
        <Text>{"mjRefresh TEST mjRefresh TEST mjRefresh TEST mjRefresh TEST mjRefresh TEST"}</Text>
      </ScrollView>
    )
  };
};
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

    "@react-native-oh-tpl/react-native-mjrefresh": "file:../../node_modules/@react-native-oh-tpl/react-native-mjrefresh/harmony/mjrefresh.har"
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

### 3. Configuring CMakeLists and Introducing MJRefreshPackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-mjrefresh/src/main/cpp" ./mjrefresh)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_mjrefresh)
# RNOH_END: manual_package_linking_2
```

Open  `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "MJRefreshPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<MJRefreshPackage>(ctx),
    };
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-MJRefresh Releases](https://github.com/react-native-oh-library/react-native-MJRefresh/releases)

## Properties 

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For more details, see [react-native-MJRefresh](https://github.com/react-native-studio/react-native-MJRefresh)

| Name               | Description | Type     | Required | Platform | HarmonyOS Support (ArkTS) |HarmonyOS Support (CAPI) |
| :----------------- | ----------- | -------- | -------- | -------- | ----------------- |----------------- |
| onRefresh          | System Path | function | No       | IOS      | yes               |yes               |
| onRefreshIdle      | System Path | function | No       | IOS      | yes               |yes               |
| onReleaseToRefresh | System Path | function | No       | IOS      | yes               |yes               |
| onPulling          | System Path | function | No       | IOS      | yes               |yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For more details, see [react-native-MJRefresh](https://github.com/react-native-studio/react-native-MJRefresh)

| Name          | Description | Type     | Required | Platform | HarmonyOS Support (ArkTS) | HarmonyOS Support (CAPI) |
| :------------ | ----------- | -------- | -------- | -------- | ----------------- |----------------- |
| beginRefresh  | System Path | function | No       | IOS      | yes               |yes               |
| finishRefresh | System Path | function | No       | IOS      | yes               |yes               |

## Others

## License

This project is licensed under [Apache License (Apache)](https://github.com/react-native-studio/react-native-MJRefresh/blob/master/LICENSE).
