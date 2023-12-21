> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-linear-gradient/react-native-linear-gradient">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

**正在 npm 发布中，当前请先从仓库[Release](https://github.com/react-native-oh-library/react-native-linear-gradient/releases)中获取库 tgz，通过使用本地依赖来安装本库。**

#### **yarn**

```bash
yarn add xxx
```

#### **npm**

```bash
npm install xxx
```

<!-- tabs:end -->

快速使用：

```js
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
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-linear-gradient": "file:../../node_modules/react-native-linear-gradient/harmony/linear_gradient.har"
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
    "rnoh-linear-gradient": "file:../../node_modules/react-native-linear-gradient/harmony/linear_gradient"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 LinearGradientPackage

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

### 在 ArkTs 侧引入 linear-gradient 组件

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
+ import { RNLinearGradient, LINEAR_GRADIENT_TYPE, LinearGradientDescriptor } from "rnoh-linear-gradient"

  @Builder
  function CustomComponentBuilder(ctx: ComponentBuilderContext) {
    if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnohContext,
        tag: ctx.descriptor.tag,
        buildCustomComponent: CustomComponentBuilder
      })
    }
+   else if (ctx.descriptor.type === LINEAR_GRADIENT_TYPE) {
+     RNLinearGradient({
+       ctx: ctx.rnohContext,
+       tag: ctx.descriptor.tag,
+       buildCustomComponent: CustomComponentBuilder
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-linear-gradient Releases](https://github.com/react-native-oh-library/react-native-linear-gradient/releases)

## 属性

| 名称        | 说明                                                     | 类型                   | 是否必填 | 原库平台 | 鸿蒙支持 |
| ----------- | -------------------------------------------------------- | ---------------------- | -------- | -------- | -------- |
| colors      | Color Array                                              | (string\|number)[]     | NO       | All      | yes      |
| locations   | Color for unknown array (length 0 or the same as colors) | number[]               | NO       | All      | yes      |
| useAngle    | Use angle (default false)                                | boolean                | NO       | All      | yes      |
| angle       | Angle (useAngle=true valid)                              | number                 | NO       | All      | yes      |
| angleCenter | Middle angle coordinate                                  | { x: number,y: number} | NO       | All      | no       |
| start       | Starting point coordinates (default value: {x: 0.5,1})   | { x: number,y: number} | NO       | All      | partial  |
| end         | End point coordinates (default value: {x: 0.5,1})        | { x: number,y: number} | NO       | All      | partial  |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE) ，请自由地享受和参与开源。
