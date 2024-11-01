> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-color-matrix-image-filters</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/iyegoroff/react-native-color-matrix-image-filters">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
       <a href="https://github.com/iyegoroff/react-native-color-matrix-image-filters/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-color-matrix-image-filters Releases](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-color-matrix-image-filters@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-color-matrix-image-filters@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import {
    Achromatomaly,
    Achromatopsia,
    Brightness
} from 'react-native-color-matrix-image-filters';

import { View, StyleSheet, Image } from 'react-native';

export const ColorMatrixImageFiltersTest = () => {

    return (<View>
        <Achromatomaly>
            <Image style={styles.image} source={require('./mini-parrot.jpg')} resizeMode={'stretch'} />
        </Achromatomaly>
        <Achromatopsia>
            <Image style={styles.image} source={require('./mini-parrot.jpg')} resizeMode={'stretch'} />
        </Achromatopsia>
        <Brightness>
            <Image style={styles.image} source={require('./mini-parrot.jpg')} resizeMode={'stretch'} />
        </Brightness>
    </View>)
}

const styles = StyleSheet.create({
    image: {
        width: 150,
        height: 100,
        justifyContent: 'center',
        alignItems: 'center'
    }
})
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides字段

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-color-matrix-image-filters": "file:../../node_modules/@react-native-oh-tpl/react-native-color-matrix-image-filters/harmony/color_matrix_image_filters.har"
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
"@rnoh/react-native-openharmony": "file:../react_native_openharmony",
"@react-native-oh-tpl/react-native-color-matrix-image-filters": "file:../../node_modules/@react-native-oh-tpl/react-native-color-matrix-image-filters/harmony/color_matrix_image_filters"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 3.配置 CMakeLists 和引入 ColorMatrixImageFiltersPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-color-matrix-image-filters/src/main/cpp" ./color_matrix_image_filters)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_color_matrix_image_filters )
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ColorMatrixImageFiltersPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ColorMatrixImageFiltersPackage>(ctx)
    };
}
```


### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-color-matrix-image-filters Releases](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| matrix  | Matrix parameter transfer for image filter settings         | number[]  | yes | iOS/Android      | yes |


### Supported filters

| Component        | Additional props                                                                                                | function                                                                                                                           |
| ---------------- | --------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------- |
| ColorMatrix      | matrix: Matrix                                                                                                  | -                                                                                                                                  |
| Normal           | -                                                                                                               | normal(): Matrix                                                                                                                   |
| RGBA             | red: number = 1, green: number = 1, blue: number = 1, alpha: number = 1                                         | rgba(red: number = 1, green: number = 1, blue: number = 1, alpha: number = 1): Matrix                                              |
| Saturate         | amount: number = 1                                                                                              | saturate(amount: number = 1): Matrix                                                                                               |
| HueRotate        | amount: number = 0                                                                                              | hueRotate(amount: number = 0): Matrix                                                                                              |
| LuminanceToAlpha | -                                                                                                               | luminanceToAlpha(): Matrix                                                                                                         |
| Invert           | -                                                                                                               | invert(): Matrix                                                                                                                   |
| Grayscale        | amount: number = 1                                                                                              | grayscale(amount: number = 1): Matrix                                                                                              |
| Sepia            | amount: number = 1                                                                                              | sepia(amount: number = 1): Matrix                                                                                                  |
| Nightvision      | -                                                                                                               | nightvision(): Matrix                                                                                                              |
| Warm             | -                                                                                                               | warm(): Matrix                                                                                                                     |
| Cool             | -                                                                                                               | cool(): Matrix                                                                                                                     |
| Brightness       | amount: number = 1                                                                                              | brightness(amount: number = 1): Matrix                                                                                             |
| Contrast         | amount: number = 1                                                                                              | contrast(amount: number = 1): Matrix                                                                                               |
| Temperature      | amount: number = 1                                                                                              | temperature(amount: number = 1): Matrix                                                                                            |
| Tint             | amount: number = 0                                                                                              | tint(amount: number = 0): Matrix                                                                                                   |
| Threshold        | amount: number = 0                                                                                              | threshold(amount: number = 0): Matrix                                                                                              |
| Technicolor      | -                                                                                                               | technicolor(): Matrix                                                                                                              |
| Polaroid         | -                                                                                                               | polaroid(): Matrix                                                                                                                 |
| ToBGR            | -                                                                                                               | toBGR(): Matrix                                                                                                                    |
| Kodachrome       | -                                                                                                               | kodachrome(): Matrix                                                                                                               |
| Browni           | -                                                                                                               | browni(): Matrix                                                                                                                   |
| Vintage          | -                                                                                                               | vintage(): Matrix                                                                                                                  |
| Night            | amount: number = 0.1                                                                                            | night(amount: number = 0.1): Matrix                                                                                                |
| Predator         | amount: number = 1                                                                                              | predator(amount: number = 1): Matrix                                                                                               |
| Lsd              | -                                                                                                               | lsd(): Matrix                                                                                                                      |
| ColorTone        | desaturation: number = 0.2, toned: number = 0.15, lightColor: string = "#FFE580", darkColor: string = "#338000" | colorTone(desaturation: number = 0.2, toned: number = 0.15, lightColor: string = "#FFE580", darkColor: string = "#338000"): Matrix |
| DuoTone          | firstColor: string = "#FFE580", secondColor: string = "#338000"                                                 | duoTone(firstColor: string = "#FFE580", secondColor: string = "#338000"): Matrix                                                   |
| Protanomaly      | -                                                                                                               | protanomaly(): Matrix                                                                                                              |
| Deuteranomaly    | -                                                                                                               | deuteranomaly(): Matrix                                                                                                            |
| Tritanomaly      | -                                                                                                               | tritanomaly(): Matrix                                                                                                              |
| Protanopia       | -                                                                                                               | protanopia(): Matrix                                                                                                               |
| Deuteranopia     | -                                                                                                               | deuteranopia(): Matrix                                                                                                             |
| Tritanopia       | -                                                                                                               | tritanopia(): Matrix                                                                                                               |
| Achromatopsia    | -                                                                                                               | achromatopsia(): Matrix                                                                                                            |
| Achromatomaly    | -                                                                                                               | achromatomaly(): Matrix                          


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-color-matrix-image-filters/blob/master/LICENSE) ，请自由地享受和参与开源。

