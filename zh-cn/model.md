# 文档模板(删除)

> [!ATTENTION] 使用模板时请将后面带有 (删除) 的语句删除。(删除)

> 模板版本：v0.0.1

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

## 安装与使用

提示：根据 npm 包部署地方不同选用不同模板：私仓 or 公仓（删除）

### 提示：私仓（删除）

> [!tip] 目前部分 React-Native-OpenHarmony(RNOH) 三方库的 NPM 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```bash
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add <原库 npm 包名>@npm:@react-native-oh-library/<xxx>
// 提示：yarn add @react-native-community/slider@npm:@react-native-oh-library/slider（删除）
// 提示：yarn add react-native-translucent-modal@npm:@react-native-oh-library/（删除）react-native-translucent-modal
```

#### **npm**

```bash
npm install <原库 npm 包名>@npm:@react-native-oh-library/<xxx>
// 提示：npm install @react-native-community/slider@npm:@react-native-oh-library/slider（删除）
// 提示：npm install react-native-translucent-modal@npm:@react-native-oh-library/react-native-translucent-modal（删除）
```

<!-- tabs:end -->

### 提示：公仓（删除）

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add <原库 npm 包名>@npm:@react-native-oh-tpl/<xxx>
// 提示：yarn add @shopify/flash-list@npm:@react-native-oh-tpl/flash-list（删除）
// 提示：yarn add react-native-linear-gradient@npm:@react-native-oh-tpl/react-native-linear-gradient（删除）
```

#### **npm**

```bash
npm install <原库 npm 包名>@npm:@react-native-oh-tpl/<xxx>
// 提示：npm install @shopify/flash-list@npm:@react-native-oh-tpl/flash-list（删除）
// 提示：npm install react-native-linear-gradient@npm:@react-native-oh-tpl/react-native-linear-gradient（删除）
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
// Slider 为例
import Slider from "@react-native-community/slider";

<Slider
  style={{ width: 200, height: 40 }}
  minimumValue={0}
  maximumValue={1}
  minimumTrackTintColor="#FFFFFF"
  maximumTrackTintColor="#000000"
/>;
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
    "rnoh-xxx": "file:../../node_modules/<原库 npm 包名>/harmony/<xxx>.har"
    // 提示: (私仓)"rnoh-slider": "file:../../node_modules/@react-native-community/slider/harmony/slider.har"（删除）
    // 提示: （公仓）"rnoh-linear-gradient": "file:../../node_modules/react-native-linear-gradient/harmony/linear_gradient.har"（删除）
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
    "rnoh-xxx": "file:../../node_modules/<原库 npm 包名>/harmony/<xxx>"
    // 提示: (私仓)"rnoh-slider": "file:../../node_modules/@react-native-community/slider/harmony/slider"（删除）
    // 提示: （公仓）"rnoh-linear-gradient": "file:../../node_modules/react-native-linear-gradient/harmony/linear_gradient"（删除）
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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-slider/src/main/cpp" ./slider)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_slider)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SliderPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SliderPackage>(ctx)
    };
}
```

**提示：Fabric 组件**（删除）

### 在 ArkTs 侧引入 xxx 组件

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
+ import { RNCSlider, SLIDER_TYPE } from "rnoh-slider"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === SLIDER_TYPE) {
+   RNCSlider({
+     ctx: ctx.rnohContext,
+     tag: ctx.descriptor.tag,
+     buildCustomComponent: CustomComponentBuilder
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<xxx> Releases](https://github.com/<仓库地址>/releases)

提示：[@react-native-oh-library/slider releases](https://github.com/react-native-oh-library/react-native-slider/releases)（删除）

## 属性（如有）

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |

## 静态方法（如有）

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |

## API（如有，一般是 TurboModules）

| 名称 | 说明 | 类型 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---- | ---- | ---- | -------- | -------- | -------- |

## 遗留问题

- [ ] xxx 问题: [issue#\*\*\*](https://github.com/issue地址1)
- [ ] yyy 问题: [issue#\*\*\*](https://github.com/issue地址2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。
