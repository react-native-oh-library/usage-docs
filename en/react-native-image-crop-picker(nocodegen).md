> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-image-crop-picker)

## Installation and Usage

Please visit the Releases page of the third-party library to check the compatible version information: [@react-native-oh-tpl/react-native-image-crop-picker Releases ](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases),and download the tgz package marked with nc, such as 0.40.3-nc.0.0.9.

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```
npm install @react-native-oh-tpl/react-native-image-crop-picker@file:#
```

#### **yarn**

```
yarn add @react-native-oh-tpl/react-native-image-crop-picker@file:#
```

The usage scenario is the same [react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#yarn)

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

```
Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 1. Configuration Entry
 
**(1) Create ImageEditAbility.ets under entry/src/main/ets/entryability**

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

**(2) Register ImageEditAbility in entry/src/main/module.json5 and add requestPermissions**

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
]

```

**(3) Create ImageEdit.ets under entry/src/main/ets/pages**

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

**(4) Add configuration in entry/src/main/resources/base/profile/main_pages.json**

```json
{
 "src": [
  "pages/Index",
  "pages/ImageEdit"
 ]
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-crop-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-image-crop-picker/harmony/image_crop_picker.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing ImageCropPickerPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+  ${IMAGE_CROP_PICKER_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_image_crop_picker)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-image-crop-picker Releases ](https://github.com/react-native-oh-library/react-native-image-crop-picker/releases)

## API

[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#api)

## Properties

[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#%E5%B1%9E%E6%80%A7)

## Known Issues

[react-native-image-crop-picker](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-crop-picker.md#%E9%81%97%E7%95%99%E9%97%AE%E9%A2%98)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ivpusic/react-native-image-crop-picker/blob/master/LICENSE).

