<p align="center">
  <h1 align="center"> <code>@react-native-oh-tpl/react-native-fast-image</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DylanVann/react-native-fast-image">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/DylanVann/react-native-fast-image/blob/main/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-community/slider.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-oh-tpl/react-native-fast-image
```

或者

```bash
npm install @react-native-oh-tpl/react-native-fast-image
```

下面的代码展示了这个库的基本使用场景：

```js
import FastImage from 'react-native-fast-image';

<FastImage
    style={ width: 200, height: 40}
    source={{uri: 'https://res.vmallres.com/cmscdn/CN/2023-05/b3cb7e6502854d49bb0e23e11b778ffe.webp'}}
    resizeMode={FastImage.resizeMode.contain}
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
    "rnoh-fast-image": "file:../../node_modules/reac-native-fast-image/harmony/fast_image.har"
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
    "rnoh-slider": "file:../../node_modules/reac-native-fast-image/harmony/fast_image"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 FastImagePackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-fast-image/src/main/cpp" ./fast_image)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_fast_image)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "FastImagePackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<FastImagePackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 FastImage 组件

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
+ import { RNFastImage, FAST_IMAGE_TYPE } from "rnoh-fast-image"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === FAST_IMAGE_TYPE) {
+   RNFastImage({
+     ctx: ctx.rnohContext,
+     tag: ctx.descriptor.tag,
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

| `@react-native-oh-tpl/react-native-fast-image` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version  |
| ----------------------------------------- | ----------------------------- | --------------------- | ------------------------------ | --------------------- |
| `8.6.3-0.0.2`                             | `0.72.5`                      | `0.72.10`             | `4.0.3.601`                    | `OpenHarmony 4.10.10` |

## 属性

| 名称                    | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 类型                                         | 是否必填 | 原库平台     | 鸿蒙支持 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | -------- | ------------ | -------- |
| `source.uri`                 | Source for the remote image to load.                                                                                                                                                                                                                                                                                                                                                                           | string                                   | Yes       | All          | yes      |
| `source.headers?`              | Headers to load the image with. e.g. { Authorization: 'someAuthToken' }.                                                                                                                                                                                                                                                                                                                                                                                                     | object                                         | No       | All          | yes      |
| `source.priority?`          | loading url priority                                                                                                                                                                                                                                                                                                                               | enum                                       | No       | All          | no      |
| `source.cache?` | setting loading url cache mode                                                                                                                                                                                                                                                                                                                                         | enum | No       | All          | no      |
| `defaultSource?`          |   An asset loaded with require(...).                                                                                                                                                                                                                                                                                                                                                                                                                     | number                                       | No       | All          | yes      |
| `resizeMode?`            | loading image for scale mode                                                                                                                                                                                                                                                                                                                                                                                                               | enum                                       | No       | ALL | yes       |
| `onLoadStart?: () => void`            | Called when the image starts to load.                                                                                                                                                                                                                                                                                                                                                                                                               | function                                       | No       | ALL | yes       |
| `onProgress?: (event) => void`        | Called when the image is loading.                                                                                                                                                                                                                                                                                                                                                 | function                                     | No       | All          | yes      |
| `onLoad?: (event) => void`     | Called on a successful image fetch. Called with the width and height of the loaded image.                                                                                                                                                                                                                                                                                                            | function                                     | No       | All          | yes      |
| `onError?: () => void`         | Called on an image fetching error.                                                                                                                                                                                                                                                                                                                                                                                                                | function                                     | No       | All          | yes      |
| `onLoadEnd?: () => void`                  | Called when the image finishes loading, whether it was successful or an error.                                                                                                                                                                                                                                                                | function                                       | No       | All          | yes      |
| `tintColor?` | If supplied, changes the color of all the non-transparent pixels to the given color. | number \| string| No       | All          | yes      |

## 静态方法

| 名称                    | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 类型                                         | 是否必填 | 原库平台     | 鸿蒙支持 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | -------- | ------------ | -------- |
| `FastImage.preload: (source[]) => void`                 | Preload images to display later. e.g.                                                                                                                                                                                                                                                                                                                                                                           | function                                   | no       | All          | No      |
| `FastImage.clearMemoryCache: () => Promise<void>`              | Clear all images from memory cache.                                                                                                                                                                                                                                                                                                                                                                                                     | function                                         | No       | All          | no      |
| `FastImage.clearDiskCache: () => Promise<void>`          | Clear all images from disk cache. priority | function                                       | No       | All          | no      |

## 遗留问题

- [ ] 部分涉及使用缓存能力的接口，未适配

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/DylanVann/react-native-fast-image/blob/main/LICENSE) ，请自由地享受和参与开源。
