> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient</code> </h1>
</p>

This project is based on [react-native-linear-gradient@3.0.0-alpha.1](https://github.com/react-native-linear-gradient/react-native-linear-gradient)。

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-linear-gradient`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.0.0-0.5.0@deprecated | @react-native-oh-tpl/react-native-linear-gradient | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient/releases) |
| > 3.0.0                   | @react-native-ohos/react-native-linear-gradient   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/releases) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

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

### 2.3 Configuring CMakeLists and Introducing LinearGradientPackage Package

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

### 2.4 Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

## 3.1 Compatibility

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

## 5. Known Issues

- The current version of HarmonyOS does not support angleCenter.

## 6. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/blob/master/LICENSE).
