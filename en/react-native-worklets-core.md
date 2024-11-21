> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-worklets-core</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/margelo/react-native-worklets-core">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/margelo/react-native-worklets-core/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-worklets-core)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-worklets-core Releases](https://github.com/react-native-oh-library/react-native-worklets-core/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm i @react-native-oh-tpl/react-native-worklets-core
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-worklets-core
```

Add babel plugins in the babel.config.js file located at the root directory of the project.

```js
module.exports = {
  plugins: [
    ["@react-native-oh-tpl/react-native-worklets-core/plugin"],
    // ...
  ],
  // ...
};
```

Reset cache and restart the project.

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import { useState } from "react";
import { Button, Text, View } from "react-native";
import { useRunOnJS, useWorklet } from "react-native-worklets-core";

const App = () => {
  const [count, setCount] = useState(0);
  const setCountRunInJS = useRunOnJS(() => {
    setCount(Math.random());
  }, [count]);
  const countInWorkLet = useWorklet(
    "default",
    () => {
      "worklet";
      setCountRunInJS();
    },
    [setCountRunInJS]
  );

  return (
    <View>
      <View style={{ flexDirection: "row", gap: 10 }}>
        <Button title="SetCount" onPress={() => countInWorkLet()} />
      </View>
      <Text>count:{count}</Text>
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
    "@react-native-oh-tpl/react-native-worklets-core": "file:../../node_modules/@react-native-oh-tpl/react-native-worklets-core/harmony/rn_worklets.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```shell
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing Worklets Package

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

add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-oh-tpl/react-native-worklets-core/src/main/cpp" ./worklets)

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_worklets)
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "WorkletsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<WorkletsPackage>(ctx)
    };
}
```

### 4. Introducing WorkletsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { WorkletsPackage } from "@react-native-oh-tpl/react-native-worklets-core/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new WorkletsPackage(ctx)
  ];
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```shell
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-worklets-core Releases](https://github.com/react-native-oh-library/react-native-worklets-core/releases)

### API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME                   | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| createContext          | Creates a new worklet context with the given name.           | function  | no       | All      | yes               |
| createSharedValue      | Creates a value that can be shared between runtimes.         | function  | no       | All      | yes               |
| createRunOnJS          | Creates a function that can be executed asynchronously on the default React-JS context. | function  | no       | All      | yes               |
| runOnJS                | Runs the given Function asynchronously on the default React-JS context. | function  | no       | All      | yes               |
| getCurrentThreadId     | Returns a unique identifier for the Thread this method is called on. | function  | no       | All      | yes               |
| defaultContext         | Get the default Worklet context.                             | interface | no       | All      | yes               |
| currentContext         | Get the current Worklet context, or `undefined` if called in main React JS context. | interface | no       | All      | yes               |
| __jsi_is_array         | Returns true if jsi/cpp believes that the passed value is an array. | function  | no       | All      | yes               |
| __jsi_is_object        | Returns true if jsi/cpp believes that the passed value is an object. | function  | no       | All      | yes               |
| context.addDecorator   | Adds an object to the worklet context. The object will be available in all worklets. | function  | no       | All      | yes               |
| context.createRunAsync | Creates a function that can be executed asynchronously on the Worklet context. | function  | no       | All      | yes               |
| context.runAsync       | Runs the given Function asynchronously on this Worklet context. | function  | no       | All      | yes               |
| useWorklet             | Create a Worklet function that automatically memoizes itself using it's auto-captured closure. | function  | no       | All      | yes               |
| useRunOnJS             | Create a Worklet function that runs the given function on the JS context. | function  | no       | All      | yes               |
| useSharedValue         | Create a Shared Value that persists between re-renders.      | function  | no       | All      | yes               |
| isWorklet              | Checks whether the given function is a Worklet or not.       | function  | no       | All      | yes               |
| worklet                | Ensures the given function is a Worklet, and throws an error if not. | function  | no       | All      | yes               |
| getWorkletDependencies | Get the dependencies of the given worklet.                   | function  | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/margelo/react-native-worklets-core/blob/main/LICENSE).
