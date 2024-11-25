> Template version: v0.2.2

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-clippath/tree/capi)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-clippathview Releases](https://github.com/react-native-oh-library/react-native-clippath/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-clippathview
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-clippathview
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

Open  `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-clippathview": "file:../../node_modules/@react-native-oh-tpl/react-native-clippathview/harmony/clipPath.har",
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


### 3. Configuring CMakeLists and Introducing ClipPathViewPackage

Open  `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open  `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing  ClipPathPackage to ArkTS

Open the  `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-clippathview Releases](https://github.com/react-native-oh-library/react-native-clippath/releases)

## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-clippath/blob/capi/LICENSE).
