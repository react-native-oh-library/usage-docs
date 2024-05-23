# 文档模板(删除)

> [!ATTENTION] 使用模板时请将后面带有 (删除) 的语句删除。<>内是需要修改的内容。(删除)

> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code><原库 npm 包名></code> </h1>
</p>
<p align="center">
    <a href="https://github.com/<原库源码仓地址>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|<如原库还支持其他平台，添加在此处>|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/<原库源码仓LICENSE的路径（如有）>">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/<鸿蒙化源码仓地址>)

如：

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-safe-area-context)（删除）

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/<库名> Releases](https://github.com/<仓库地址>/releases)，并下载适用版本的 tgz 包。

如：请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases)，并下载适用版本的 tgz 包。（删除）

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/<库名>@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/<库名>@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
// react-native-safe-area-context 为例
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

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-oh-tpl/<Package_Name>": "file:../../node_modules/@react-native-oh-tpl/<Package_Name>/harmony/<xxx>.har"
    // 提示: "@react-native-oh-tpl/react-native-safe-area-context": "file:../../node_modules/@react-native-oh-tpl/react-native-safe-area-context/harmony/safe_area.har"（删除）
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

### 配置 CMakeLists 和引入 xxxPackge

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

**提示：ArkTs 侧引入 Fabric 组件**（删除）

### 在 ArkTs 侧引入 xxx 组件（若需要运行 ArkTs 版本）

> [!WARNING] Deprecated！该库已接入 CAPI。（若已经 CAPI 化则需要加上这行）

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { SAFE_AREA_VIEW_TYPE, SafeAreaView, SAFE_AREA_PROVIDER_TYPE, SafeAreaProvider } from "@react-native-oh-tpl/react-native-safe-area-context"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+ if (ctx.componentName === SAFE_AREA_VIEW_TYPE) {
+   SafeAreaView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+     buildCustomComponent: buildCustomRNComponent
+   })
+ }
...
}
...
```

**提示：TurboModule**（删除）

### 在 ArkTs 侧引入 xxx Package

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

## 约束与限制

### 兼容性

**已发 Releases 的库**（删除）

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<xxx> Releases](https://github.com/<仓库地址>/releases)

提示：[@react-native-oh-tpl/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases)（删除）

**未发 Releases 使用原库的库**（删除）

本文档内容基于以下版本验证通过：

(示例)

1. RNOH: 0.72.11; SDK: OpenHarmony(api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;

### 权限要求（如有）

（填入相关权限配置）

**以下属性、静态方法、API 需要检查说明中手机平台描述，例如已支持鸿蒙的接口并且说明中提到 ios 和 android，那么需要检查是否补充 harmony 进到描述中。示例如下（删除）**

```
// 原描述
Needed for Android to work properly with assets, iOS will ignore it.
// 修改后
Needed for Android and harmony to work properly with assets, iOS will ignore it.
```

（删除）

## 属性（如有）

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 静态方法（如有）

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## API（如有，一般是 TurboModules）

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 遗留问题

- [ ] xxx 问题: [issue#\*\*\*](https://github.com/issue地址1)
- [ ] yyy 问题: [issue#\*\*\*](https://github.com/issue地址2)

## 其他

## 开源协议

本项目基于 [XXX License (XXX)](https://github.com/xxx/xxx/blob/main/LICENSE.md) ，请自由地享受和参与开源。

例子：本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。(删除)
