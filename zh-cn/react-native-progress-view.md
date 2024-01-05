> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>@react-native-community/progress-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-progress-view/progress-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-progress-view/progress-view/blob/main/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-progress-view/progress-view.svg" alt="License" />
    </a>
</p>

## 安装与使用

> [!tip] 目前部分 React-Native-OpenHarmony(RNOH) 三方库的 npm 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```bash
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

<!-- tabs:start -->

**正在 npm 发布中，当前请先从仓库[Release](https://github.com/react-native-oh-library/react-native-svg/releases)中获取库 tgz，通过使用本地依赖来安装本库。**

#### **yarn**

```bash
yarn add @react-native-community/progress-view@npm:@react-native-oh-library/progress-view
```

#### **npm**

```bash
npm install @react-native-community/progress-view@npm:@react-native-oh-library/progress-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import {ProgressView} from '@react-native-community/progress-view';

<ProgressView
          progressTintColor="orange"
          trackTintColor="blue"
          progress={0.7}
/>
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
    "rnoh-progress-view": "file:../../node_modules/@react-native-community/progress-view/harmony/progress_view.har"
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
    "rnoh-progress-view": "file:../../node_modules/@react-native-community/progress-view/harmony/progress-view"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 ProgressViewPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-progress-view/src/main/cpp" ./progress-view)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh-progress-view)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ProgressViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ProgressViewPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 ProgressViewPackage 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
...
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
+ import { RNCProgressView, PROGRESS_VIEW_TYPE } from "rnoh-picker"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === PROGRESS_VIEW_TYPE) {
+   RNCProgressView({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag,
+     buildCustomComponent: CustomComponentBuilder
+   })
+ }
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/progress-view Releases](https://github.com/react-native-oh-library/progress-view/releases)

## 属性

| Name                | Description                                | Type          | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| `progress`          | The progress value (between 0 and 1).      | number        | No       | All      | yes               |
| `progressTintColor` | The tint color of the progress bar itself. | string        | No       | All      | yes               |
| `trackTintColor`    | The tint color of the progress bar track.  | string        | No       | All      | yes               |

## 遗留问题

- [ ] 部分接口，未适配

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/progress-view/blob/harmony/LICENSE) ，请自由地享受和参与开源。
