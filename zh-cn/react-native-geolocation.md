<!-- {% raw %} -->
> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> react-native-geolocation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/michalchudziak/react-native-geolocation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-geolocation/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License"/>
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-geolocation/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-geolocation Releases](https://github.com/react-native-oh-library/react-native-geolocation/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-geolocation@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-geolocation@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
// setRNConfiguration 为例
Geolocation.setRNConfiguration(
  config: {
    skipPermissionRequests: boolean;
    authorizationLevel?: 'always' | 'whenInUse' | 'auto';
    enableBackgroundLocationUpdates?: boolean;
    locationProvider?: 'playServices' | 'android' | 'auto';
  }
) => void
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "rnoh-geolocation": "file:../../node_modules/@react-native-oh-tpl/react-native-geolocation/harmony/geolocation.har"
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
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-geolocation/src/main/cpp" ./geolocation)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_geolocation)
# RNOH_END: link_packages
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
+ import {GeoLocationPackage} from 'rnoh-geolocation/ts';

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-geolocation Releases](https://github.com/react-native-oh-library/react-native-geolocation/releases)

### 权限要求

打开 entry/src/main/module.json5,添加

```
{
  "module": {
    "requestPermissions": [
      {"name": "ohos.permission.INTERNET"},
      {"name": "ohos.permission.LOCATION"},S
      {"name": "ohos.permission.APPROXIMATELY_LOCATION"},
    ]
  }
}
```

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                                            | Type                                            | Required | Platform    | HarmonyOS Support | Notes                                                                                                       |
| -------------------- | -------------------------------------------------------------------------------------- | ----------------------------------------------- | -------- | ----------- | ----------------- | ----------------------------------------------------------------------------------------------------------- |
| setRNConfiguration   | Sets configuration options that will be used in all location requests                  | function(config)                                | NO       | IOS Android | partially         | config 仅支持 skipPermissionRequests                                                                        |
| requestAuthorization | Request suitable Location permission                                                   | function(success,error)                         | YES      | IOS Android | partially         | success 支持,error 仅支持 code 与 message                                                                   |
| getCurrentPosition   | Invokes the success callback once with the latest location info                        | function(success(position),error(error),option) | NO       | IOS Android | partially         | position 中仅 altitudeAccuracy 不支持,option 仅支持 timeout 与 maximumAge,error 仅支持 code 与 message      |
| watchPosition        | Invokes the success callback whenever the location changes. Returns a watchId (number) | function(success(postion),error(error),option)  | NO       | IOS Android | partially         | position 中仅 altitudeAccuracy 不支持,error 仅支持 code 与 message,option 仅支持 interval 与 distanceFilter |
| clearWatch           | Clears watch observer by id returned by watchPosition()                                | function(watchID)                               | NO       | IOS Android | yes               | watchID 仅支持默认值 0                                                                                      |

## 遗留问题

- [ ] react-native-geolocation 部分属性未实现 HarmonyOS 化: [issue#I8WRMI](https://gitee.com/react-native-oh-library/usage-docs/issues/I8WRMI)

## 其他

## 开源协议

本项目基于 [The MIT License(MIT)](https://github.com/react-native-oh-library/react-native-geolocation/blob/sig/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->