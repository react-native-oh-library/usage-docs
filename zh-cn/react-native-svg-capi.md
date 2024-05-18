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

### 在 ArkTs 侧引入 SvgPackage (注册TurboModule)

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { SvgPackage } from '@react-native-oh-tpl/react-native-svg/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SvgPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-svg Releases](https://github.com/react-native-oh-library/react-native-harmony-svg/releases)

## 属性

详细请查看 [react-native-svg 的文档介绍](https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md)

以下为目前已支持的组件属性：

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Svg**：绘制组件的父组件

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|        width        |       组件宽度       | number\| string |   Yes    |   All    |        Yes        |
|       height        |       组件高度       | number\| string |   Yes    |   All    |        Yes        |
|       viewBox       |       组件视区       |     string      |    No    |   All    |        Yes        |
|        color        |         颜色         |     string      |    No    |   All    |        Yes        |
|        title        |      组件标题名      |     string      |    No    |   All    |        Yes        |
| preserveAspectRatio | 是否强制进行统一缩放 |     string      |    No    |   All    |        Yes        |

**G**：该元素是用于对其他 SVG 元素进行分组的容器

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
| opacity |   透明度    | number\| string | No       | All      | Yes               |

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
| :--: | :---------: | :--: | -------- | -------- | ----------------- |
|  /   |      /      |  /   | /        | All      | Yes               |

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

|    Name     |  Description   |  Type  | Required | Platform | HarmonyOS Support |
| :---------: | :------------: | :----: | -------- | -------- | ----------------- |
|  stopColor  |     渐变色     | string | No       | All      | Yes               |
| stopOpacity |  渐变色透明度  | string | No       | All      | Yes               |
|   offset    | 渐变色相对位置 | string | No       | All      | Yes               |

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
| :--: | :---------: | :--: | -------- | -------- | ----------------- |
|  /   |      /      |  /   | /        | All      | Yes               |

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

**Pattern**：用于定义一个图形对象，可以被引用以平铺重绘该图形对象以覆盖某个区域。

|        Name         |                                Description                                |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :-----------------------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                           为元素分配唯一的名称                            |     string      | Yes      | All      | Yes               |
|          x          |                            标记参考点的 x 坐标                            | number\| string | No       | All      | Yes               |
|          y          |                            标记参考点的 y 坐标                            | number\| string | No       | All      | Yes               |
|        width        |                         表示标记进入的视窗的宽度                          | number\| string | No       | All      | Yes               |
|       height        |                         表示标记进入的视窗的高度                          | number\| string | No       | All      | Yes               |
|    patternUnits     |              属性指示 pattern 元素的几何属性使用哪个坐标系。              |     string      | No       | All      | Yes               |
| patternContentUnit  |              属性指示 pattern 元素的几何属性使用哪个坐标系。              |     string      | No       | All      | Yes               |
|  patternTransform   |                   定义了应用于图案图块的变换定义的列表                    |     string      | No       | All      | Yes               |
|       viewBox       |                     定义视窗在用户空间中的位置和尺寸                      |     string      | No       | All      | Yes               |
| preserveAspectRatio | 指示具有提供给定宽高比的 viewBox 的元素必须如何适应具有不同宽高比的视口。 |     string      | No       | All      | Yes               |

**Symbol**：用于定义可由 use 元素实例化的图形模板对象。

|        Name         |                                Description                                |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :-----------------------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                           为元素分配唯一的名称                            |     string      | Yes      | All      | Yes               |
|       viewBox       |                     定义视窗在用户空间中的位置和尺寸                      |     string      | No       | All      | Yes               |
| preserveAspectRatio | 指示具有提供给定宽高比的 viewBox 的元素必须如何适应具有不同宽高比的视口。 |     string      | No       | All      | Yes               |
|       opacity       |      指定一个对象或一组对象的透明度，即元素后面的背景被覆盖的程度。       | number\| string | No       | All      | Yes               |

