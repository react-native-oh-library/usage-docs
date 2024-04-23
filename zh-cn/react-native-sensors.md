> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-sensors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-sensors/react-native-sensors">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-sensors/react-native-sensors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-sensors/react-native-sensors)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/sensors Releases](https://github.com/react-native-oh-library/react-native-sensors/releases/)，并下载适用版本的 tgz 包

#### **npm**

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

```bash
npm install  @react-native-oh-tpl/react-native-sensors@file:#
```

#### **yarn**

```bash
yarn add  @react-native-oh-tpl/react-native-sensors@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。 应用设备需具备对应类型的传感器

```js
import {
  accelerometer,
  gyroscope,
  setUpdateIntervalForType,
  magnetometer,
  barometer,
  orientation,
  gravity,
} from "react-native-sensors";

//accelerometer  加速度计 accelerometer: Observable<{x: number, y: number, z: number, timestamp: string}>
accelerometer.subscribe(({ x, y, z, timestamp }) =>
  console.log("accelerometer", { x, y, z, timestamp })
);

//gyroscope  陀螺仪 gyroscope: Observable<{x: number, y: number, z: number, timestamp: string}>
gyroscope
  .pipe(filter((speed) => speed.x > 1))
  .subscribe(({ x, y, z, timestamp }) =>
    console.log("gyroscope", { x, y, z, timestamp })
  );

//magnetometer 磁力计 magnetometer: Observable<{x: number, y: number, z: number, timestamp: string}>
magnetometer.subscribe(({ x, y, z, timestamp }) =>
  console.log("magnetometer", { x, y, z, timestamp })
);

//barometer 气压计 barometer: Observable<{pressure: number}>
barometer.subscribe(({ pressure }) => console.log("barometer", { pressure }));

//orientation 方向 orientation: Observable<{x: number, y: number, z: number, timestamp: string}>
orientation.subscribe(({ x, y, z, timestamp }) =>
  console.log("orientation", { x, y, z, timestamp })
);

//gravity 重力 gravity: Observable<{x: number, y: number, z: number, timestamp: string}>
gravity.subscribe(({ x, y, z, timestamp }) =>
  console.log("gravity", { x, y, z, timestamp })
);
// setUpdateIntervalForType(type: string, interval: number)
setUpdateIntervalForType(SensorTypes.accelerometer, 100);
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-sensors": "file:../../node_modules/@react-native-oh-tpl/react-native-sensors/harmony/sensors.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-sensors": "file:../../node_modules/@react-native-oh-tpl/sensors/harmony/sensors"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 SensorsPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/sensors/src/main/cpp" ./sensors)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: rnoh_sensors
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_sensors)
# RNOH_END: rnoh_sensors
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SensorsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SensorsPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 SensorsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {SensorsPackage} from "rnoh-sensors/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SensorsPackage(ctx)
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

## 约束与限制

设备使用 sensors 时需具备对应类型的传感器。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[Releases](https://github.com/react-native-oh-library/react-native-sensors/releases/)

## API

| Name                     | Description  | Platform    | HarmonyOS Support |
| ------------------------ | ------------ | ----------- | ----------------- |
| accelerometer            | 加速度计     | ios/Android | yes               |
| gyroscope                | 陀螺仪       | ios/Android | yes               |
| magnetometer             | 磁力计       | ios/Android | yes               |
| barometer                | 气压计       | ios/Android | yes               |
| orientation              | 方向         | ios/Android | yes               |
| gravity                  | 重力         | ios/Android | yes               |
| setUpdateIntervalForType | 间隔时间     | ios/Android | yes               |
| setLogLevelForType       | 日志打印级别 | ios/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Kureev/react-native-blur/blob/master/LICENSE) ，请自由地享受和参与开源。
