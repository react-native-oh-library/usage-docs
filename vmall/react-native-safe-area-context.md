> 模板版本：v0.1.1

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

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-area-context
```

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-area-context
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

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
    "rnoh-safe-area": "file:../../node_modules/@react-native-oh-tpl/react-native-safe-area-context/harmony/safe_area.har"
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
    "rnoh-safe-area": "file:../../node_modules/@react-native-oh-tpl/react-native-safe-area-context/harmony/safe_area"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 SafeAreaViewPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-safe-area/src/main/cpp" ./safe_area)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_safe_area)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SafeAreaViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SafeAreaViewPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 react-native-safe-area-context 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
import {
  RNApp,
  ComponentBuilderContext,
  RNAbility,
  AnyJSBundleProvider,
  MetroJSBundleProvider,
  ResourceJSBundleProvider,
} from 'rnoh'
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
import { createRNPackages } from '../RNPackagesFactory'
+ import { SAFE_AREA_VIEW_TYPE, SafeAreaView, SAFE_AREA_PROVIDER_TYPE, SafeAreaProvider } from "rnoh-safe-area"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === SAFE_AREA_VIEW_TYPE) {
+   SafeAreaView({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag,
+     buildCustomComponent: CustomComponentBuilder
+   })
+ }
+ else if (ctx.componentName === SAFE_AREA_PROVIDER_TYPE) {
+   SafeAreaProvider({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag,
+     buildCustomComponent: CustomComponentBuilder
+   })
+ }
 ...
}
...
```

### 在 ArkTs 侧引入 SafeAreaViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {SafeAreaViewPackage} from 'rnoh-safe-area/ts';

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

**组件 SafeAreaProvider**

You should add `SafeAreaProvider` in your app root component. You may need to add it in other places like the root of modals and routes when using react-native-screens.

Note that providers should not be inside a View that is animated with Animated or inside a ScrollView since it can cause very frequent updates.

| 名称             | 说明                                                                                                                                                            | 类型   | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props`          | Accepts all View props. Has a default style of {flex: 1}.                                                                                                       | object | no       | All      | yes      |
| `initialMetrics` | Can be used to provide the initial value for frame and insets, this allows rendering immediatly. See optimization for more information on how to use this prop. | object | no       | All      | yes      |

**组件 SafeAreaView**

`SafeAreaView` is a regular View component with the safe area insets applied as padding or margin.

| 名称    | 说明                                                                                            | 类型   | 是否必填 | 原库平台 | 鸿蒙支持 |
| ------- | ----------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| `Props` | Accepts all View props. Has a default style of {flex: 1}.                                       | object | no       | All      | yes      |
| `edges` | Sets the edges to apply the safe area insets to. Defaults to all.                               | array  | no       | All      | yes      |
| `mode`  | Optional, padding (default) or margin. Apply the safe area to either the padding or the margin. | string | no       | All      | yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/th3rdwave/react-native-safe-area-context/blob/main/LICENSE) ，请自由地享受和参与开源。
