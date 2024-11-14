> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/beefe/react-native-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-picker)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-picker Releases](https://github.com/react-native-oh-library/react-native-picker/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-picker
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-picker
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { View, Button } from 'react-native';
import Picker from 'react-native-picker';

const MyPicker = () => {
  let data = {
    pickerData:
      [{
        a: [
          {
            a1: [1, 2, 3, 4]
          },
          {
            a2: [5, 6, 7, 8]
          },
          {
            a3: [9, 10, 11, 12]
          }
        ]
      },
      {
        b: [
          {
            b1: [11, 22, 33, 44]
          },
          {
            b2: [55, 66, 77, 88]
          },
          {
            b3: [99, 1010, 1111, 1212]
          }
        ]
      },
      {
        c: [
          {
            c1: ['a', 'b', 'c']
          },
          {
            c2: ['aa', 'bb', 'cc']
          },
          {
            c3: ['aaa', 'bbb', 'ccc']
          }
        ]
      },],
    isLoop: false,
    selectedValue: ['b', 'b1', 22],
    onPickerConfirm: data => {
      console.log('onPickerConfirm:', data)
    },
    onPickerCancel: data => {
      console.log('onPickerCancel:', data);
    },
    onPickerSelect: data => {
      console.log('onPickerSelect:', data);
    }
  }
  return (
    <View>
      <Button title='initPicker' onPress={() => Picker.init(data)} />
      <Button title='showPicker' onPress={() => Picker.show()} />
    </View>
  );
};

export default MyPicker;
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

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-picker/harmony/picker.har"
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

### 3. Configuring CMakeLists and Introducing PickerPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-picker/src/main/cpp" ./picker)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_native_picker)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "PickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<PickerPackage>(ctx),
    };
}
```

### 4.Introducing PickerViewPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { PickerViewPackage } from "@react-native-oh-tpl/react-native-picker/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+  new PickerViewPackage(ctx),
  ];
}
```

### 5.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-picker Releases](https://github.com/react-native-oh-library/react-native-picker/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- |---------|---------| ------ | ----------- |-------------------|
|isLoop                | 列的内容是否可以循环 | boolean      | yes   |    Android   | yes               |
|pickerTextEllipsisLen | 文本的起始省略长度 | number       | yes   |    Android   | no                |
|pickerConfirmBtnText  | 确认按钮的文本内容 | string       | yes   |iOS/Android  | yes               |
|pickerCancelBtnText   | 取消按钮的文本内容 | string       | yes   |iOS/Android  | yes               |
|pickerTitleText       | 顶部标题的文本内容 | string       | yes   |iOS/Android  | yes               |
|pickerConfirmBtnColor | 确认按钮的字体颜色 | array        | yes   |iOS/Android  | yes               |
|pickerCancelBtnColor  | 取消按钮的字体颜色 | array        | yes   |iOS/Android  | yes               |
|pickerTitleColor      | 顶部标题的字体颜色 | array        | yes   |iOS/Android  | yes               |
|pickerToolBarBg       | 顶部ToolBar的背景色 | array        | yes   |iOS/Android  | yes               |
|pickerBg              | picker的背景色 | array        | yes   |iOS/Android  | yes               |
|pickerToolBarFontSize | 顶部ToolBar文本的字体大小 | number       | yes   |iOS/Android  | yes               |
|wheelFlex             | picker每一列所占的比例 | array        | yes   |iOS/Android  | no                |
|pickerFontSize        | picker选择器字体内容的大小 | number       | yes   |iOS/Android  | yes               |
|pickerFontColor       | picker选择器的字体颜色 | array        | yes   |iOS/Android  | yes               |
|pickerFontFamily      | picker选择器的字体样式 | string       | no    |iOS/Android  | no                |
|pickerRowHeight       | picker选择器的行高 | number       | yes   |iOS           | yes               |
|pickerData            | picker选择器所填充的数据 | array        |  no   |iOS/Android  | yes               |
|selectedValue         | picker选择器所选的默认值 | array        |  no   |iOS/Android  | yes               |
|onPickerConfirm       | 点击确认按钮触发的回调函数 | function     |  no   |iOS/Android  | yes               |
|onPickerCancel        | 点击取消按钮触发的回调函数 | function     | no    |iOS/Android  | yes               |
|onPickerSelect        | 当picker的选择内容发生改变时触发的回调函数 | function     | no    |iOS/Android   | yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type     | Required | Platform    | HarmonyOS Support |
| --- |----------|----------|----------|-------------|-------------------|
|init        |init and pass parameters to picker      | function | no       | iOS/Android | yes               |
|toggle      |show or hide picker                     | function | no       | iOS/Android | yes               |
|show        |show picker                             | function | no       | iOS/Android | yes               |
|hide        |hide picker                             | function | no       | iOS/Android | yes               |
|select      |select a row                            | function | no       | iOS/Android | yes                |
|isPickerShow|get status of picker, return a boolean  | function | no       | iOS/Android | yes               |

## Known Issues

- [ ] 当前picker是使用的TextPicker实现，TextPicker并未提供每列设置宽度的方法，因此暂不能支持wheelFlex。[issue#6](https://github.com/react-native-oh-library/react-native-picker/issues/6)
- [ ] 当前TextPicker的字体设置目前只支持大小和字体粗细，不支持pickerFontFamily。[issue#7](https://github.com/react-native-oh-library/react-native-picker/issues/7)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://mit-license.org/).
