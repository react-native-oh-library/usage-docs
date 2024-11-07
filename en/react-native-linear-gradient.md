> Template version: v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-linear-gradient/react-native-linear-gradient">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [Gitee Repository](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient)

> [Gitee Releases: @react-native-ohos/react-native-linear-gradient](https://github.com/react-native-oh-library/react-native-linear-gradient/releases)

> [Github Repository(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient)

> [Github Releases(<= 3.0.0-0.5.0): @react-native-ohos/react-native-linear-gradient](https://github.com/react-native-oh-library/react-native-linear-gradient/releases)

## Installation and Usage

`This third-party library has been migrated to Gitee and is now available for direct download from npm.`

Go to the project directory and execute the following instruction:

> [!TIP] # Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-linear-gradient
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-linear-gradient
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { ReactNode } from "react";
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  View,
} from "react-native";
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
      </LinearGradient>
      ;
    </View>
  );
}
export default LinearGradientDemo;
// Later on in your styles..
var styles = StyleSheet.create({
  container: {
    backgroundColor: "#fff",
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

### 2. Introducing Native Code

Currently, two methods are available:

1. Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-linear-gradient": "file:../../node_modules/@react-native-ohos/react-native-linear-gradient/harmony/linear_gradient.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code.](/en/link-source-code.md)

### 3. Configuring CMakeLists and Introducing LinearGradientPackage Package

Open entry/src/main/cpp/CMakeLists.txt and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-linear-gradient/src/main/cpp" ./linear-gradient)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_linear_gradient)
# RNOH_END: manual_package_linking_2
```

Open entry/src/main/cpp/PackageProvider.cpp and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "LinearGradientPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<LinearGradientPackage>(ctx)
    };
}
```

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native-linear-gradient Releases](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/releases)

## Properties

> [!TIP] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name        | Description                                              | Type                   | Required | Platform | HarmonyOS Support |
| ----------- | -------------------------------------------------------- | ---------------------- | -------- | -------- | ----------------- |
| colors      | Color Array                                              | (string\|number)[]     | NO       | All      | yes               |
| locations   | Color for unknown array (length 0 or the same as colors) | number[]               | NO       | All      | yes               |
| useAngle    | Use angle (default false)                                | boolean                | NO       | All      | yes               |
| angle       | Angle (useAngle=true valid)                              | number                 | NO       | All      | yes               |
| angleCenter | Middle angle coordinate                                  | { x: number,y: number} | NO       | All      | no                |
| start       | Starting point coordinates (default value: {x: 0.5,1})   | { x: number,y: number} | NO       | All      | yes               |
| end         | End point coordinates (default value: {x: 0.5,1})        | { x: number,y: number} | NO       | All      | yes               |

## Known Issues

- The current version of HarmonyOS does not support angleCenter.

## Others

## License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/blob/master/LICENSE).
