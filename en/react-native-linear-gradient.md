> Template version: v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-linear-gradient/react-native-linear-gradient">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github address](https://github.com/react-native-oh-library/react-native-linear-gradient)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-linear-gradient Releases](https://github.com/react-native-oh-library/react-native-linear-gradient/releases).

Go to the project directory and execute the following instruction:

> [!TIP] # Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-linear-gradient@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-linear-gradient@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { ReactNode } from 'react';
import {
    SafeAreaView,
    ScrollView,
    StatusBar,
    StyleSheet,
    Text,
    View,
} from 'react-native';
import LinearGradient from "react-native-linear-gradient";

// Within your render function
function LinearGradientDemo() {
    return (
        <View style={styles.container}>
            <LinearGradient
                colors={["#4c669f", "#3b5998", "#192f6a"]}
                style={styles.linearGradient}
            >
            <Text style={styles.buttonText}>Sign in with Facebook</Text>
            </LinearGradient>;
        </View>
    );
};
export default LinearGradientDemo;
// Later on in your styles..
var styles = StyleSheet.create({
    container: {
        backgroundColor: '#fff',
        flex: 1,
        paddingTop: 24,
    },
    linearGradient: {
        flex: 1,
        paddingLeft: 15,
        paddingRight: 15,
        borderRadius: 5,
    },
    buttonText: {
        fontSize: 18,
        fontFamily: "Gill Sans",
        textAlign: "center",
        margin: 10,
        color: "#ffffff",
        backgroundColor: "transparent",
    },
});
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-linear-gradient": "file:../../node_modules/@react-native-oh-tpl/react-native-linear-gradient/harmony/linear_gradient.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code.](/zh-cn/link-source-code.md)

### 3.Configuring CMakeLists and Introducing LinearGradientPackage Package

Open entry/src/main/cpp/CMakeLists.txt and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-linear-gradient/src/main/cpp" ./linear-gradient)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_linear_gradient)
# RNOH_END: manual_package_linking_2
```

Open entry/src/main/cpp/PackageProvider.cpp and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "LinearGradientPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<LinearGradientPackage>(ctx)
    };
}
```

### 4.Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

## Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-linear-gradient Releases](https://github.com/react-native-oh-library/react-native-linear-gradient/releases)

This document is verified based on the following versions:
1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 5.0.3.228; ROM: 3.0.0.23;

## Properties

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description                                              | Type                   | Required | Platform | HarmonyOS Support (ArkTS) | HarmonyOS Support (CAPI) |
| ----------- | -------------------------------------------------------- | ---------------------- | -------- | -------- |---------------------------|--------------------------|
| colors      | Color Array                                              | (string\|number)[]     | NO       | All      | yes                       | yes                      |
| locations   | Color for unknown array (length 0 or the same as colors) | number[]               | NO       | All      | yes                       | yes                      |
| useAngle    | Use angle (default false)                                | boolean                | NO       | All      | yes                       | yes                      |
| angle       | Angle (useAngle=true valid)                              | number                 | NO       | All      | yes                       | yes                      |
| angleCenter | Middle angle coordinate                                  | { x: number,y: number} | NO       | All      | no                        | yes                      |
| start       | Starting point coordinates (default value: {x: 0.5,1})   | { x: number,y: number} | NO       | All      | partial                   | yes                      |
| end         | End point coordinates (default value: {x: 0.5,1})        | { x: number,y: number} | NO       | All      | partial                   | yes                      |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE).