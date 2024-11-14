> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-async-storage/async-storage</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-async-storage/async-storage">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-async-storage/async-storage/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/async-storage)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/async-storage Releases](https://github.com/react-native-oh-library/async-storage/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/async-storage
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/async-storage
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import AsyncStorage from "@react-native-async-storage/async-storage";

// Storing data
const storeData = async (value) => {
  try {
    await AsyncStorage.setItem("my-key", value);
  } catch (e) {
    // saving error
  }
};

// Reading data
const getData = async () => {
  try {
    const value = await AsyncStorage.getItem("my-key");
    if (value !== null) {
      // value previously stored
    }
  } catch (e) {
    // error reading value
  }
};
```

下面的代码展示了这个库的Hooks使用场景：

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from "react";
import { View, Text, TouchableOpacity } from "react-native";
import { useAsyncStorage } from "@react-native-async-storage/async-storage";

export default function App() {
  const [value, setValue] = useState("value");
  const { getItem, setItem } = useAsyncStorage("@storage_key");

  const readItemFromStorage = async () => {
    const item = await getItem();
    setValue(item);
  };

  const writeItemToStorage = async (newValue) => {
    await setItem(newValue);
    setValue(newValue);
  };

  useEffect(() => {
    readItemFromStorage();
  }, []);

  return (
    <View style={{ margin: 40 }}>
      <Text>Current value: {value}</Text>
      <TouchableOpacity
        onPress={() =>
          writeItemToStorage(Math.random().toString(36).substr(2, 5))
        }
      >
        <Text>Update value</Text>
      </TouchableOpacity>
    </View>
  );
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

    "@react-native-oh-tpl/async-storage": "file:../../node_modules/@react-native-oh-tpl/async-storage/harmony/async_storage.har"
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

### 3. Configuring CMakeLists and Introducing AsynStoragePackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/async-storage/src/main/cpp" ./async-storage)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_async_storage)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "AsyncStoragePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<AsyncStoragePackage>(ctx)
    };
}
```

### 4.Introducing AsynStoragePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+ import {AsyncStoragePackage} from '@react-native-oh-tpl/async-storage/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AsyncStoragePackage(ctx)
  ];
}
```

### 5.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/async-storage Releases](https://github.com/react-native-oh-library/async-storage/releases)

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                                                                                                              | Type                                                                                                                | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `getItem`         | Gets a string value for given key. This function can either return a string value for existing key or return null otherwise.                             | function(key: string, value: string, [callback]: ?(error: ?Error) => void): Promise                                 | No       | All      | yes               |
| `setItem`         | Sets a string value for given key. This operation can either modify an existing entry, if it did exist for given key, or add new one otherwise.          | function(key: string, value: string, [callback]: ?(error: ?Error) => void): Promise                                 | No       | All      | yes               |
| `mergeItem`       | Merges an existing value stored under key, with new value, assuming both values are stringified JSON.                                                    | function(key: string, value: string, [callback]: ?(error: ?Error) => void): Promise                                 | No       | All      | yes               |
| `removeItem`      | Removes item for a key, invokes (optional) callback once completed.                                                                                      | function(key: string, [callback]: ?(error: ?Error) => void): Promise                                                | No       | All      | yes               |
| `getAllKeys`      | Returns all keys known to your App, for all callers, libraries, etc. Once completed, invokes callback with errors (if any) and array of keys.            | function([callback]: ?(error: ?Error, keys: ?Array<string>) => void): Promise                                       | No       | All      | yes               |
| `multiGet`        | Fetches multiple key-value pairs for given array of keys in a batch. Once completed, invokes callback with errors (if any) and results.                  | function(keys: Array<string>, [callback]: ?(errors: ?Array<Error>, result: ?Array<Array<string>>) => void): Promise | No       | All      | yes               |
| `multiSet`        | Stores multiple key-value pairs in a batch. Once completed, callback with any errors will be called.                                                     | function(keyValuePairs: Array<Array<string>>, [callback]: ?(errors: ?Array<Error>) => void): Promise                | No       | All      | yes               |
| `multiMerge`      | Multiple merging of existing and new values in a batch. Assumes that values are stringified JSON. Once completed, invokes callback with errors (if any). | function(keyValuePairs: Array<Array<string>>, [callback]: ?(errors: ?Array<Error>) => void): Promise                | No       | All      | yes               |
| `multiRemove`     | Clears multiple key-value entries for given array of keys in a batch. Once completed, invokes a callback with errors (if any).                           | function(keys: Array<string>, [callback]: ?(errors: ?Array<Error>) => void)                                         | No       | All      | yes               |
| `clear`           | Removes whole AsyncStorage data, for all clients, libraries, etc. You probably want to use removeItem or multiRemove to clear only your App's keys.      | function([callback]: ?(error: ?Error) => void): Promise                                                             | No       | All      | yes               |
| `useAsyncStorage` | The useAsyncStorage returns an object that exposes all methods that allow you to interact with the stored value.                                         | hooks                                                                                                               | No       | All      | yes               |

## Known Issues

- [ ] Harmony 的 taskpool 支持类型有限，无法用 taskpool 实现，仅用简单的线程锁替代,无法设置指定的存储大小: [issue#8](https://github.com/react-native-oh-library/async-storage/issues/8)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-async-storage/async-storage/blob/main/LICENSE).
