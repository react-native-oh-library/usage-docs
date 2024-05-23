> 模板版本：v0.1.3

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

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-cameraroll Releases](https://github.com/react-native-oh-library/react-native-cameraroll/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/camera-roll@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/camera-roll@file:#
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

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

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "rnoh-camera-roll": "file:../../node_modules/@react-native-oh-tpl/camera-roll/harmony/camera_roll.har"
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

### 在 ArkTs 侧引入 CameraRollPackage

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

### 应用权限申请

> [!tip] "ohos.permission.READ_IMAGEVIDEO"，"ohos.permission.WRITE_IMAGEVIDEO"权限等级为<B>system_basic</B>，授权方式为<B>user_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.READ_IMAGEVIDEO" },
+     { "name": "ohos.permission.WRITE_IMAGEVIDEO" }
    ]
  }
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
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| saveToCameraRoll | 保存图片/视频 | function | no | android,ios | no |
| getPhotos | 查找图片/视频 | function | no | android,ios | partially |
| getAlbums | 查找相册 | function | no | android,ios | partially |
| deletePhotos | 删除图片/视频 | function | no | android,ios | no |
| iosGetImageDataById | 获取图片数据 | function | no | ios | partially |
| getPhotoThumbnail | 获取缩略图 | function | no | ios | partially |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                       | Description                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------ | ------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `iosReadGalleryPermission`                 | 权限验证                                   | function | no       | ios      | no                |
| `iosRequestReadWriteGalleryPermission`     | 读写权限申请                               | function | no       | ios      | no                |
| `iosRequestAddOnlyGalleryPermission`       | 添加权限申请                               | function | no       | ios      | no                |
| `iosRefreshGallerySelection`               | 图片列表刷新                               | function | no       | ios      | no                |
| `harmonyReadGalleryPermission`             | 对比`iosReadGalleryPermission`             | function | no       | harmony  | yes               |
| `harmonyRequestReadWriteGalleryPermission` | 对比`iosRequestReadWriteGalleryPermission` | function | no       | harmony  | yes               |
| `harmonyRequestAddOnlyGalleryPermission`   | 对比`iosRequestAddOnlyGalleryPermission`   | function | no       | harmony  | yes               |
| `harmonyRefreshGallerySelection`           | 对比`iosRefreshGallerySelection`           | function | no       | harmony  | no                |

## 遗留问题

- [ ] harmony 保存图片/视频到指定相册需要使用系统接口
- [ ] harmony 查找图片/视频部分查询条件和返回字段需要使用系统接口
- [ ] harmony 纯图片相册暂未对外开放，系统相册不返回相册名
- [ ] harmony 删除图片/视频需要使用系统接口
- [ ] harmony 暂无对标 ios 图片列表刷新的方法

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE) ，请自由地享受和参与开源。
