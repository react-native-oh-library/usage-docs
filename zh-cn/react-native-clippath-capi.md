<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-clippath(CAPI)</code> </h1>
</p>
<p align="center">
 <a href="https://github.com/Only-IceSoul/react-native-clippath">
        <img src="https://img.shields.io/badge/platforms-ios%20%7C%20android%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-clippath/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-clippath/tree/capi)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-clippathview Releases](https://github.com/react-native-oh-library/react-native-clippath/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-clippathview@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-clippathview@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import { View, Text, ScrollView } from "react-native";
import React from "react";
import { ClipPathView } from "react-native-clippathview";

export default function index() {
  const viewBox = [0, 0, 400, 400];
  const path = "M 0 0 L 400 0 L 0 400 L 400 400 Z";

  return (
    <ScrollView style={{ width: "100%", height: "100%" }}>
      <ClipPathView d={path} style={{ backgroundColor: "#ff0" }}>
        <Text style={{ height: 800, fontSize: 26 }}>
          MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
        </Text>
      </ClipPathView>
    </ScrollView>
  );
}
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-clippathview": "file:../../node_modules/@react-native-oh-tpl/react-native-clippathview/harmony/clipPath.har",
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


### 配置 CMakeLists 和引入 ClipPathViewPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-clippathview/src/main/cpp" ./clippath)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_clip_path )
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ClipPathViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ClipPathViewPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 ClipPathPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ClipPathPackage } from '@react-native-oh-tpl/react-native-clippathview/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ClipPathPackage(ctx),
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-clippathview Releases](https://github.com/react-native-oh-library/react-native-clippath/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                                                                    | Type              | Required | Platform    | HarmonyOS Support |
| -------------------- | -------------------------------------------------------------------------------------------------------------- | ----------------- | -------- | ----------- | ----------------- |
| svgKey               | 唯一 key                                                                                                       | string            | No       | Web | No               |
| d                    | 形状由一系列命令定义（svg path data）                                                                          | string            | No       | iOS/Android | Yes               |
| viewBox              | 定义用户空间中的位置和维度                                                                                     | Array<Number>(4)  | No       | iOS/Android | Yes               |
| align                | preserveAspectRatio 属性的 align                                                                               | string            | No       | iOS/Android | Yes                |
| aspect               | preserveAspectRatio 属性的 meetOrSlice                                                                         | meet/slice/none   | No       | iOS/Android | Yes                |
| fillRule             | 路径内部填充规则                                                                                               | nonzero/evenodd   | No       | iOS/Android | Yes                |
| strokeWidth          | 路径描边宽度                                                                                                   | number            | No       | iOS/Android | Yes               |
| strokeCap            | 开放路径两端的形状                                                                                             | butt/round/square | No       | iOS/Android | Yes               |
| strokeJoin           | 路径转角处使用的形状                                                                                           | bevel/miter/round | No       | iOS/Android | Yes               |
| strokeMiter          | strokeJoin 值是 miter，设置夹角延伸                                                                            | number            | No       | iOS/Android | Yes               |
| strokeStart          | iOS CAShapeLayer 描线开始的地方占总路径的百分比。默认值是 0。                                                  | number            | No       | iOS/Android | Yes                |
| strokeEnd            | iOS CAShapeLayer 表示绘制结束的地方站总路径的百分比。默认值是 1，如果小于等于 strokeStart 则绘制不出任何内容。 | number            | No       | iOS/Android | Yes                |
| translateZ           | 设置定位层级，相当于 index                                                                                     | number            | No       | iOS/Android | Yes               |
| transX               | 在二维平面上水平方向移动元素                                                                                   | number            | No       | iOS/Android | Yes               |
| transY               | 在二维平面上垂直方向移动元素                                                                                   | number            | No       | iOS/Android | Yes               |
| transPercentageValue | transX、transY 使用百分比                                                                                      | boolean           | No       | iOS/Android | Yes               |
| rot                  | 元素围绕一个定点旋转                                                                                           | number            | No       | iOS/Android | Yes               |
| rotOx                | 旋转中心点水平位置                                                                                             | number            | No       | iOS/Android | Yes               |
| rotOy                | 旋转中心点垂直位置                                                                                             | number            | No       | iOS/Android | Yes               |
| rotPercentageValue   | rotOx、rotOy 使用百分比                                                                                        | boolean           | No       | iOS/Android | Yes               |
| sc                   | 放大或缩小元素                                                                                                 | number            | No       | iOS/Android | Yes               |
| scX                  | 水平缩放                                                                                                       | number            | No       | iOS/Android | Yes               |
| scY                  | 垂直缩放                                                                                                       | number            | No       | iOS/Android | Yes               |
| scO                  | 缩放中心点位置                                                                                                 | number            | No       | iOS/Android | Yes               |
| scOx                 | 缩放中心点水平位置                                                                                             | number            | No       | iOS/Android | Yes               |
| scOy                 | 缩放中心点垂直位置                                                                                             | number            | No       | iOS/Android | Yes               |
| scPercentageValue    | scO、scOx、scOy 使用百分比                                                                                     | boolean           | No       | iOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-clippath/blob/capi/LICENSE) ，请自由地享受和参与开源。

---

<!-- {% endraw %} -->