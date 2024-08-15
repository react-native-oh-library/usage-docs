> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-crop-picker（nocodegen）</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ivpusic/react-native-image-crop-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/ivpusic/react-native-image-crop-picker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-crop-picker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-crop-picker Releases ](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases)，并下载带有 `nc` 标识的 tgz 包，如 `0.40.3-nc.0.0.9`。

进入到工程目录并输入以下命令：

> [!TIP] #处替换为 tgz 包的路径

#### **npm**

```
npm install @react-native-oh-tpl/react-native-image-crop-picker@file:#
```

#### **yarn**

```
yarn add @react-native-oh-tpl/react-native-image-crop-picker@file:#
```

使用场景同[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#yarn)

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 harmony

```
在工程根目录的 oh-package.json5 添加 overrides字段
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 配置 Entry

**1.在 entry/src/main/ets/entryability 下创建 ImageEditAbility.ets**

```ts
import UIAbility from '@ohos.app.ability.UIAbility'
import window from '@ohos.window'

const TAG = 'ImageEditAbility';

export default class ImageEditAbility extends UIAbility {

  onWindowStageCreate(windowStage: window.WindowStage) {
    this.setWindowOrientation(windowStage, window.Orientation.PORTRAIT)
    windowStage.loadContent('pages/ImageEdit', (err, data) => {
      if (err.code) {
        console.info(TAG,'Failed to load the content. Cause: %{public}s',
          JSON.stringify(err) ?? '')
        return;
      }
      console.info(TAG,'Succeeded in loading the content')
    });
    try {
      windowStage.getMainWindowSync().setWindowLayoutFullScreen(true, (err)=>{
        if (err.code) {
          console.error('Failed to enable the full-screen mode. Cause: ' + JSON.stringify(err));
          return;
        }
        console.info('Succeeded in enabling the full-screen mode.');
      })
    } catch (exception) {
      console.error('Failed to set the system bar to be invisible. Cause: ' + JSON.stringify(exception));
    }
  }

  setWindowOrientation(stage: window.WindowStage, orientation: window.Orientation): void {
    console.info(TAG,"into setWindowOrientation :")
    if (!stage || !orientation) {
      return;
    }
    stage.getMainWindow().then(windowInstance => {
      windowInstance.setPreferredOrientation(orientation);
    })
  }

  onBackground() {
    this.context.terminateSelf();
  }
}
```

**2.在 entry/src/main/module.json5 注册 ImageEditAbility 并添加 requestPermissions**

```json
"abilities":[{
        "name": "ImageEditAbility",
        "srcEntry": "./ets/entryability/ImageEditAbility.ets",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "startWindowIcon": "$media:startIcon",
        "startWindowBackground": "$color:start_window_background",
        "removeMissionAfterTerminate": true,

}
...
],
"requestPermissions": [
      {
        "name": "ohos.permission.MEDIA_LOCATION",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "ImageEditAbility"
          ],
          "when": "inuse"
        }
      },
      {
        "name": "ohos.permission.READ_MEDIA",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "ImageEditAbility"
          ],
          "when": "inuse"
        }
      },
      {
        "name": "ohos.permission.WRITE_MEDIA",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "ImageEditAbility"
          ],
          "when": "inuse"
        }
      }
    ]

```

**3.在 entry/src/main/ets/pages 下创建 ImageEdit.ets**

```ts
import { ImageEditInfo } from '@react-native-oh-tpl/react-native-image-crop-picker';

@Entry
@Component
struct ImageEdit {

 build() {
  Row(){
   Column(){
    ImageEditInfo();
   }
   .width('100%')
  }
  .height('100%')
 }
}
```

**4.在 entry/src/main/resources/base/profile/main_pages.json 添加配置**

```json
{
 "src": [
  "pages/Index",
  "pages/ImageEdit"
 ]
}
```

**5.打开 entry/src/main/resources/base/element/string.json，添加**

```json
{
  "string": [
    {
     "name": "reason",
      "value": "Access Write Media"
   }
  ]
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入。
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-crop-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-image-crop-picker/harmony/image_crop_picker.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)

### 配置 CMakeLists 和引入 ImageCropPickerPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-image-crop-picker/src/main/cpp" ./image-crop-picker)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")
+ file(GLOB IMAGE_CROP_PICKER_CPP_FILES "${OH_MODULES}/@react-native-oh-tpl/react-native-image-crop-picker/src/main/cpp/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
+  ${IMAGE_CROP_PICKER_CPP_FILES }
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_image-crop-picker)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ImageCropPickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+ std::make_shared<ImageCropPickerPackage>(ctx),
    };
}

```

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ImageCropPickerPackage } from "@react-native-oh-tpl/react-native-image-crop-picker/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageCropPickerPackage (ctx),
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-crop-picker Releases ](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases)

## API

同[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#api)

## 属性

同[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#%E5%B1%9E%E6%80%A7)

## 遗留问题

同[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#%E9%81%97%E7%95%99%E9%97%AE%E9%A2%98)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ivpusic/react-native-image-crop-picker/blob/master/LICENSE) ，请自由地享受和参与开源。

