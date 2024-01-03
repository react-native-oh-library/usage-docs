> 模板版本：v0.1.1

<p align="center">
  <h1 align="center"> <code>react-native-cameraroll</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-cameraroll/react-native-cameraroll">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/react-native-cameraroll/react-native-cameraroll/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-cameraroll)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add @react-native-oh-tpl/camera-roll
```

#### **npm**

```bash
npm install @react-native-oh-tpl/camera-roll
```

<!-- tabs:end -->

快速使用：

```js
import { View, Button } from "react-native";
import {
  CameraRoll,
  harmonyRequestAddOnlyGalleryPermission,
  harmonyRequestReadWriteGalleryPermission,
} from "react-native-camera-roll/camera-roll";

export default function App() {
  return (
    <View>
      <Button
        title="getPhotos"
        onPress={() => {
          CameraRoll.getPhotos({ first: 10 }).then((photos) => {
            // TODO
          });
        }}
      />
      <Button
        title="getAlbums"
        onPress={() => {
          CameraRoll.getAlbums({ assetType: "All" }).then((albums) => {
            // TODO
          });
        }}
      />
      <Button
        title="harmonyRequestAddOnlyGalleryPermission"
        onPress={() => {
          harmonyRequestAddOnlyGalleryPermission().then((status) => {
            // TODO
          });
        }}
      />
      <Button
        title="harmonyRequestReadWriteGalleryPermission"
        onPress={() => {
          harmonyRequestReadWriteGalleryPermission().then((status) => {
            // TODO
          });
        }}
      />
    </View>
  );
}
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
    "rnoh-camera-roll": "file:../../node_modules/@react-native-tpl-oh/camera-roll/harmony/camera_roll.har"
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
    "rnoh-camera-roll": "file:../../node_modules/@react-native-tpl-oh/camera-roll/harmony/camera_roll"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 CameraRollPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-camera-roll/src/main/cpp" ./camera-roll)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_camera_roll)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "CameraRollPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<CameraRollPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 Gesture Handler Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { CameraRollPackage } from 'rnoh-camera-roll/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CameraRollPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/camera-roll Releases](https://github.com/react-native-oh-library/react-native-cameraroll/releases)

## 静态方法
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**CameraRoll**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| saveToCameraRoll | 保存图片/视频 | function | no | android,ios | no   |
| getPhotos | 查找图片/视频 | function | no   | android,ios | partially |
| getAlbums | 查找相册 | function | no   | android,ios      | partially |
| deletePhotos | 删除图片/视频 | function | no  | android,ios  | no     |
| iosGetImageDataById | 获取图片数据 | function | no  | ios    | no     |
| getPhotoThumbnail | 获取缩略图 | function | no     | ios     | no     |



## API
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| `iosReadGalleryPermission` | 权限验证 | function | no    | ios  | no  |
| `iosRequestReadWriteGalleryPermission` | 读写权限申请 | function | no  | ios  | no      |
| `iosRequestAddOnlyGalleryPermission` | 添加权限申请 | function | no  | ios  | no      |
| `iosRefreshGallerySelection` | 图片列表刷新 | function | no   | ios   | no  |
| `harmonyReadGalleryPermission` | 对比`iosReadGalleryPermission` | function | no    | harmony  | no  |
| `harmonyRequestReadWriteGalleryPermission` | 对比`iosRequestReadWriteGalleryPermission` | function | no  | harmony  | partially      |
| `harmonyRequestAddOnlyGalleryPermission` | 对比`iosRequestAddOnlyGalleryPermission` | function | no  | harmony  | partially      |
| `harmonyRefreshGallerySelection` | 对比`iosRefreshGallerySelection` | function | no   | harmony   | no  |


## 遗留问题

- [ ] harmony 保存图片/视频到指定相册需要使用系统接口
- [ ] harmony 查找图片/视频部分查询条件和返回字段需要使用系统接口
- [ ] harmony 纯图片相册暂未对外开放，系统相册不返回相册名
- [ ] harmony 删除图片/视频需要使用系统接口
- [ ] harmony 权限验证需要应用tokenID,获取tokenID需要使用系统接口
- [ ] harmony 权限申请需要先验证权限，当前跳过验证，直接申请
- [ ] harmony 暂无对标ios图片列表刷新的方法

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE) ，请自由地享受和参与开源。
