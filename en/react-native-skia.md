模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-skia</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Shopify/react-native-skia">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Shopify/react-native-skia/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-skia)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-skia Releases](https://github.com/react-native-oh-library/react-native-skia/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-skia@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-skia@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { Canvas, Circle, Group } from "@shopify/react-native-skia";

const App = () => {
  const width = 256;
  const height = 256;
  const r = width * 0.33;
  return (
    <Canvas style={{ width, height }}>
      <Group blendMode="multiply">
        <Circle cx={r} cy={r} r={r} color="cyan" />
        <Circle cx={width - r} cy={r} r={r} color="magenta" />
        <Circle cx={width / 2} cy={width - r} r={r} color="yellow" />
      </Group>
    </Canvas>
  );
};

export default App;
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-skia": "file:../../node_modules/@react-native-oh-tpl/react-native-skia/harmony/skia.har"
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

### 3.配置 CMakeLists 和引入 SkiaPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-skia/src/main/cpp" ./skia)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_skia)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SkiaPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SkiaPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 SkiaDomView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNCSkiaDomView, SKIA_DOM_VIEW_TYPE } from '@react-native-oh-tpl/react-native-skia';

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SKIA_DOM_VIEW_TYPE) {
+   RNCSkiaDomView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SKIA_DOM_VIEW_TYPE
  ];
```

### 5.在 ArkTs 侧引入 RNSkiaPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNSkiaPackage} from '@react-native-oh-tpl/react-native-skia/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSkiaPackage(ctx)
  ];
}
```

### 6.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-skia Releases](https://github.com/react-native-oh-library/react-native-skia/releases)

## 组件

### Canvas

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> | Name     | Description                                                                                                                                            | Type                     | Required | Platform    | HarmonyOS Support |
> | -------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------ | -------- | ----------- | ----------------- |
> | style    | View style                                                                                                                                             | ViewStyle                | no       | android/ios | yes               |
> | ref      | Reference to the SkiaView object                                                                                                                       | Ref<SkiaView>            | no       | android/ios | yes               |
> | mode     | By default, the canvas is only updated when the drawing tree or animation values change. With mode="continuous", the canvas will redraw on every frame | default/continuous       | no       | android/ios | yes               |
> | onSize   | Reanimated value to which the canvas size will be assigned                                                                                             | SharedValue<Size>        | no       | android/ios | yes               |
> | onLayout | Invoked on mount and on layout changes                                                                                                                 | NativeEvent<LayoutEvent> | no       | android/ios | yes               |