**Line**：SVG 基本形状，用于创建连接两点的线。

|  Name   |   Description    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :--------------: | :-------------: | -------- | -------- | ----------------- |
|   x1    | x 轴上线条的起点 | number\| string | No       | All      | Yes               |
|   y1    | y 轴上的线的起点 | number\| string | No       | All      | Yes               |
|   x2    | x 轴上的线的末端 | number\| string | No       | All      | Yes               |
|   y2    | y 轴上的线的末端 | number\| string | No       | All      | Yes               |
| opacity |      透明度      | number\| string | No       | All      | Yes               |

**Text**：绘制由文本组成的图形元素

|    Name    |           Description            |      Type       | Required | Platform | HarmonyOS Support |
| :--------: | :------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x      |      文本基线起点的 x 坐标       |  number\string  | No       | All      | Yes               |
|     y      |      文本基线起点的 y 坐标       |  number\string  | No       | All      | Yes               |
|     dx     | 从前一个文本元素水平移动文本位置 |  number\string  | No       | All      | Yes               |
|     dy     | 从前一个文本元素垂直移动文本位置 | number\| string | No       | All      | Yes               |
|   rotate   |      旋转每个单独字形的方向      |      array      | No       | All      | Yes               |
|  opacity   |              透明度              |     number      | No       | All      | Yes               |
| inlineSize |          水平或垂直尺寸          |     number      | No       | All      | Yes               |

**TSpan**：绘制文本或 Text 内的子文本

|    Name    |           Description            |      Type       | Required | Platform | HarmonyOS Support |
| :--------: | :------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x      |      文本基线起点的 x 坐标       |  number\string  | No       | All      | Yes               |
|     y      |      文本基线起点的 y 坐标       |  number\string  | No       | All      | Yes               |
|     dx     | 从前一个文本元素水平移动文本位置 |  number\string  | No       | All      | Yes               |
|     dy     | 从前一个文本元素垂直移动文本位置 | number\| string | No       | All      | Yes               |
|   rotate   |      旋转每个单独字形的方向      |      array      | No       | All      | Yes               |
|  opacity   |              透明度              |     number      | No       | All      | Yes               |
| inlineSize |          水平或垂直尺寸          |     number      | No       | All      | Yes               |

**TextPath**：若要沿路径形状呈现文本，将文本括在具有 href 属性的 TextPath 元素中，并引用 Path 元素。

|   Name    |            Description             |  Type  | Required | Platform | HarmonyOS Support |
| :-------: | :--------------------------------: | :----: | -------- | -------- | ----------------- |
|   href    | 用于呈现文本的路径或基本形状的 URL | string | No       | All      | Yes               |
| xlinkHref | 用于呈现文本的路径或基本形状的 URL | string | No       | All      | Yes               |
|  method   |      沿路径渲染各个字形的方法      | string | No       | All      | Yes               |
|  spacing  |         绘制字符之间的间距         | string | No       | All      | Yes               |
|   side    |      文本应呈现在路径的哪一侧      | string | No       | All      | Yes               |
|  midLine  |                中线                | string | No       | All      | Yes               |

**SvgAst**：该组件通过传入 ast 来渲染出 svg

|   Name   |         Description          |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :--------------------------: | :------: | :------: | :------: | :---------------: |
|   ast    | 解析 svg 字符串得到的 ast 树 |  JsxAST  |   Yes    |   All    |        Yes        |
| override |    覆盖 svg 样式，如宽高     |  object  |    No    |   All    |        Yes        |
| onError  |          错误时触发          | function |    No    |   All    |        Yes        |
|  onLoad  |        加载成功后触发        | function |    No    |   All    |        Yes        |
| fallback |          加载中元素          | function |    No    |   All    |        Yes        |

**SvgFromUri**：该组件通过传入 uri 地址来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   uri    |     svg 资源地址      |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |
| onError  |      错误时触发       | function |    No    |   All    |        Yes        |
|  onLoad  |    加载成功后触发     | function |    No    |   All    |        Yes        |
| fallback |      加载中元素       | function |    No    |   All    |        Yes        |

