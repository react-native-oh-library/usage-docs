

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-linear-gradient/react-native-linear-gradient">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    </p>

## 安装与使用

目前 React-Native-OpenHarmony(RNOH) 三方库的npm包部署在私仓，需要通过github token来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将TOKEN替换为RNOH三方库指定的token。
```json
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

```bash
yarn add react-native-linear-gradient@npm:@react-native-oh-library/react-native-linear-gradient
```

或者

```bash
npm install react-native-linear-gradient@npm:@react-native-oh-library/react-native-linear-gradient
```

快速使用：

```js
import LinearGradient from 'react-native-linear-gradient';
  <LinearGradient
      angleCenter={{ x: 0.5, y: 0.5}}
      colors={['green', 'bule', 'red']}
      start={{x: 0, y: 0}} 
      end={{x: 1, y: 0}}
      style={styles.gradient}>
        <Text style={styles.buttonText}>1111</Text>
        <Text style={styles.buttonText}>2222</Text>
        <Text style={styles.buttonText}>3333</Text>
  </LinearGradient>
```

## Link

目前鸿蒙暂不支持 AutoLink，所以Link步骤需要手动配置。

首先需要使用DevEco Studio打开项目里的鸿蒙工程 `harmony`

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

### 配置CMakeLists和引入LinearGradientPackage

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


### 在ArkTs侧引入 linear-gradient 组件

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
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnohContext,
        tag: ctx.descriptor.tag,
        buildCustomComponent: CustomComponentBuilder
      })
    }
+   else if (ctx.componentName === LINEAR_GRADIENT_TYPE) {
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
要使用此库，需要使用正确的React-Native和RNOH版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

| `@react-native-oh-library/react-native-linear-gradient` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version    |
| ------------------------------------------------------------ | ----------------------------- | --------------------- | ------------------------------ | ----------------------- |
| 3.0.0-alpha.1-0.2.4                                          | `>=0.72.5`                    | `>=0.72.6`            | `>=4.0.3.501`                  | `>=OpenHarmony 4.10.10` |


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