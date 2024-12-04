> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-reanimated</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-reanimated">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-harmony-reanimated/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-reanimated Releases](https://github.com/react-native-oh-library/react-native-harmony-reanimated/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-reanimated@3.6.0
npm install @react-native-oh-tpl/react-native-reanimated
```

#### **yarn**

```bash
yarn add react-native-reanimated@3.6.0
yarn add @react-native-oh-tpl/react-native-reanimated
```

<!-- tabs:end -->

添加 react-native-reanimated/plugin 插件到 `babel.config.js`:

> [!TIP] 为什么需要添加这个？Reanimated Babel 插件会自动转换特殊的 JavaScript 函数（称为 worklet），以便它们可以被传递并在 UI 线程上运行。

```js
  module.exports = {
    presets: [
      ... // don't add it here :)
    ],
    plugins: [
      ...
      'react-native-reanimated/plugin',
    ],
  };
```

清除 Metro 的缓存（推荐）:

<!-- tabs:start -->

#### **npm**

```bash
npm start -- --reset-cache
```

#### **yarn**

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { Button, View } from "react-native";
import Animated, { useSharedValue, withSpring } from "react-native-reanimated";

export default function App() {
  const width = useSharedValue(100);

  const handlePress = () => {
    width.value = withSpring(width.value + 50);
  };

  return (
    <View style={{ flex: 1, alignItems: "center" }}>
      <Animated.View
        style={{
          width,
          height: 100,
          backgroundColor: "violet",
        }}
      />
      <Button onPress={handlePress} title="Click me" />
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

    "@react-native-oh-tpl/react-native-reanimated": "file:../../node_modules/@react-native-oh-tpl/react-native-reanimated/harmony/reanimated.har"
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

### 3.配置 CMakeLists 和引入 ReanimatedPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-reanimated/src/main/cpp" ./reanimated)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_reanimated)
# RNOH_BEGIN: manual_package_linking_2
```
> [!Tip] 注意：上面NODE_MODULES定义，为源库的安装路径，用户可以根据安装源库的路径定义NODE_MODULES

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ReanimatedPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ReanimatedPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 ReanimatedPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ReanimatedPackage } from '@react-native-oh-tpl/react-native-reanimated/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ReanimatedPackage(ctx),
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

## 约束与限制

### 兼容性

该库是基于react-native-reanimated（version=3.6.0）进行适配，要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-reanimated Releases](https://github.com/react-native-oh-library/react-native-harmony-reanimated/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                                                                                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `withTiming`       | withTiming lets you create an animation based on duration and easing..                                                                                                                                                     | function | No       | All      | yes               |
| `withSpring`       | withSpring lets you create spring-based animations.                                                                                                                                                                        | function | No       | All      | yes               |
| `withDecay`        | withDecay lets you create animations that mimic objects in motion with friction. The animation will start with the provided velocity and slow down over time according to the given deceleration rate until it stops.      | function | No       | All      | yes               |
| `withRepeat`       | withRepeat is an animation modifier that lets you repeat an animation given number of times or run it indefinitely.                                                                                                        | function | No       | All      | yes               |
| `useSharedValue`   | useSharedValue lets you define shared values in your components.                                                                                                                                                           | function | No       | All      | yes               |
| `useAnimatedStyle` | useAnimatedStyle lets you create a styles object, similar to StyleSheet styles, which can be animated using shared values.                                                                                                 | function | No       | All      | yes               |
| `useAnimatedRef`   | useAnimatedRef lets you get a reference of a view. Used alongside measure, scrollTo, and useScrollViewOffset functions.                                                                                                    | function | No       | All      | yes               |
| `useDerivedValue`  | useDerivedValue lets you create new shared values based on existing ones while keeping them reactive.                                                                                                                      | function | No       | All      | yes               |
| `cancelAnimation`  | cancelAnimation lets you cancel a running animation paired to a shared value.                                                                                                                                              | function | No       | All      | yes               |
| `runOnJS`          | runOnJS lets you asynchronously run non-workletized functions that could not otherwise run on the UI thread. This applies to most external libraries as they do not have their functions marked with "worklet"; directive. | function | No       | All      | yes               |
| `runOnUI`          | runOnUI lets you asynchronously run workletized functions on the UI thread.                                                                                                                                                | function | No       | All      | yes               |
| `measure`          | measure lets you synchronously get the dimensions and position of a view on the screen, all on the UI thread.                                                                                                              | function | No       | All      | yes               |
| `Easing`           | easing set motion trajectory                                                                                                                                                                                               | function | No       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE) ，请自由地享受和参与开源。