**SvgFromXml**：该组件通过传入字符串来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   xml    |   svg 代码的字符串    |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |
| onError  |      错误时触发       | function |    No    |   All    |        Yes        |
|  onLoad  |    加载成功后触发     | function |    No    |   All    |        Yes        |
| fallback |      加载中元素       | function |    No    |   All    |        Yes        |

**SvgUri**：该组件通过传入 uri 地址来渲染出 svg

|   Name   |      Description      |   Type   | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :------: | :------: | :------: | :---------------: |
|   uri    |     svg 资源地址      |  string  |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 |  object  |    No    |   All    |        Yes        |
| onError  |      错误时触发       | function |    No    |   All    |        Yes        |
|  onLoad  |    加载成功后触发     | function |    No    |   All    |        Yes        |
| fallback |      加载中元素       | function |    No    |   All    |        Yes        |

**函数**

|   Name    |        Description         |   Type   | Required | Platform | HarmonyOS Support |
| :-------: | :------------------------: | :------: | :------: | :------: | :---------------: |
|   parse   | 将 svg 字符串解析成 JsxAST | function |    No    |   All    |        Yes        |
|    err    |          打印日志          | function |    No    |   All    |        Yes        |
| camelCase |    字符串首字母转成大写    | function |    No    |   All    |        Yes        |
| fetchText | 将 svg 字符串解析成 JsxAST | function |    No    |   All    |        Yes        |

**公共属性**：Common props 组件属性鸿蒙侧支持情况

|       Name       |                 Description                 |    Type     |  Default  | Required | Platform |
| :--------------: | :-----------------------------------------: | :---------: | :-------: | :------: | :------: |
|       fill       |              设置填充区域颜色               |   string    |  '#000'   |    No    |   All    |
|   fillOpacity    |             设置填充区域透明度              |   number    |     1     |    No    |   All    |
|     fillRule     |                设置填充规则                 |   number    |     1     |    No    |   All    |
|     clipRule     |                设置裁剪规则                 |   string    | 'evenodd' |    No    |   All    |
|     clipPath     |           指定、关联一条裁剪路径            |   string    |  'none'   |    No    |   All    |
|      stroke      |    设置边框颜色，不设置时，默认没有边框     |   string    |   none    |    No    |   All    |
|   strokeWidth    |                设置边框宽度                 |   number    |     1     |    No    |   All    |
|  strokeOpacity   |                 边框透明度                  |   number    |     1     |    No    |   All    |
| strokeDasharray  |         用来描边的点划线的图案范式          |   number    |   none    |    No    |   All    |
| strokeDashoffset |      指定了 dash 模式到路径开始的距离       |   number    |     1     |    No    |   All    |
|  strokeLinecap   |             设置路径两端的形状              |   string    |   butt    |    No    |   All    |
|  strokeLinejoin  |         指明路径的转角处使用的形状          |   string    |   miter   |    No    |   All    |
| strokeMiterlimit | 对斜接长度和 stroke-width 的比率设置极限 值 |   number    |     4     |    No    |   All    |
|   vectorEffect   |       指明绘制对象时要使用的矢量效果        |   string    |   none    |    No    |   All    |
|     clipRule     |            将元素进行剪切的规则             |   string    |  evenodd  |    No    |   All    |
|     clipPath     |               将元素进行剪切                |   string    |     -     |    No    |   All    |
|    translate     |                  设置位移                   | numberArray |    0,0    |    No    |   All    |
|    translateX    |                设置 x 轴位移                |   number    |     0     |    No    |   All    |
|    translateY    |                设置 y 轴位移                |   number    |     0     |    No    |   All    |
|      origin      |           更改一个元素变形的原点            | numberArray |    0,0    |    No    |   All    |
|     originX      |        更改一个元素变形的原点 x 坐标        |   number    |     0     |    No    |   All    |
|     originY      |        更改一个元素变形的原点 y 坐标        |   number    |     0     |    No    |   All    |
|      scale       |                定义缩放大小                 | numberArray |   1，1    |    No    |   All    |
|      scaleX      |              定义 x 轴缩放大小              |   number    |     1     |    No    |   All    |
|      scaleY      |              定义 y 轴缩放大小              |   number    |     1     |    No    |   All    |
|     rotation     |                设置旋转角度                 |   number    |   0，0    |    No    |   All    |
|        x         |              标识一个 x 轴坐标              |   number    |     0     |    No    |   All    |
|        y         |              标识一个 y 轴坐标              |   number    |     0     |    No    |   All    |
|    transform     |   定义应用于元素及其子元素的变换规则列表    |   string    |     -     |    No    |   All    |
|      marker      |         指定路径所有顶点的路标样式          |   string    |     -     |    No    |   All    |
|   markerStart    |        指定路径起点所采用的路标样式         |   string    |     -     |    No    |   All    |
|    markerMid     |      指定路径中间顶点所采用的路标样式       |   string    |     -     |    No    |   All    |
|    markerEnd     |        指定路径终点所采用的路标样式         |   string    |     -     |    No    |   All    |
|       mask       |    给元素指定使用 Mask 元素实现遮罩效果     |   string    |     -     |    No    |   All    |
|        id        |                 设置节点 id                 |   string    |     -     |    No    |   All    |
|     opacity      |                 设置透明度                  |   number    |     1     |    No    |   All    |
|    transform     |   定义应用于元素及其子元素的变换规则列表    |   string    |     -     |    No    |   All    |
|     display      |             控制元素展示的方式              |   string    |   block   |    No    |   All    |
|  pointerEvents   |          设置元素如何响应点击事件           |   string    |           |    No    |   All    |
|   vectorEffect   |       指明绘制对象时要使用的矢量效果        |     Int     |     0     |    No    |   All    |

