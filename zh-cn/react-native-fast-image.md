> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>react-native-fast-image</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DylanVann/react-native-fast-image">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-fast-image/blob/harmony/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

**正在 npm 发布中，当前请先从仓库[Release](https://github.com/react-native-oh-library/react-native-fast-image/releases)中获取库 tgz，通过使用本地依赖来安装本库。**

#### **yarn**

```bash
yarn add xxx
```

#### **npm**

```bash
npm install xxx
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import FastImage from "react-native-fast-image";

const YourImage = () => (
  <FastImage
    style={{ width: 200, height: 200 }}
    source={{
      uri: "https://unsplash.it/400/400?image=1",
      headers: { Authorization: "someAuthToken" },
      priority: FastImage.priority.normal,
    }}
    resizeMode={FastImage.resizeMode.contain}
  />
);
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
    "rnoh-fast-image": "file:../../node_modules/react-native-fast-image/harmony/fast_image.har"
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
    "rnoh-fast-image": "file:../../node_modules/react-native-fast-image/harmony/fast_image"
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
  if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.descriptor.type === FAST_IMAGE_TYPE) {
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

### 在 ArkTs 侧引入 FastImagePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import { FastImagePackage } from 'rnoh-fast-image/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FastImagePackage(ctx)
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

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl Releases](https://github.com/react-native-oh-library/react-native-fast-image/releases)

## 属性

| 名称                           | 说明                                                                                      | 类型             | 是否必填 | 原库平台 | 鸿蒙支持 |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | -------- |
| `source.uri`                   | Source for the remote image to load.                                                      | string           | yes      | All      | yes      |
| `source.headers?`              | Headers to load the image with. e.g. { Authorization: 'someAuthToken' }.                  | object           | yes      | All      | yes      |
| `source.priority?`             | loading url priority                                                                      | enum             | No       | All      | no       |
| `source.cache?`                | setting loading url cache mode                                                            | enum             | No       | All      | no       |
| `defaultSource?`               | An asset loaded with require(...).                                                        | number           | yes      | All      | yes      |
| `resizeMode?`                  | loading image for scale mode                                                              | enum             | yes      | ALL      | yes      |
| `onLoadStart?: () => void`     | Called when the image starts to load.                                                     | function         | yes      | ALL      | yes      |
| `onProgress?: (event) => void` | Called when the image is loading.                                                         | function         | yes      | All      | yes      |
| `onLoad?: (event) => void`     | Called on a successful image fetch. Called with the width and height of the loaded image. | function         | yes      | All      | yes      |
| `onError?: () => void`         | Called on an image fetching error.                                                        | function         | yes      | All      | yes      |
| `onLoadEnd?: () => void`       | Called when the image finishes loading, whether it was successful or an error.            | function         | yes      | All      | yes      |
| `tintColor?`                   | If supplied, changes the color of all the non-transparent pixels to the given color.      | number \| string | yes      | All      | yes      |

## 静态方法

| 名称                                              | 说明                                       | 类型     | 是否必填 | 原库平台 | 鸿蒙支持 |
| ------------------------------------------------- | ------------------------------------------ | -------- | -------- | -------- | -------- |
| `FastImage.preload: (source[]) => void`           | Preload images to display later. e.g.      | function | No       | All      | No       |
| `FastImage.clearMemoryCache: () => Promise<void>` | Clear all images from memory cache.        | function | No       | All      | no       |
| `FastImage.clearDiskCache: () => Promise<void>`   | Clear all images from disk cache. priority | function | No       | All      | no       |

## 遗留问题

- [ ] 部分涉及使用缓存能力的接口[issue#8](https://github.com/react-native-oh-library/react-native-fast-image/issues/8)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/DylanVann/react-native-fast-image/blob/main/LICENSE) ，请自由地享受和参与开源。
