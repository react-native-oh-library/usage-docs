> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-image-picker/react-native-image-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-image-picker/react-native-image-picker/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-image-picker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-picker Releases](https://github.com/react-native-oh-library/react-native-image-picker/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-picker
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-picker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Text } from 'react-native';
import { launchImageLibrary } from 'react-native-image-picker';

const App = () => {
  const [urlInfo, setUrlInfo] = React.useState<string>();
  return (
    <View style={{ flex: 1, marginTop: 100 }}>
      <View style={{
        width: 160,
        height: 36,
        backgroundColor: 'hsl(190,50%,70%)',
        paddingHorizontal: 16,
        paddingVertical: 8,
        borderRadius: 8
      }} onTouchEnd={() => {
        launchImageLibrary({ mediaType: 'photo', selectionLimit: 1 }, (data) => {
          if (data.assets?.length) {
            setUrlInfo(JSON.stringify(data.assets))
          }
        })
      }}>
        <Text style={{ width: '100%', height: '100%', fontWeight: 'bold', textAlign: 'center' }}>选择</Text>
      </View>
      <Text>{urlInfo}</Text>
    </View>
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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-image-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-image-picker/harmony/image_picker.har"
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

### 3.配置 CMakeLists 和引入 ImagePickerViewPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-image-picker/src/main/cpp" ./image_picker)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_picker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNImagePickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNImagePickerPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 ImagePickerViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ImagePickerViewPackage } from '@react-native-oh-tpl/react-native-image-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImagePickerViewPackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-picker Releases](https://github.com/react-native-oh-library/react-native-image-picker/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Options

| Name                    | Description                                                                                                                                                                      | Type    | Required | Platform        | HarmonyOS Support |
| ----------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | --------------- | ----------------- |
| mediaType               | photo or video or mixed(launchCamera on Android does not support 'mixed'). Web only supports 'photo' for now.                                                                    | string  | yes      | iOS Android Web | yes               |
| maxWidth                | To resize the image.                                                                                                                                                             | number  | no       | iOS Android     | no                |
| maxHeight               | To resize the image.                                                                                                                                                             | number  | no       | iOS Android     | no                |
| videoQuality            | low, medium, or high on iOS, low or high on Android.                                                                                                                             | string  | no       | iOS Android     | no                |
| durationLimit           | Video max duration (in seconds).                                                                                                                                                 | number  | no       | iOS Android     | no                |
| quality                 | 0 to 1, photos.                                                                                                                                                                  | number  | no       | iOS Android     | no                |
| cameraType              | 'back' or 'front' (May not be supported in few android devices).                                                                                                                 | string  | no       | iOS Android     | yes                |
| includeBase64           | If true, creates base64 string of the image (Avoid using on large image files due to performance).                                                                               | boolean | no       | iOS Android Web | yes                |
| includeExtra            | If true, will include extra data which requires library permissions to be requested (i.e. exif data).                                                                            | boolean | no       | iOS Android     | no                |
| saveToPhotos            | (Boolean) Only for launchCamera, saves the image/video file captured to public photo.                                                                                            | boolean | no       | iOS Android     | no                |
| selectionLimit          | Supports providing any integer value. Use 0 to allow any number of files on iOS version >= 14 & Android version >= 13, Use 0 to allow up to 50 files on HarmonyOS. Default is 1. | number  | no       | iOS Android Web | yes               |
| presentationStyle       | Controls how the picker is presented. currentContext, pageSheet, fullScreen, formSheet, popover, overFullScreen, overCurrentContext. Default is currentContext.                  | string  | no       | iOS             | no                |
| formatAsMp4             | Converts the selected video to MP4 (iOS Only).                                                                                                                                   | boolean | no       | iOS             | no                |
| assetRepresentationMode | A mode that determines which representation to use if an asset contains more than one. Possible values: 'auto', 'current', 'compatible'. Default is 'auto'.                      | string | no       | iOS             | no                |

### The Response Object

| Name         | Description                                             | Type    | Required | Platform        | HarmonyOS Support |
| ------------ | ------------------------------------------------------- | ------- | -------- | --------------- | ----------------- |
| didCancel    | true if the user cancelled the process                  | boolean | no       | iOS Android Web | yes               |
| errorCode    | Check ErrorCode for all error codes                     | string  | no       | iOS Android Web | no                |
| errorMessage | Description of the error, use it for debug purpose only | string  | no       | iOS Android Web | no                |
| assets       | Array of the selected media, refer to Asset Object      | Asset   | no       | iOS Android Web | yes               |

### Asset Object

| Name         | Description                                                                                                                                                                                                                                                                | Type   | Required | Platform        | HarmonyOS Support |
| ------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | --------------- | ----------------- |
| base64       | The base64 string of the image (photos only)                                                                                                                                                                                                                               | string | no       | iOS Android Web | yes                |
| uri          | The file uri in app specific cache storage. Except when picking video from Android gallery where you will get read only content uri, to get file uri in this case copy the file to app specific storage using any react-native library. For web it uses the base64 as uri. | string | yes      | iOS Android Web | yes               |
| originalPath | The original file path.                                                                                                                                                                                                                                                    | string | yes      | iOS Android Web | yes               |
| width        | Asset dimensions                                                                                                                                                                                                                                                           | number | yes      | iOS Android Web | yes               |
| height       | Asset dimensions                                                                                                                                                                                                                                                           | number | yes      | iOS Android Web | yes               |
| fileSize     | The file size                                                                                                                                                                                                                                                              | number | yes      | iOS Android     | yes               |
| type         | The file type                                                                                                                                                                                                                                                              | string | yes      | iOS Android     | yes               |
| fileName     | The file name                                                                                                                                                                                                                                                              | string | yes      | iOS Android     | yes               |
| duration     | The selected video duration in seconds                                                                                                                                                                                                                                     | number | no       | iOS Android     | no                |
| bitrate      | The average bitrate (in bits/sec) of the selected video, if available. (Android only)                                                                                                                                                                                      | number | no       | Android         | no                |
| timestamp    | Timestamp of the asset. Only included if 'includeExtra' is true                                                                                                                                                                                                            | string | no       | iOS Android     | no                |
| id           | local identifier of the photo or video. On Android & HarmonyOS, this is the same as | string | no       | iOS Android     | yes                |

## 静态方法

| Name               | Description                            | Type     | Required | Platform        | HarmonyOS Support |
| ------------------ | -------------------------------------- | -------- | -------- | --------------- | ----------------- |
| launchCamera       | Launch camera to take photo or video.  | function | yes      | iOS Android Web | yes                |
| launchImageLibrary | Launch gallery to pick image or video. | function | yes      | iOS Android Web | yes               |

## 遗留问题

- [ ] image-picker部分属性未实现 HarmonyOS 化: [issue#14](https://github.com/react-native-oh-library/react-native-image-picker/issues/14)
- [x] 只实现了选择图库的接口属性，相机功能暂未适配: [issue#13](https://github.com/react-native-oh-library/react-native-image-picker/issues/13)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-image-picker/react-native-image-picker/blob/main/LICENSE.md) ，请自由地享受和参与开源。