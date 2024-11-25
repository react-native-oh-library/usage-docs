
> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/async-storage)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/async-storage Releases](https://github.com/react-native-oh-library/async-storage/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

> [!WARNING] 使用时 import 的库名不变。

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/async-storage": "file:../../node_modules/@react-native-oh-tpl/async-storage/harmony/async_storage.har"
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

### 3.配置 CMakeLists 和引入 AsynStoragePackge

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 4.在 ArkTs 侧引入 AsynStorage Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/async-storage Releases](https://github.com/react-native-oh-library/async-storage/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 遗留问题

- [ ] Harmony 的 taskpool 支持类型有限，无法用 taskpool 实现，仅用简单的线程锁替代,无法设置指定的存储大小: [issue#8](https://github.com/react-native-oh-library/async-storage/issues/8)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-async-storage/async-storage/blob/main/LICENSE) ，请自由地享受和参与开源。

