> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-harmony-svg)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-svg Releases](https://github.com/react-native-oh-library/react-native-harmony-svg/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-svg@15.0.0
npm install @react-native-oh-tpl/react-native-svg
```

#### **yarn**

```bash
yarn add react-native-svg@15.0.0
yarn add @react-native-oh-tpl/react-native-svg
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, SafeAreaView } from "react-native";
import { Svg, Path } from "react-native-svg";

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <Svg width="100" height="100">
        <Path d="M90 0 L0 180 L180 180 Z" fill="red" />
      </Svg>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "grey",
  },
});
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-svg": "file:../../node_modules/@react-native-oh-tpl/react-native-svg/harmony/svg.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing SVGPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing SvgPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

### 在 ArkTs 侧引入和注册字体文件(非必选配置项)

> [!TIP] 本项非必配项，当使用 Text 组件的 fontFamily Properties 指定字体时才需配置

步骤一：
复制字体文件到 `entry/src/main/resources/rawfile/assets/fonts` 目录下(如使用了外部字体文件，需要将\*.ttf 文件复制过来)

步骤二：
打开 `entry/src/main/ets/pages/Index.ets`，添加以下代码

    const fonts: Record<string, Resource> = {
        "Noto Sans Pau Cin Hau": $rawfile("assets/fonts/Noto Sans Pau Cin Hau.ttf") ,
        "NotoSansVai-Regular": $rawfile("assets/fonts/NotoSansVai-Regular.ttf") ,
        "HarmonyOS_Sans_Condensed_Regular_Italic": $rawfile("assets/fonts/HarmonyOS_Sans_Condensed_Regular_Italic.ttf")
        "HarmonyOS_Sans_Digit_Medium": $rawfile("assets/fonts/HarmonyOS_Sans_Digit_Medium.ttf")
    }

    @Entry
    @Component
    struct Index {
        //...
        build() {
            Column(){
                //...

                //注册字体文件
                RNApp({
                rnInstanceConfig: {
                    //...
                    fontResourceByFontFamily: fonts
                },
                //...
            }

        }
        //...
    }

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-svg Releases](https://github.com/react-native-oh-library/react-native-harmony-svg/releases)

## Properties

For details, see [react-native-svg](https://github.com/software-mansion/react-native-svg/blob/main/USAGE.md)

以下为目前已支持的组件 Properties：

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**Svg**：绘制组件的父组件

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|        width        |       组件宽度       | number\| string |   Yes    |   All    |        Yes        |
|       height        |       组件高度       | number\| string |   Yes    |   All    |        Yes        |
|       viewBox       |       组件视区       |     string      |    No    |   All    |        Yes        |
|        color        |         颜色         |     string      |    No    |   All    |        Yes        |
|        title        |      组件标题名      |     string      |    No    |   All    |        Yes        |
| preserveAspectRatio | 是否强制进行统一缩放 |     string      |    No    |   All    |        Yes        |

**G**：该元素是用于对 Others SVG 元素进行分组的容器

|  Name   | Description |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------: | :-------------: | -------- | -------- | ----------------- |
| opacity |   透明度    | number\| string | No       | All      | Yes               |

**Path**： 路径绘制组件，根据绘制路径生成封闭的自定义形状

|  Name   |     Description      |  Type  | Required | Platform | HarmonyOS Support |
| :-----: | :------------------: | :----: | -------- | -------- | ----------------- |
|    d    | 路径绘制的命令字符串 | string | Yes      | All      | Yes               |
| opacity |        透明度        | number | No       | All      | Yes               |

**Rect**： 矩形绘制组件，根据角位置和宽高生成矩形形状

|  Name   |    Description    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :---------------: | :-------------: | -------- | -------- | ----------------- |
|    x    | 在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|    y    | 在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
|  width  |     元素宽度      | number\| string | Yes      | All      | Yes               |
| height  |     元素高度      | number\| string | Yes      | All      | Yes               |
|   rx    | 定义 x 轴上的半径 | number\| string | No       | All      | Yes               |
|   ry    | 定义 y 轴上的半径 | number\| string | No       | All      | Yes               |
| opacity |      透明度       | number\| string | No       | All      | Yes               |

**Image**： 图像元素，支持 JPEG、PNG 格式

> [!WARNING]
>
> 注： Image 依赖 Canary3 Sp2 以上版本的 SDK 和 ROM。

|        Name         |                Description                 |               Type               | Required | Platform | HarmonyOS Support |
| :-----------------: | :----------------------------------------: | :------------------------------: | -------- | -------- | ----------------- |
|          x          |             在 x 轴上平移距离              |         number\| string          | No       | All      | Yes               |
|          y          |             在 y 轴上平移距离              |         number\| string          | No       | All      | Yes               |
|        width        |                  元素宽度                  |         number\| string          | Yes      | All      | Yes               |
|       height        |                  元素高度                  |         number\| string          | Yes      | All      | Yes               |
|        href         |                图像资源引用                |         source\| string          | Yes      | All      | Yes               |
|      xlinkHref      |         用于指定要嵌入的图像的 URL         | RNImageProps['source'] \| string | No       | All      | Yes               |
| preserveAspectRatio | 控制在给定的容器尺寸内如何保持图像的宽高比 |              string              | No       | All      | Yes               |
|       opacity       |                   透明度                   |         source\| string          | No       | All      | Yes               |

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

**Defs**：该元素是用于对 Others SVG 元素进行分组的容器

> 注： 该组件无 Properties

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | -------- | -------- | ----------------- |
|  /   |      /      |  /   | /        | All      | Yes               |

**LinearGradient**：用于定义线性渐变

|       Name        |              Description               |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        x1         |           在 x 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        y1         |           在 y 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        x2         |           在 x 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|        y2         |           在 y 轴上平移距离            |             number\| string             | No       | All      | Yes               |
|   gradientUnits   |    指定元素 Properties 使用的坐标系    | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
| gradientTransform | 指定从元素当前坐标系到目标坐标系的转换 |  ColumnMajorTransformMatrix \| string   | No       | All      | Yes               |

**RadialGradient**：用于定义线性渐变

> [!WARNING]
>
> 注： RadialGradient 依赖 Canary3 Sp2 以上版本的 SDK 和 ROM。

|       Name        |              Description               |                  Type                   | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------------: | :-------------------------------------: | -------- | -------- | ----------------- |
|        fx         |           起始圆的 x 轴坐标            |             number\| string             | No       | All      | Yes               |
|        fy         |           起始圆的 y 轴坐标            |             number\| string             | No       | All      | Yes               |
|        rx         |          终止椭圆的 x 轴半径           |             number\| string             | No       | All      | Yes               |
|        ry         |          终止椭圆的 y 轴半径           |             number\| string             | No       | All      | Yes               |
|        cx         |           终止圆的 x 轴坐标            |             number\| string             | No       | All      | Yes               |
|        cy         |           终止圆的 y 轴坐标            |             number\| string             | No       | All      | Yes               |
|         r         |              终止圆的半径              |             number\| string             | No       | All      | Yes               |
|   gradientUnits   |    指定元素 Properties 使用的坐标系    | 'userSpaceOnUse' \| 'objectBoundingBox' | No       | All      | Yes               |
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

|   Name    |                      Description                       |      Type       | Required | Platform | HarmonyOS Support |
| :-------: | :----------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|     x     |                   在 x 轴上平移距离                    | number\| string | No       | All      | Yes               |
|     y     |                   在 y 轴上平移距离                    | number\| string | No       | All      | Yes               |
|   width   |                        元素宽度                        | number\| string | No       | All      | Yes               |
|  height   |                        元素高度                        | number\| string | No       | All      | Yes               |
|   href    |                      图像资源引用                      | source\| string | Yes      | All      | Yes               |
| xlinkHref | 指定了一个 URI，该 URI 指向了 SVG 文档中定义的一个元素 |     string      | No       | All      | Yes               |
|  opacity  |                         透明度                         | number\| string | No       | All      | Yes               |

**Ellipse**： 椭圆绘制组件，基于一个中心坐标以及它们的 x 半径和 y 半径

|  Name   |      Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :-------------------: | :-------------: | -------- | -------- | ----------------- |
|   cx    | 圆心在 x 轴上平移距离 | number\| string | No       | All      | Yes               |
|   cy    | 圆心在 y 轴上平移距离 | number\| string | No       | All      | Yes               |
|   rx    |   定义 x 轴上的半径   | number\| string | No       | All      | Yes               |
|   ry    |   定义 y 轴上的半径   | number\| string | No       | All      | Yes               |
| opacity |        透明度         | number\| string | No       | All      | Yes               |

**Symbol**： 该元素用来定义一个图形模板对象，它可以用一个<use>元素实例化

|        Name         |     Description      |  Type  | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :----: | -------- | -------- | ----------------- |
| preserveAspectRatio | 是否强制进行统一缩放 | string | No       | All      | Yes               |
|       viewBox       |       组件视区       | string | No       | All      | Yes               |

**ClipPath**：该元素定义一条剪切路径，可作为 Others 元素的 clipPath Properties 的值

> 注： 该组件无 Properties

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| :--: | :---------: | :--: | -------- | -------- | ----------------- |
|  /   |      /      |  /   | /        | All      | Yes               |

**Marker**：用于在绘制类组件上添加标记

|     Name     |                          Description                          |      Type       | Required | Platform | HarmonyOS Support |
| :----------: | :-----------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|      id      |                     为元素分配唯一的名称                      |     string      | Yes      | All      | Yes               |
|   viewBox    |                 视窗在用户空间中的位置和尺寸                  |     string      | No       | All      | Yes               |
|     refX     |                      标记参考点的 x 坐标                      | number\| string | No       | All      | Yes               |
|     refY     |                      标记参考点的 y 坐标                      | number\| string | No       | All      | Yes               |
| markerUnits  | markerWidth 和 markerHeight Properties 的坐标系以及标记的内容 |     string      | No       | All      | Yes               |
|    orient    |            将标记放置在形状上的相应位置时如何旋转             |     string      | No       | All      | Yes               |
| markerWidth  |                   表示标记进入的视窗的宽度                    | number\| string | No       | All      | Yes               |
| markerHeight |                   表示标记进入的视窗的高度                    | number\| string | No       | All      | Yes               |

**Pattern**：用于定义一个图形对象，可以被引用以平铺重绘该图形对象以覆盖某个区域。

|        Name         |                                Description                                |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :-----------------------------------------------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         id          |                           为元素分配唯一的名称                            |     string      | Yes      | All      | Yes               |
|          x          |                            标记参考点的 x 坐标                            | number\| string | No       | All      | Yes               |
|          y          |                            标记参考点的 y 坐标                            | number\| string | No       | All      | Yes               |
|        width        |                         表示标记进入的视窗的宽度                          | number\| string | No       | All      | Yes               |
|       height        |                         表示标记进入的视窗的高度                          | number\| string | No       | All      | Yes               |
|    patternUnits     |      Properties 指示 pattern 元素的几何 Properties 使用哪个坐标系。       |     string      | No       | All      | Yes               |
| patternContentUnit  |      Properties 指示 pattern 元素的几何 Properties 使用哪个坐标系。       |     string      | No       | All      | Yes               |
|  patternTransform   |                   定义了应用于图案图块的变换定义的列表                    |     string      | No       | All      | Yes               |
|       viewBox       |                     定义视窗在用户空间中的位置和尺寸                      |     string      | No       | All      | Yes               |
| preserveAspectRatio | 指示具有提供给定宽高比的 viewBox 的元素必须如何适应具有不同宽高比的视口。 |     string      | No       | All      | Yes               |

**Symbol**：用于定义可由 use 元素实例化的图形模板对象。

|        Name         |                                Description                                |  Type  | Required | Platform | HarmonyOS Support |
| :-----------------: | :-----------------------------------------------------------------------: | :----: | -------- | -------- | ----------------- |
|         id          |                           为元素分配唯一的名称                            | string | Yes      | All      | Yes               |
|       viewBox       |                     定义视窗在用户空间中的位置和尺寸                      | string | No       | All      | Yes               |
| preserveAspectRatio | 指示具有提供给定宽高比的 viewBox 的元素必须如何适应具有不同宽高比的视口。 | string | No       | All      | Yes               |

**Line**：SVG 基本形状，用于创建连接两点的线。

|  Name   |   Description    |      Type       | Required | Platform | HarmonyOS Support |
| :-----: | :--------------: | :-------------: | -------- | -------- | ----------------- |
|   x1    | x 轴上线条的起点 | number\| string | No       | All      | Yes               |
|   y1    | y 轴上的线的起点 | number\| string | No       | All      | Yes               |
|   x2    | x 轴上的线的末端 | number\| string | No       | All      | Yes               |
|   y2    | y 轴上的线的末端 | number\| string | No       | All      | Yes               |
| opacity |      透明度      | number\| string | No       | All      | Yes               |

**Text**：绘制由文本组成的图形元素

|       Name        |           Description            |      Type       | Required | Platform | HarmonyOS Support |
| :---------------: | :------------------------------: | :-------------: | -------- | -------- | ----------------- |
|         x         |      文本基线起点的 x 坐标       |  number\string  | No       | All      | Yes               |
|         y         |      文本基线起点的 y 坐标       |  number\string  | No       | All      | Yes               |
|        dx         | 从前一个文本元素水平移动文本位置 |  number\string  | No       | All      | Yes               |
|        dy         | 从前一个文本元素垂直移动文本位置 | number\| string | No       | All      | Yes               |
|      rotate       |      旋转每个单独字形的方向      |      array      | No       | All      | Yes               |
|      opacity      |              透明度              |     number      | No       | All      | Yes               |
|    inlineSize     |          水平或垂直尺寸          |     number      | No       | All      | No                |
| alignmentBaseline |        指定文本的对齐基线        |     string      | NO       | ALL      | Yes               |
|   baselineShift   |         设置垂直位置调整         | number\| string | No       | All      | Yes               |
|   lengthAdjust    |   调整文本以适应特定的布局约束   |     string      | No       | All      | Yes               |
|    textLength     |     指定文本应该被渲染的长度     |     number      | No       | All      | Yes               |

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

**TextPath**：若要沿路径形状呈现文本，将文本括在具有 href Properties 的 TextPath 元素中，并引用 Path 元素。

|    Name     |            Description             |      Type       | Required | Platform | HarmonyOS Support |
| :---------: | :--------------------------------: | :-------------: | -------- | -------- | ----------------- |
|    href     | 用于呈现文本的路径或基本形状的 URL |     string      | No       | All      | No                |
|  xlinkHref  | 用于呈现文本的路径或基本形状的 URL |     string      | No       | All      | No                |
|   method    |      沿路径渲染各个字形的方法      |     string      | No       | All      | No                |
|   spacing   |         绘制字符之间的间距         |     string      | No       | All      | No                |
|    side     |      文本应呈现在路径的哪一侧      |     string      | No       | All      | No                |
|   midLine   |                中线                |     string      | No       | All      | No                |
| startOffset |  文本开始被沿着路径绘制时的偏移量  | number\| string | No       | All      | No                |

**SvgAst**：该组件通过传入 ast 来渲染出 svg

|   Name   |         Description          |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :--------------------------: | :----: | :------: | :------: | :---------------: |
|   ast    | 解析 svg 字符串得到的 ast 树 | JsxAST |   Yes    |   All    |        Yes        |
| override |    覆盖 svg 样式，如宽高     | object |    No    |   All    |        Yes        |

**SvgFromUri**：该组件通过传入 uri 地址来渲染出 svg

|   Name   |      Description      |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :----: | :------: | :------: | :---------------: |
|   uri    |     svg 资源地址      | string |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 | object |    No    |   All    |        Yes        |

**SvgFromXml**：该组件通过传入字符串来渲染出 svg

|   Name   |      Description      |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :----: | :------: | :------: | :---------------: |
|   xml    |   svg 代码的字符串    | string |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 | object |    No    |   All    |        Yes        |

**SvgXml**：该组件通过传入字符串来渲染出 svg

|   Name   |      Description      |  Type  | Required | Platform | HarmonyOS Support |
| :------: | :-------------------: | :----: | :------: | :------: | :---------------: |
|   xml    |   svg 代码的字符串    | string |   Yes    |   All    |        Yes        |
| override | 覆盖 svg 样式，如宽高 | object |    No    |   All    |        Yes        |

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

**公共 Properties**：

Common props 组件 Properties HarmonyOS 侧支持情况

|       Name       |                                       Description                                       |    Type     |  Default  | Required | Platform |
| :--------------: | :-------------------------------------------------------------------------------------: | :---------: | :-------: | :------: | :------: |
|       fill       |                                    设置填充区域颜色                                     |   string    |  '#000'   |    No    |   All    |
|   fillOpacity    |                                   设置填充区域透明度                                    |   number    |     1     |    No    |   All    |
|     fillRule     |                                      设置填充规则                                       |   number    |     1     |    No    |   All    |
|     clipRule     |                                      设置裁剪规则                                       |   string    | 'evenodd' |    No    |   All    |
|     clipPath     |                                 指定、关联一条裁剪路径                                  |   string    |  'none'   |    No    |   All    |
|      stroke      |                          设置边框颜色，不设置时，默认没有边框                           |   string    |   none    |    No    |   All    |
|   strokeWidth    |                                      设置边框宽度                                       |   number    |     1     |    No    |   All    |
|  strokeOpacity   |                                       边框透明度                                        |   number    |     1     |    No    |   All    |
| strokeDasharray  |                               用来描边的点划线的图案范式                                |   number    |   none    |    No    |   All    |
| strokeDashoffset |                            指定了 dash 模式到路径开始的距离                             |   number    |     1     |    No    |   All    |
|  strokeLinecap   |                                   设置路径两端的形状                                    |   string    |   butt    |    No    |   All    |
|  strokeLinejoin  |                               指明路径的转角处使用的形状                                |   string    |   miter   |    No    |   All    |
| strokeMiterlimit |                       对斜接长度和 stroke-width 的比率设置极限 值                       |   number    |     4     |    No    |   All    |
|   vectorEffect   |                             指明绘制对象时要使用的矢量效果                              |   string    |   none    |    No    |   All    |
|    translate     |                                        设置位移                                         | numberArray |    0,0    |    No    |   All    |
|    translateX    |                                      设置 x 轴位移                                      |   number    |     0     |    No    |   All    |
|    translateY    |                                      设置 y 轴位移                                      |   number    |     0     |    No    |   All    |
|      origin      |                                 更改一个元素变形的原点                                  | numberArray |    0,0    |    No    |   All    |
|     originX      | 更改一个元素变形的原点 x 坐标（单独使用无效，需配合 OthersProperties 如 rotation 使用） |   number    |     0     |    No    |   All    |
|     originY      | 更改一个元素变形的原点 y 坐标（单独使用无效，需配合 OthersProperties 如 rotation 使用） |   number    |     0     |    No    |   All    |
|      scale       |                                      定义缩放大小                                       | numberArray |   1，1    |    No    |   All    |
|      scaleX      |                                    定义 x 轴缩放大小                                    |   number    |     1     |    No    |   All    |
|      scaleY      |                                    定义 y 轴缩放大小                                    |   number    |     1     |    No    |   All    |
|     rotation     |                                      设置旋转角度                                       |   number    |   0，0    |    No    |   All    |
|        x         |                                    标识一个 x 轴坐标                                    |   number    |     0     |    No    |   All    |
|        y         |                                    标识一个 y 轴坐标                                    |   number    |     0     |    No    |   All    |
|    transform     |                         定义应用于元素及其子元素的变换规则列表                          |   string    |     -     |    No    |   All    |
|      marker      |                               指定路径所有顶点的路标样式                                |   string    |     -     |    No    |   All    |
|   markerStart    |                              指定路径起点所采用的路标样式                               |   string    |     -     |    No    |   All    |
|    markerMid     |                            指定路径中间顶点所采用的路标样式                             |   string    |     -     |    No    |   All    |
|    markerEnd     |                              指定路径终点所采用的路标样式                               |   string    |     -     |    No    |   All    |
|       mask       |                          给元素指定使用 Mask 元素实现遮罩效果                           |   string    |     -     |    No    |   All    |
|        id        |                                       设置节点 id                                       |   string    |     -     |    No    |   All    |
|     opacity      |                                       设置透明度                                        |   number    |     1     |    No    |   All    |
|    transform     |                         定义应用于元素及其子元素的变换规则列表                          |   string    |     -     |    No    |   All    |
|     display      |                                   控制元素展示的方式                                    |   string    |   block   |    No    |   All    |
|  pointerEvents   |                                设置元素如何响应点击事件                                 |   string    |           |    No    |   All    |
|   vectorEffect   |                             指明绘制对象时要使用的矢量效果                              |     Int     |     0     |    No    |   All    |

FontProps 组件 Properties HarmonyOS 侧支持情况

|         Name          |                          Description                           |        Type        | Default | Required | Platform |
| :-------------------: | :------------------------------------------------------------: | :----------------: | :-----: | :------: | :------: |
|       fontSize        | 在多行布局环境中将多行文本设置为实线时，从基线到基线的字体大小 |       string       | medium  |    No    |   All    |
|      fontWeight       | 用于呈现文本的字形相对于同一字体族中的 Others 字体的粗度或亮度 |       string       | normal  |    No    |   All    |
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

## Known Issues

- [ ] isPointInFill 判断点位坐标是否在 fill 上 未实现
- [ ] isPointInStroke 判断点位坐标是否在 stroke 上 未实现
- [ ] getTotalLength 获取总 path 的长度 未实现
- [ ] getPointAtLength 获取点位坐标在 path 上的信息 未实现
- [ ] getBBox 获取组件的边界信息 未实现
- [ ] getCTM 获取相对于父组件的 matrix 矩阵信息 未实现
- [ ] getScreenCTM 获取组件的 matrix 矩阵信息 未实现
- [ ] getRawResource 获取 android 中的资源文件 未实现
- [ ] foreignObject 该组件允许 svg 使用外部组件 未实现
- [ ] filter 该组件可以为 SVG 图形添加各种视觉效果 未实现
- [ ] TextPath 功能未完全实现
- [ ] Text,TSpan 组件的 rotate,fontFamily,wordSpacingProperties 未实现

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-svg/blob/harmony/LICENSE).