### Group

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name       | Description                                                                                                                                                                                                            | Type              | Required | Platform    | HarmonyOS Support |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------- | -------- | ----------- | ----------------- |
| transform  | [ Same API that's in React Native](https://reactnative.dev/docs/transforms). The default origin of the transformation is, however, different. It is the center object in React Native and the top-left corner in Skia. | Transform2d       | no       | android/ios | yes               |
| origin     | Sets the origin of the transformation. This property is not inherited by its children.                                                                                                                                 | Point             | no       | android/ios | yes               |
| clip       | Rectangle, rounded rectangle, or Path to use to clip the children.                                                                                                                                                     | RectOrRRectOrPath | no       | android/ios | yes               |
| invertClip | Invert the clipping region: parts outside the clipping region will be shown and, inside will be hidden.                                                                                                                | boolean           | no       | android/ios | yes               |
| layer      | Draws the children as a bitmap and applies the effects provided by the paint.                                                                                                                                          | RefObject<Paint>  | no       | android/ios | yes               |

### Path

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                                                                                                                                                                                                      | Type             | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ---------------- | -------- | ----------- | ----------------- |
| path   | Path to draw. Can be a string using the [SVG Path notation](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths#line_commands) or an object created with `Skia.Path.Make()`.                                                         | SkPath`or`string | no       | android/ios | yes               |
| start  | Trims the start of the path. Value is in the range `[0, 1]` (default is 0).                                                                                                                                                                      | number           | no       | android/ios | yes               |
| end    | Trims the end of the path. Value is in the range `[0, 1]` (default is 1).                                                                                                                                                                        | number           | no       | android/ios | yes               |
| stroke | Turns this path into the filled equivalent of the stroked path. This will fail if the path is a hairline. `StrokeOptions` describes how the stroked path should look. It contains three properties: `width`, `strokeMiterLimit` and, `precision` | StrokeOptions    | no       | android/ios | yes               |

### Polygons

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description              | Type             | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------ | ---------------- | -------- | ----------- | ----------------- |
| x      | X coordinate.            | SkPath`or`string | no       | android/ios | yes               |
| y      | Y coordinate.            | number           | no       | android/ios | yes               |
| width  | Width of the rectangle.  | number           | no       | android/ios | yes               |
| height | Height of the rectangle. | StrokeOptions    | no       | android/ios | yes               |

### Ellipses

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description  | Type   | Required | Platfor     | HarmonyOS Support |
| ---- | ------------ | ------ | -------- | ----------- | ----------------- |
| cx   | Start point. | number | no       | android/ios | yes               |
| cy   | End point.   | number | no       | android/ios | yes               |
| r`   | Radius.      | number | no       | android/ios | yes               |

### Atlas

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name       | Type              | Description                                                               | Required | android/ios | HarmonyOS Support |
| ---------- | ----------------- | ------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| image      | `SkImage or null` | Altas: image containing the sprites.                                      | no       | android/ios | yes               |
| sprites    | `SkRect[]`        | locations of sprites in atlas.                                            | no       | android/ios | yes               |
| transforms | `RSXform[]`       | Rotation/scale transforms to be applied for each sprite.                  | no       | android/ios | yes               |
| colors     | `SkColor[]`       | Optional. Color to blend the sprites with.                                | yes      | android/ios | yes               |
| blendMode  | `BlendMode`       | Optional. Blend mode used to combine sprites and colors together.\*\*\*\* | yes      | android/ios | yes               |

### Vertices

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Type         | Description                                                                                                                                                           | Required | android/ios | HarmonyOS Support |
| --------- | ------------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| vertices  | `Point[]`    | Vertices to draw                                                                                                                                                      | no       | android/ios | yes               |
| mode      | `VertexMode` | Can be `triangles`, `trianglesStrip` or `triangleFan`. Default is `triangles`                                                                                         | yes      | android/ios | yes               |
| indices   | `number[]`   | Indices of the vertices that form the triangles. If not provided, the order of the vertices will be taken. Using this property enables you not to duplicate vertices. | yes      | android/ios | yes               |
| textures  | `Point[]`.   | [Texture mapping](https://en.wikipedia.org/wiki/Texture_mapping). The texture is the shader provided by the paint.                                                    | no       | android/ios | yes               |
| colors    | `string[]`   | Optional colors to be associated to each vertex                                                                                                                       | yes      | android/ios | yes               |
| blendMode | `BlendMode`  | If `colors` is provided, colors are blended with the paint using the blend mode. Default is `dstOver` if colors are provided, `srcOver` if not.                       | yes      | android/ios | yes               |

### Patch

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Type             | Description                                                                                                                                                 | Required | android/ios | HarmonyOS Support |
| --------- | ---------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| cubics    | `CubicBezier[4]` | Specifies four cubic Bezier starting at the top-left corner, in clockwise order, sharing every fourth point. The last cubic Bezier ends at the first point. | no       | android/ios | yes               |
| textures  | `Point[]`.       | [Texture mapping](https://en.wikipedia.org/wiki/Texture_mapping). The texture is the shader provided by the paint                                           | no       | android/ios | yes               |
| colors    | `string[]`       | Optional colors to be associated to each corner                                                                                                             | yes      | android/ios | yes               |
| blendMode | `BlendMode`      | If `colors` is provided, colors are blended with the paint using the blend mode. Default is `dstOver` if colors are provided, `srcOver` if not              | yes      | android/ios | yes               |

### Gradients 公共属性

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                                                                                                                                                                                                                                                                                            | Type         | Required | Platform    | HarmonyOS Support |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------ | -------- | ----------- | ----------------- |
| colors    | Colors to be distributed between start and end.                                                                                                                                                                                                                                                        | string[]     | yes      | android/ios | yes               |
| positions | The relative positions of colors. If supplied, it must be of the same length as colors.                                                                                                                                                                                                                | number[]     | no       | android/ios | yes               |
| mode      | Can be `clamp`, `repeat`, `mirror`, or `decal`.                                                                                                                                                                                                                                                        | TileMode     | no       | android/ios | yes               |
| flags     | By default, gradients will interpolate their colors in unpremultiplied space and then premultiply each of the results. By setting this to 1, the gradients will premultiply their colors first and then interpolate between them.                                                                      | number       | no       | android/ios | yes               |
| transform | The transform property is identical to its [homonymous property in React Native](https://reactnative.dev/docs/transforms) except for one significant difference: in React Native, the origin of transformation is the center of the object, whereas it is the top-left position of the object in Skia. | Transforms2d | no       | android/ios | yes               |

### LinearGradient

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description                     | Type  | Required | Platform    | HarmonyOS Support |
| ----- | ------------------------------- | ----- | -------- | ----------- | ----------------- |
| start | Start position of the gradient. | Point | yes      | android/ios | yes               |
| end   | End position of the gradient.   | Point | yes      | android/ios | yes               |

### RadialGradient

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| c    | Center of the gradient. | Point  | yes      | android/ios | yes               |
| r    | Radius of the gradient. | number | yes      | android/ios | yes               |

### TwoPointConicalGradient

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                 | Type   | Required | Platform    | HarmonyOS Support |
| ------ | --------------------------- | ------ | -------- | ----------- | ----------------- |
| start  | Center of the start circle. | Point  | yes      | android/ios | yes               |
| startR | Radius of the start circle. | number | yes      | android/ios | yes               |
| end    | Center of the end circle.   | number | yes      | android/ios | yes               |
| endR   | Radius of the end circle.   | number | yes      | android/ios | yes               |

### SweepGradient

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description                            | Type   | Required | Platform    | HarmonyOS Support |
| ----- | -------------------------------------- | ------ | -------- | ----------- | ----------------- |
| c     | Center of the gradient.                | Point  | yes      | android/ios | yes               |
| start | Start angle in degrees (default is 0). | number | no       | android/ios | yes               |
| end   | End angle in degrees (default is 360). | number | no       | android/ios | yes               |

### FractalNoise

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name       | Description                                                                                                                    | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| freqX      | base frequency in the X direction; range [0.0, 1.0]                                                                            | number | yes      | android/ios | yes               |
| freqY      | base frequency in the Y direction; range [0.0, 1.0]                                                                            | number | yes      | android/ios | yes               |
| octaves    |                                                                                                                                | number | yes      | android/ios | yes               |
| seed       |                                                                                                                                | number | yes      | android/ios | yes               |
| tileWidth  | if this and `tileHeight` are non-zero, the frequencies will be modified so that the noise will be tileable for the given size. | number | no       | android/ios | yes               |
| tileHeight | if this and `tileWidth` are non-zero, the frequencies will be modified so that the noise will be tileable for the given size.  | number | no       | android/ios | yes               |

### Turbulence

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name       | Description                                                                                                                    | Type   | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| freqX      | base frequency in the X direction; range [0.0, 1.0]                                                                            | number | yes      | android/ios | yes               |
| freqY      | base frequency in the Y direction; range [0.0, 1.0]                                                                            | number | yes      | android/ios | yes               |
| octaves    |                                                                                                                                | number | yes      | android/ios | yes               |
| seed       |                                                                                                                                | number | yes      | android/ios | yes               |
| tileWidth  | if this and `tileHeight` are non-zero, the frequencies will be modified so that the noise will be tileable for the given size. | number | no       | android/ios | yes               |
| tileHeight | if this and `tileWidth` are non-zero, the frequencies will be modified so that the noise will be tileable for the given size.  | number | no       | android/ios | yes               |

### Blend

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                                                                                                                                                                                                                                                                                                                                                                                                                                          | Type      | Required | Platform    | HarmonyOS Support |
| -------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | ----------- | ----------------- |
| mode     | Sets the blend mode that is, the mode used to combine source color with destination color. The following values are available: `clear`, `src`, `dst`, `srcOver`, `dstOver`, `srcIn`, `dstIn`, `srcOut`, `dstOut`, `srcATop`, `dstATop`, `xor`, `plus`, `modulate`, `screen`, `overlay`, `darken`, `lighten`, `colorDodge`, `colorBurn`, `hardLight`, `softLight`, `difference`, `exclusion`, `multiply`, `hue`, `saturation`, `color`, `luminosity`. | BlendMode | yes      | android/ios | yes               |
| children | Shaders to blend                                                                                                                                                                                                                                                                                                                                                                                                                                     | ReactNode | yes      | android/ios | yes               |

### ColorShader

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------ | -------- | ----------- | ----------------- |
| color | Color       | string | yes      | android/ios | yes               |

### DiscretePathEffect

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                                                   | Type       | Required | Platform    | HarmonyOS Support |
| --------- | ------------------------------------------------------------- | ---------- | -------- | ----------- | ----------------- |
| length    | length of the subsegments.                                    | number     | yes      | android/ios | yes               |
| deviation | limit of the movement of the endpoints.                       | number     | yes      | android/ios | yes               |
| seed      | modifies the randomness. See SkDiscretePathEffect.h for more. | number     | yes      | android/ios | yes               |
| children  | Optional path effect to apply.                                | PathEffect | no       | android/ios | yes               |

### DashPathEffect

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                                                                                                                             | Type       | Required | Platform    | HarmonyOS Support |
| --------- | --------------------------------------------------------------------------------------------------------------------------------------- | ---------- | -------- | ----------- | ----------------- |
| intervals | even number of entries with even indices specifying the length of the "on" intervals, and the odd index specifying the length of "off". | number[]   | yes      | android/ios | yes               |
| phase     | offset into the intervals array. Defaults to 0.                                                                                         | number     | yes      | android/ios | yes               |
| children  | Optional path effect to apply.                                                                                                          | PathEffect | no       | android/ios | yes               |

### CornerPathEffect

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                    | Type       | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------ | ---------- | -------- | ----------- | ----------------- |
| r        | Radius.                        | number     | yes      | android/ios | yes               |
| children | Optional path effect to apply. | PathEffect | no       | android/ios | yes               |

### Path1DPathEffect

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                                                                     | Type              | Required | Platform    | HarmonyOS Support |
| -------- | ------------------------------------------------------------------------------- | ----------------- | -------- | ----------- | ----------------- |
| path     | The path to replicate (dash)                                                    | PathDef           | yes      | android/ios | yes               |
| advance  | The space between instances of path                                             | number            | yes      | android/ios | yes               |
| phase    | distance (mod advance) along the path for its initial position                  | number            | yes      | android/ios | yes               |
| style    | how to transform path at each point (based on the current position and tangent) | Path1DEffectStyle | yes      | android/ios | yes               |
| children | Optional path effect to apply.                                                  | PathEffect        | no       | android/ios | yes               |

### Path2DPathEffect

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                   | Type       | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------- | ---------- | -------- | ----------- | ----------------- |
| path     | The path to use               | PathDef    | yes      | android/ios | yes               |
| matrix   | Matrix to be applied          | SkMatrix   | yes      | android/ios | yes               |
| children | Optional path effect to apply | PathEffect | no       | android/ios | yes               |

### Line2DPathEffect

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                   | Type       | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------- | ---------- | -------- | ----------- | ----------------- |
| width    | The path to use               | PathDef    | yes      | android/ios | yes               |
| matrix   | Matrix to be applied          | IMatrix    | yes      | android/ios | yes               |
| children | Optional path effect to apply | PathEffect | no       | android/ios | yes               |

### Mask

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name     | Description                                          | Type               | Required | Platform    | HarmonyOS Support |
| -------- | ---------------------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| mode     | Is it a luminance or alpha mask (default is `alpha`) | alpha \| luminance | no       | android/ios | yes               |
| clip     | clip the mask so it doesn't exceed the content       | bool               | no       | android/ios | yes               |
| mask     | ReactNode                                            | ReactNode[]        | yes      | android/ios | yes               |
| children | ReactNode                                            | ReactNode[]        | yes      | android/ios | yes               |

### Image

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                                                                                                                                | Type    | Required | Platform    | HarmonyOS Support |
| ------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| image  | An instance of the image.                                                                                                                                                  | SkImage | yes      | android/ios | yes               |
| x      | The left position of the destination image.                                                                                                                                | number  | yes      | android/ios | yes               |
| y      | The top position of the destination image.                                                                                                                                 | number  | yes      | android/ios | yes               |
| width  | The width of the destination image.                                                                                                                                        | number  | yes      | android/ios | yes               |
| height | The height of the destination image.                                                                                                                                       | number  | yes      | android/ios | yes               |
| fit    | The method used to fit the image into the rectangle. Values can be `contain`, `fill`, `cover`, `fitHeight`, `fitWidth`, `scaleDown`, or `none` (the default is `contain`). | Fit     | no       | android/ios | yes               |

### SVG Image

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| svg    | SVG Image.                                  | SVG    | yes      | android/ios | yes               |
| x      | The left position of the destination image. | number | no       | android/ios | yes               |
| y      | The top position of the destination image.  | number | no       | android/ios | yes               |
| width  | The width of the destination image.         | number | no       | android/ios | yes               |
| height | The height of the destination image.        | number | no       | android/ios | yes               |

### Paragraph

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                                   | Type        | Required | Platform    | HarmonyOS Support |
| --------- | --------------------------------------------- | ----------- | -------- | ----------- | ----------------- |
| paragraph | text paragraph                                | skParagraph | yes      | android/ios | yes               |
| x         | Left position of the text (default is 0)      | number      | yes      | android/ios | yes               |
| y         | Bottom position the text (default is 0, the ) | number      | yes      | android/ios | yes               |
| width     | The width of the paragraph.                   | number      | yes      | android/ios | yes               |

### Text

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description                                   | Type   | Required | Platform    | HarmonyOS Support |
| ---- | --------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| text | Text to draw                                  | string | yes      | android/ios | yes               |
| x    | Left position of the text (default is 0)      | number | yes      | android/ios | yes               |
| y    | Bottom position the text (default is 0, the ) | number | yes      | android/ios | yes               |
| font | Font to use                                   | SkFont | yes      | android/ios | yes               |

### Glyphs

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                | Type    | Required | Platform    | HarmonyOS Support |
| ------ | ---------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| glyphs | Glyphs to draw                                             | Glyph[] | yes      | android/ios | yes               |
| x      | x coordinate of the origin of the entire run. Default is 0 | number  | no       | android/ios | yes               |
| y      | y coordinate of the origin of the entire run. Default is 0 | number  | yno      | android/ios | yes               |
| font   | Font to use                                                | SkFont  | yes      | android/ios | yes               |

### Text Path

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description                                                                                                                                                                             | Type           | Required | Platform    | HarmonyOS Support |
| ---- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | -------- | ----------- | ----------------- |
| path | Path to draw. Can be a string using the [SVG Path notation](https://developer.mozilla.org/en-US/docs/Web/SVG/Tutorial/Paths#line_commands) or an object created with `Skia.Path.Make()` | Path \| string | yes      | android/ios | yes               |
| text | Text to draw                                                                                                                                                                            | string         | yes      | android/ios | yes               |
| font | Font to use                                                                                                                                                                             |                |          |             |                   |

### Text Path

#### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description                                                | Type     | Required | Platform    | HarmonyOS Support |
| ---- | ---------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| blob | Text blob                                                  | TextBlob | yes      | android/ios | yes               |
| x    | x coordinate of the origin of the entire run. Default is 0 | number   | no       | android/ios | yes               |
| y    | y coordinate of the origin of the entire run. Default is 0 | number   | no       | android/ios | yes               |

## RNSkiaModule API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description      | Type     | Required | Platform    | HarmonyOS Support |
| ------- | ---------------- | -------- | -------- | ----------- | ----------------- |
| install | initialized skia | function | yes      | android/ios | yes               |

## 遗留问题

- [x] Text 组件无法使用 问题: [issue#Text 暂不支持](https://github.com/react-native-oh-library/react-native-skia/issues/5)
- [ ] Video 组件无法使用 问题: [issue#Video 暂不支持](https://github.com/react-native-oh-library/react-native-skia/issues/6)
- [x] Image 组件无法使用 问题: [issue#Image 暂不支持](https://github.com/react-native-oh-library/react-native-skia/issues/7)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-skia/blob/sig/LICENSE.md) ，请自由地享受和参与开源。
