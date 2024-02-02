> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-native-community/progress-bar-android</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-progress-view/progress-bar-android">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-progress-view/progress-bar-android/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/progress-bar-android)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/progress-bar-android Releases](https://github.com/react-native-oh-library/progress-bar-android/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **yarn**

```bash
yarn add @react-native-oh-tpl/progress-bar-android@file:#
```

#### **npm**

```bash
npm install @react-native-oh-tpl/progress-bar-android@file:#
```

<!-- tabs:end -->

快速使用：

>[!WARNING] 使用时 import 的库名不变。

```js
 import {ProgressBar} from '@react-native-community/progress-bar-android';

<ProgressBar styleAttr="Horizontal" indeterminate={true} animating={true}  />
<ProgressBar  indeterminate={true}/>
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
  	"rnoh-progress-bar-android": "file:../../node_modules/@react-native-oh-tpl/progress-bar-android/harmony/progress_bar_android.har"
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
  	"rnoh-progress-bar-android": "file:../../node_modules/@react-native-oh-tpl/progress-bar-android/harmony/progress_bar_android"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 ProgressBarAndroidPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-progress-bar-android/src/main/cpp" ./progress-bar-android)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_progress_bar_android)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ProgressBarAndroidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ProgressBarAndroidPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 ProgressBarAndroid 组件

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
+ import { ProgressBarAndroid,PROGRESS_BAR_TYPE } from "rnoh-progress-bar-android"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName == PROGRESS_BAR_TYPE){
+     ProgressBarAndroid({
+       ctx: ctx.rnohContext,
+       tag: ctx.tag,
+     buildCustomComponent: CustomComponentBuilder
+     })
+   }
 ...
}
...
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/progress-bar-android Releases](https://github.com/react-native-oh-library/progress-bar-android/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Inherits [View Props](https://reactnative.dev/docs/view#props).

| Name            | Description                                                                                                                                                | Type                                                                                                                       | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- |
| `animating`     | Whether to show the ProgressBar (true, the default) or hide it (false).                                                                             | bool                                                                                                                       | No       | Android  | yes      |
| `color`         | Color of the progress bar.                                                                                                                          | [color](https://reactnative.dev/docs/colors)                                                                               | No       | Android  | yes      |
| `indeterminate` | If the progress bar will show indeterminate progress. Note that this can only be false if styleAttr is Horizontal, and requires a `progress` value. | indeterminateType                                                                                                          | No       | Android  | yes      |
| `progress`      | The progress value (between 0 and 1).                                                                                                               | number                                                                                                                     | No       | Android  | yes      |
| `styleAttr`     | Style of the ProgressBar.                                                                                                                           | One of:<br />Horizontal <br />Normal (default) <br />Small <br />Large <br />Inverse <br />SmallInverse <br />LargeInverse | No       | Android  | yes      |

## 遗留问题

- [x] styleAttr 为 Horizontal 时无法铺满全屏 [issues#4](https://github.com/react-native-oh-library/progress-bar-android/issues/4)。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-progress-view/progress-bar-android/blob/master/LICENSE) ，请自由地享受和参与开源。