FontProps 组件属性鸿蒙侧支持情况

|         Name          |                          Description                           |        Type        | Default | Required | Platform |
| :-------------------: | :------------------------------------------------------------: | :----------------: | :-----: | :------: | :------: |
|       fontSize        | 在多行布局环境中将多行文本设置为实线时，从基线到基线的字体大小 |       string       | medium  |    No    |   All    |
|      fontWeight       |   用于呈现文本的字形相对于同一字体族中的其他字体的粗度或亮度   |       string       | normal  |    No    |   All    |
|         font          |                   设置一个用于文字布局的字体                   | FontObject（对象） |  none   |    No    |   All    |
|       fontStyle       |                        指定文本渲染样式                        |       string       | normal  |    No    |   All    |
|      fontVariant      |                        设置文本字体变体                        |                    |         |    No    |   All    |
|      fontStretch      |                        控制字体拉伸程度                        |       string       | normal  |    No    |   All    |
|      fontFamily       |                          指定文本字体                          |       string       | normal  |    No    |   All    |
|      textAnchor       |               用于指定文本相对于其锚点的对齐方式               |       string       |  start  |    No    |   All    |
|    textDecoration     |                        设置文本装饰效果                        |       string       |    -    |    No    |   All    |
|     letterSpacing     |                     设置字符间距或字母间距                     |       number       |    1    |    No    |   All    |
|      wordSpacing      |                     设置英文单词之间的距离                     |       number       |    1    |    No    |   All    |
|        kerning        |                       设置字符之间的间距                       |       number       |    0    |    No    |   All    |
|  fontFeatureSettings  |                          字体特性控制                          |       string       | normal  |    No    |   All    |
| fontVariantLigatures  |                         控制文本中连字                         |       string       | normal  |    No    |   All    |
| fontVariationSettings |                 设置字体的宽度、高度、倾斜度等                 |       string       | normal  |    No    |   All    |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE) ，请自由地享受和参与开源。
