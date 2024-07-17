<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> @react-native-community/geolocation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/michalchudziak/react-native-geolocation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/michalchudziak/react-native-geolocation/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"/>
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-geolocation/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/geolocation Releases](https://github.com/react-native-oh-library/react-native-geolocation/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/geolocation@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/geolocation@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import Geolocation from "@react-native-community/geolocation";
import { Button } from "react-native";

export function GeolocationDemo(): JSX.Element {
  const tap = () => {
    Geolocation.setRNConfiguration({
      skipPermissionRequests: true,
      authorizationLevel: "auto",
      enableBackgroundLocationUpdates: true,
      locationProvider: "auto",
    });
    console.log("tap");
  };

  return <Button title='test' onPress={tap} />;
}
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
   ...
   "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/geolocation": "file:../../node_modules/@react-native-oh-tpl/geolocation/harmony/geolocation.har"
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

### 配置 CMakeLists 和引入 geolocation

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/geolocation/src/main/cpp" ./geolocation)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_geolocation)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "GeoLocationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<GeoLocationPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 GeolocationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {GeoLocationPackage} from '@react-native-oh-tpl/geolocation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GeoLocationPackage(ctx)
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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/geolocation Releases](https://github.com/react-native-oh-library/react-native-geolocation/releases)

### 权限要求

打开 entry/src/main/module.json5,添加

```
{
  "module": {
    "requestPermissions": [
      {"name": "ohos.permission.INTERNET"},
      {"name": "ohos.permission.LOCATION"},
      {"name": "ohos.permission.APPROXIMATELY_LOCATION"},
    ]
  }
}
```

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                                            | Type                                            | Required | Platform    | HarmonyOS Support | Notes                                                                                                                                                          |
| -------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------- | -------- | ----------- | ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| setRNConfiguration   | Sets configuration options that will be used in all location requests                  | function(config)                                | NO       | iOS Android | partially         | config only supports skipPermissionRequests                                                                                                                    |
| requestAuthorization | Request suitable Location permission                                                   | function(success,error)                         | YES      | iOS Android | partially         | error: Only code and message are supported.                                                                                                                    |
| getCurrentPosition   | Invokes the success callback once with the latest location info                        | function(success(position),error(error),option) | NO       | iOS Android | partially         | In position, only altitudeAccuracy is not supported. In option, only timeout and maximumAge are supported. In error, only code and message are supported.      |
| watchPosition        | Invokes the success callback whenever the location changes. Returns a watchId (number) | function(success(postion),error(error),option)  | NO       | iOS Android | partially         | In position, only altitudeAccuracy is not supported. In error, only code and message are supported. In option, only interval and distanceFilter are supported. |
| clearWatch           | Clears watch observer by id returned by watchPosition()                                | function(watchID)                               | NO       | iOS Android | yes               | watchID supports only the default value 0.                                                                                                                     |

## 遗留问题

- [ ] @react-native-oh-tpl/geolocation 部分属性未完全实现 HarmonyOS 化，maximumAge 延时问题: [issue#6](https://github.com/react-native-oh-library/react-native-geolocation/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License(MIT)](https://github.com/michalchudziak/react-native-geolocation/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
