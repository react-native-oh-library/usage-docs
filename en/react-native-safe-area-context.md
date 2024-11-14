> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-area-context</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/th3rdwave/react-native-safe-area-context">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20web%20%7C%20macos%20%7C%20windows%20%7C%20harmony-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github address](https://github.com/react-native-oh-library/react-native-safe-area-context)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-area-context
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-area-context
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { Text, View } from "react-native";
import {
  SafeAreaProvider,
  SafeAreaView,
  initialWindowMetrics,
} from "react-native-safe-area-context";

const App = () => {
  return (
    <SafeAreaProvider initialMetrics={initialWindowMetrics}>
      <SafeAreaView style={{ flex: 1, backgroundColor: "red" }}>
        <View style={{ flex: 1 }}>
          <Text>hello</Text>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
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

    "@react-native-oh-tpl/react-native-safe-area-context": "file:../../node_modules/@react-native-oh-tpl/react-native-safe-area-context/harmony/safe_area.har"
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

### 3. Configuring CMakeLists and Introducing SafeAreaViewPackage

Open `entry/src/main/cpp/CMakeLists.txt ` and add the following code:

```diff
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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-safe-area-context/src/main/cpp" ./safe-area)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_safe_area)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SafeAreaViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SafeAreaViewPackage>(ctx),
    };
}
```

### 4. Introducing SafeAreaViewPackage to ArkTS 

Open the`entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import {SafeAreaViewPackage} from '@react-native-oh-tpl/react-native-safe-area-context/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SafeAreaViewPackage(ctx)
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

## Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**SafeAreaProvider**

You should add `SafeAreaProvider` in your app root component. You may need to add it in other places like the root of modals and routes when using react-native-screens.

Note that providers should not be inside a View that is animated with Animated or inside a ScrollView since it can cause very frequent updates.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props`          | Accepts all View props. Has a default style of {flex: 1}.                                                                                                       | object | no       | All      | yes      |
| `initialMetrics` | Can be used to provide the initial value for frame and insets, this allows rendering immediatly. See optimization for more information on how to use this prop. | object | no       | All      | yes      |

**SafeAreaView**

`SafeAreaView` is a regular View component with the safe area insets applied as padding or margin.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ------- | ----------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props` | Accepts all View props. Has a default style of {flex: 1}.                                       | object | no       | All      | yes      |
| `edges` | Sets the edges to apply the safe area insets to. Defaults to all.                               | array  | no       | All      | yes      |
| `mode`  | Optional, padding (default) or margin. Apply the safe area to either the padding or the margin. | string | no       | All      | yes      |

# API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type     | Required | Platform | HarmonyOS Support  |
| ---- | ----------- |----------|----------| -------- | ------------------ |
| useSafeAreaInsets  | Returns the safe area insets of the nearest provider.         | object   | no       | All      | yes   |
| useSafeAreaFrame  | Returns the frame of the nearest provider. This can be used as an alternative to the Dimensions module.       | object | no       | All      | yes   |
| SafeAreaInsetsContext  | React Context with the value of the safe area insets.         | object | no       | All      | yes  |
| withSafeAreaInsets  | Higher order component that provides safe area insets as the insets prop.         | function | no       | All      | yes   |
| SafeAreaFrameContext  | React Context with the value of the safe area frame.         | object | no       | All      | yes  |
| initialWindowMetrics  | Insets and frame of the window on initial render. This can be used with the initialMetrics from SafeAreaProvider  | object | no       | All      | yes   |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE).
