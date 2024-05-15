> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-svg(CAPI)</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-svg">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-svg/blob/main/LICENSE">
        <img src="https://img.shields.io/npm/l/react-native-svg.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-harmony-svg)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-svg Releases](https://github.com/react-native-oh-library/react-native-harmony-svg/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-svg@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-svg@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import Svg, { Path } from "react-native-svg";

<Svg width="100" height="100">
  <Path d="M90 0 L0 180 L180 180 Z" fill="red" />
</Svg>;
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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/svg": "file:../../node_modules/@react-native-oh-tpl/react-native-svg/harmony/svg.har"
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

把 `tester/node_modules/@react-native-oh-tpl/react-native-svg/harmony/` 目录下的源码 `svg` 复制到 `harmony` 工程根目录下

在`harmony`工程根目录的 `build-profile.template.json5(若有)` 和 `build-profile.json5` 添加以下模块

```json
modules:[
  ...
  {
    name: 'svg',
    srcPath: './svg',
  }
]
```

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/svg": "file:../svg"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install
```

### 配置 CMakeLists 和引入 SVGPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-svg/src/main/cpp" ./svg)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_svg)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SVGPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SVGPackage>(ctx),
    };
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-svg Releases](https://github.com/react-native-oh-library/react-native-harmony-svg/releases)

## 属性

详细请查看 [react-native-svg 的文档介绍](https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md)

以下为目前已支持的组件属性：

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Svg**：绘制组件的父组件

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
|  width  |  组件宽度   | number\| string | Yes      | All      | Yes               |
| height  |  组件高度   | number\| string | Yes      | All      | Yes               |
| viewBox |  组件视区   |     string      | No       | All      | Yes               |
|  color  |    颜色     |     string      | No       | All      | Yes               |

**G**：该元素是用于对其他 SVG 元素进行分组的容器

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | -------- | -------- | ----------------- |

**Path**： 路径绘制组件，根据绘制路径生成封闭的自定义形状

|  Name   |     Description      |  Type  | Required | Platform | HarmonyOS Support |
| :-----: | :------------------: | :----: | -------- | -------- | ----------------- |
|    d    | 路径绘制的命令字符串 | string | Yes      | All      | Yes               |
| opacity |        透明度        | number | No       | All      | Yes               |

**Rect**： 矩形绘制组件，根据角位置和宽高生成矩形形状

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | Yes      | All      | Yes               |
| height |     元素高度      | number\| string | Yes      | All      | Yes               |
|   rx   | 定义 x 轴上的半径 | number\| string | No       | All      | Yes               |
|   ry   | 定义 y 轴上的半径 | number\| string | No       | All      | Yes               |

**Image**： 图像元素，支持 JPEG、PNG 格式

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | Yes      | All      | Yes               |
| height |     元素高度      | number\| string | Yes      | All      | Yes               |
|  href  |   图像资源引用    | source\| string | Yes      | All      | Yes               |

**Circle**： 园绘制组件，基于圆心和半径生成园形形状

|  Name   |      Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :-------------------: | :-------------: | -------- | -------- | ----------------- |
|    r    |        园半径         | number\| string | Yes      | All      | Yes               |
|   cx    | 圆心在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   cy    | 圆心在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| opacity |        透明度         |     number      | No       | All      | Yes               |

**Polygon**： 多边形制组件，用于创建至少包含三条边的图形

|  Name   |          Description           |      Type      | Required | Platform | HarmonyOS Support |
| :-----: | :----------------------------: | :------------: | -------- | -------- | ----------------- |
| points  | 定义多边形每个角的 x 和 y 坐标 | string\| array | Yes      | All      | Yes               |
| opacity |             透明度             |     number     | No       | All      | Yes               |

**Polyline**： 多段线组件，用于创建一条线段构成的轨迹

|  Name   |           Description            |      Type      | Required | Platform | HarmonyOS Support |
| :-----: | :------------------------------: | :------------: | -------- | -------- | ----------------- |
| points  | 定义多段线每个端点的 x 和 y 坐标 | string\| array | Yes      | All      | Yes               |
| opacity |              透明度              |     number     | No       | All      | Yes               |

**Defs**：该元素是用于对其他 SVG 元素进行分组的容器
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------: | :-------------: | -------- | -------- | ----------------- |
| / | / | / | / | All | Yes |

**LinearGradient**：用于定义线性渐变

> [!tip] 注： LinearGradient 目前仅支持 Path、Rect、Circle 组件，只支持在 fill 上使用，不支持 stroke

|       Name        |              Description               |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        x1         |           在 x 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        y1         |           在 y 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        x2         |           在 x 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        y2         |           在 y 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|   gradientUnits   |        指定元素属性使用的坐标系        | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | 指定从元素当前坐标系到目标坐标系的转换 |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**RadialGradient**：用于定义线性渐变

> [!tip] 注： RadialGradient 目前仅支持 Path、Rect、Circle 组件，只支持在 fill 上使用，不支持 stroke

|       Name        |              Description               |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        fx         |           起始圆的 x 轴坐标            |             number\| string             | No       | All      | Yes               |
|        fy         |           起始圆的 y 轴坐标            |             number\| string             | No       | All      | Yes               |
|        rx         |          终止椭圆的 x 轴半径           |             number\| string             | No       | All      | Yes               |
|        ry         |          终止椭圆的 y 轴半径           |             number\| string             | No       | All      | Yes               |
|        cx         |           终止圆的 x 轴坐标            |             number\| string             | No       | All      | Yes               |
|        cy         |           终止圆的 y 轴坐标            |             number\| string             | No       | All      | Yes               |
|         r         |              终止圆的半径              |             number\| string             | No       | All      | Yes               |
|   gradientUnits   |        指定元素属性使用的坐标系        | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | 指定从元素当前坐标系到目标坐标系的转换 |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**Stop**：定义渐变上的颜色坡度

|    Name     |         Description          |      Type       | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------: | :-------------: | -------- | -------- | ----------------- |
|  stopColor  |        渐变停止的颜色        |     string      | No       | All      | Yes               |
| stopOpacity |      渐变停止的不透明度      | number\| string | No       | All      | Yes               |
|   offset    | 渐变停止沿渐变向量放置的位置 | number\| string | No       | All      | Yes               |

**Mask**：定义 alpha 蒙版，用于将当前对象合成到背景中

|       Name       | Description                                                                                                | Type       | Required | Platform | HarmonyOS Support |
| :--------------: | ---------------------------------------------------------------------------------------------------------- | ---------- | -------- | -------- | :---------------: |
|        id        | 唯一标识                                                                                                   | string     | No       | All      |        Yes        |
|        x         | 左侧顶角横坐标                                                                                             | NumberProp | No       | All      |        Yes        |
|        y         | 左侧顶角纵坐标                                                                                             | NumberProp | No       | All      |        Yes        |
|      width       | 元素宽度                                                                                                   | NumberProp | No       | All      |        Yes        |
|      height      | 元素高度                                                                                                   | NumberProp | No       | All      |        Yes        |
|    maskUnits     | 定义 x,y,width,height 使用的坐标系，默认值为 objectBoundingBox，可以使用 objectBoundingBox\|userSpaceOnUse | TMaskUnits | No       | All      |        Yes        |
| maskContentUnits | 定义内容使用的坐标系，默认值为 userSpaceOnUse，可以使用 objectBoundingBox\|userSpaceOnUse                  | TMaskUnits | No       | All      |        Yes        |

**Use**：该元素可以重复使用 SVG 元素

|  Name  |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|   x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
| width  |     元素宽度      | number\| string | No       | All      | Yes               |
| height |     元素高度      | number\| string | No       | All      | Yes               |
|  href  |   图像资源引用    | source\| string | Yes      | All      | Yes               |

**Ellipse**： 椭圆绘制组件，基于一个中心坐标以及它们的 x 半径和 y 半径

| Name |      Description      |      Type       | Required | Platform | HarmonyOS Support |
| :--: | :-------------------: | :-------------: | -------- | -------- | ----------------- |
|  cx  | 圆心在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|  cy  | 圆心在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
|  rx  |   定义 x 轴上的半径   | number\| string | No       | All      | Yes               |
|  ry  |   定义 y 轴上的半径   | number\| string | No       | All      | Yes               |

**Symbol**： 该元素用来定义一个图形模板对象，它可以用一个<use>元素实例化

|        Name         |     Description      |  Type  | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :----: | -------- | -------- | ----------------- |
| preserveAspectRatio | 是否强制进行统一缩放 | string | No       | All      | Yes               |
|       viewBox       |       组件视区       | string | No       | All      | Yes               |

**ClipPath**：该元素定义一条剪切路径，可作为其他元素的 clipPath 属性的值
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------: | :-------------: | -------- | -------- | ----------------- |
| / | / | / | / | All | Yes |

**Marker**：用于在绘制类组件上添加标记

|        Name         |                      Description                       |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                  为元素分配唯一的名称                  |     string      | Yes      | All      | Yes               |
|       viewBox       |              视窗在用户空间中的位置和尺寸              |     string      | No       | All      | Yes               |
| preserveAspectRatio |                  是否强制进行统一缩放                  |     string      | No       | All      | Yes               |
|        refX         |                  标记参考点的 x 坐标                   | number\| string | No       | All      | Yes               |
|        refY         |                  标记参考点的 y 坐标                   | number\| string | No       | All      | Yes               |
|     markerUnits     | markerWidth 和 markerHeight 属性的坐标系以及标记的内容 |     string      | No       | All      | Yes               |
|       orient        |         将标记放置在形状上的相应位置时如何旋转         |     string      | No       | All      | Yes               |
|     markerWidth     |                表示标记进入的视窗的宽度                | number\| string | No       | All      | Yes               |
|    markerHeight     |                表示标记进入的视窗的高度                | number\| string | No       | All      | Yes               |

**公共属性**：Common props 组件属性鸿蒙侧支持情况

|    Name     |             Description              |  Type  | Default | Required | Platform | G   | Path | Rect | Circle | Polygon |
| :---------: | :----------------------------------: | :----: | :-----: | :------: | -------- | --- | ---- | ---- | ------ | ------- |
|    fill     |           设置填充区域颜色           | string | '#000'  |    No    | All      |     | √    | √    | √      | √       |
|   stroke    | 设置边框颜色，不设置时，默认没有边框 | string | 'none'  |    No    | All      |     | √    | √    | √      | √       |
| strokeWidth |             设置边框宽度             | number |    1    |    No    | All      |     | √    | √    | √      | √       |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE) ，请自由地享受和参与开源。
