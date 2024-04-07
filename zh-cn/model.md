# 文档模板(删除)

> [!ATTENTION] 使用模板时请将后面带有 (删除) 的语句删除。<>内是需要修改的内容。(删除)

> 模板版本：v0.1.3

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

> [!TIP] [Github 地址](https://github.com/<源码仓地址>)

如：[Github 地址](https://github.com/react-native-oh-library/react-native-linear-gradient)（已建仓的地址，未建仓则使用原库地址）（删除）

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/<库名> Releases](https://github.com/<仓库地址>/releases)，并下载适用版本的 tgz 包。

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
// linear-gradient 为例
import LinearGradient from "react-native-linear-gradient";

// Within your render function
<LinearGradient
  colors={["#4c669f", "#3b5998", "#192f6a"]}
  style={styles.linearGradient}
>
  <Text style={styles.buttonText}>Sign in with Facebook</Text>
</LinearGradient>;

// Later on in your styles..
var styles = StyleSheet.create({
  linearGradient: {
    flex: 1,
    paddingLeft: 15,
    paddingRight: 15,
    borderRadius: 5,
  },
  buttonText: {
    fontSize: 18,
    fontFamily: "Gill Sans",
    textAlign: "center",
    margin: 10,
    color: "#ffffff",
    backgroundColor: "transparent",
  },
});
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
    "rnoh-xxx": "file:../../node_modules/@react-native-oh-tpl/<Package_Name>/harmony/<xxx>.har"
    // 提示: （公仓）"rnoh-linear-gradient": "file:../../node_modules/@react-native-oh-tpl/react-native-linear-gradient/harmony/linear_gradient.har"（删除）
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
    "rnoh-xxx": "file:../../node_modules/@react-native-oh-tpl/<Package_Name>/harmony/<xxx>"
    // 提示: （公仓）"rnoh-linear-gradient": "file:../../node_modules/@react-native-oh-tpl/react-native-linear-gradient/harmony/linear_gradient"（删除）
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 xxxPackge

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-linear-gradient/src/main/cpp" ./linear-gradient)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_linear_gradient)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "LinearGradientPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<LinearGradientPackage>(ctx)
    };
}
```

**提示：Fabric 组件**（删除）

### 在 ArkTs 侧引入 xxx 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { RNLinearGradient, LINEAR_GRADIENT_TYPE, LinearGradientDescriptor } from "rnoh-linear-gradient"

  @Builder
  function buildCustomComponent(ctx: ComponentBuilderContext) {
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnComponentContext,
        tag: ctx.tag,
        buildCustomComponent: buildCustomComponent
      })
    }
+   else if (ctx.componentName === LINEAR_GRADIENT_TYPE) {
+     RNLinearGradient({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomComponent
+     })
+   }
    ...
  }
  ...
```

**提示：TurboModule**（删除）

### 在 ArkTs 侧引入 xxx Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
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

## 约束与限制

### 兼容性

**已发包的库**（删除）

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<xxx> Releases](https://github.com/<仓库地址>/releases)

提示：[@react-native-oh-tpl/linear-gradient releases](https://github.com/react-native-oh-library/react-native-linear-gradient/releases)（删除）

**未发包使用原库的库**（删除）

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

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
