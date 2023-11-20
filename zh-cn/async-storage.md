<p align="center">
  <h1 align="center"> <code>@react-native-async-storage/async-storage</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-async-storage/async-storage">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-async-storage/async-storage/blob/main/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-async-storage/async-storage.svg" alt="License" />
    </a>
</p>

## 安装与使用

> [!tip] 目前 React-Native-OpenHarmony(RNOH) 三方库的 npm 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```bash
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-async-storage/async-storage@npm:@react-native-oh-library/async-storage
```

或者

```bash
npm install @react-native-async-storage/async-storage@npm:@react-native-oh-library/async-storage
```

下面的代码展示了这个库的基本使用场景：

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

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-slider": "file:../../node_modules/@react-native-async-storage/async-storage/harmony/async_storage.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-slider": "file:../../node_modules/@react-native-async-storage/async-storage/harmony/async-storage"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 SliderPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-async-storage/src/main/cpp" ./async-storage)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_async_storage)
# RNOH_END: link_packages
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

### 在 ArkTs 侧引入 slider 组件

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {AsyncStoragePackage} from 'rnoh-async-storage/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AsyncStoragePackage(ctx)
  ];
}

```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

| `@react-native-oh-library/async-storage` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version  |
| ------------------------------------------------ | ----------------------------- | --------------------- | ------------------------------ | --------------------- |
| `1.19.5-0.0.3`                                   | `0.72.5`                      | `0.72.10`             | `4.0.3.601`                    | `OpenHarmony 4.10.10` |

## API

| 名称              | 说明                                                                                                                                                     | 类型     | 是否必填 | 平台 | 鸿蒙支持 |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ---- | -------- |
| `getItem`         | Gets a string value for given key. This function can either return a string value for existing key or return null otherwise.                             | function | No       | All  | yes      |
| `setItem`         | Sets a string value for given key. This operation can either modify an existing entry, if it did exist for given key, or add new one otherwise.          | function | No       | All  | yes      |
| `mergeItem`       | Merges an existing value stored under key, with new value, assuming both values are stringified JSON.                                                    | function | No       | All  | yes      |
| `removeItem`      | Removes item for a key, invokes (optional) callback once completed.                                                                                      | function | No       | All  | yes      |
| `getAllKeys`      | Returns all keys known to your App, for all callers, libraries, etc. Once completed, invokes callback with errors (if any) and array of keys.            | function | No       | All  | yes      |
| `multiGet`        | Fetches multiple key-value pairs for given array of keys in a batch. Once completed, invokes callback with errors (if any) and results.                  | function | No       | All  | yes      |
| `multiSet`        | Stores multiple key-value pairs in a batch. Once completed, callback with any errors will be called.                                                     | function | No       | All  | yes      |
| `multiMerge`      | Multiple merging of existing and new values in a batch. Assumes that values are stringified JSON. Once completed, invokes callback with errors (if any). | function | No       | All  | yes      |
| `multiRemove`     | Clears multiple key-value entries for given array of keys in a batch. Once completed, invokes a callback with errors (if any).                           | function | No       | All  | yes      |
| `clear`           | Removes whole AsyncStorage data, for all clients, libraries, etc. You probably want to use removeItem or multiRemove to clear only your App's keys.      | function | No       | All  | yes      |
| `useAsyncStorage` | The useAsyncStorage returns an object that exposes all methods that allow you to interact with the stored value.                                         | hook     | No       | All  | yes      |

## 遗留问题

- [ ] Harmony 的 taskpool 支持类型有限，无法用 taskpool 实现，仅用简单的线程锁替代
- [ ] Harmony 无法设置指定的存储大小

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。