<!-- {% raw %} -->
> 模板版本：v0.2.2

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

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-safe-area-context)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-area-context@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-area-context@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-safe-area-context": "file:../../node_modules/@react-native-oh-tpl/react-native-safe-area-context/harmony/safe_area.har"
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

### 配置 CMakeLists 和引入 SafeAreaViewPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 在 ArkTs 侧引入 SafeAreaViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**组件 SafeAreaProvider**

You should add `SafeAreaProvider` in your app root component. You may need to add it in other places like the root of modals and routes when using react-native-screens.

Note that providers should not be inside a View that is animated with Animated or inside a ScrollView since it can cause very frequent updates.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props`          | Accepts all View props. Has a default style of {flex: 1}.                                                                                                       | object | no       | All      | yes      |
| `initialMetrics` | Can be used to provide the initial value for frame and insets, this allows rendering immediatly. See optimization for more information on how to use this prop. | object | no       | All      | yes      |

**组件 SafeAreaView**

`SafeAreaView` is a regular View component with the safe area insets applied as padding or margin.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ------- | ----------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props` | Accepts all View props. Has a default style of {flex: 1}.                                       | object | no       | All      | yes      |
| `edges` | Sets the edges to apply the safe area insets to. Defaults to all.                               | array  | no       | All      | yes      |
| `mode`  | Optional, padding (default) or margin. Apply the safe area to either the padding or the margin. | string | no       | All      | yes      |

# API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type     | Required | Platform | HarmonyOS Support  |
| ---- | ----------- |----------|----------| -------- | ------------------ |
| useSafeAreaInsets  | Returns the safe area insets of the nearest provider.         | object   | no       | All      | yes   |
| useSafeAreaFrame  | Returns the frame of the nearest provider. This can be used as an alternative to the Dimensions module.       | object | no       | All      | yes   |
| SafeAreaInsetsContext  | React Context with the value of the safe area insets.         | object | no       | All      | yes  |
| withSafeAreaInsets  | Higher order component that provides safe area insets as the insets prop.         | function | no       | All      | yes   |
| SafeAreaFrameContext  | React Context with the value of the safe area frame.         | object | no       | All      | yes  |
| initialWindowMetrics  | Insets and frame of the window on initial render. This can be used with the initialMetrics from SafeAreaProvider  | object | no       | All      | yes   |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->
