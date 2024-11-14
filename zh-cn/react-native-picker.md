> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-picker </h1>
</p>
<p align="center">
    <a href="https://github.com/beefe/react-native-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-picker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-picker Releases](https://github.com/react-native-oh-library/react-native-picker/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-picker/harmony/picker.har"
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

### 3.配置 CMakeLists 和引入 PickerPackage

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 4.在 ArkTs 侧引入 PickerViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { PickerViewPackage } from "@react-native-oh-tpl/react-native-picker/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+  new PickerViewPackage(ctx),
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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-picker Releases](https://github.com/react-native-oh-library/react-native-picker/releases)


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| --- |----------|---------| ------ | ----------- |-------------------|
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

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type     | Required | Platform    | HarmonyOS Support |
| --- |----------|----------|----------|-------------|-------------------|
|init        |init and pass parameters to picker      | function | no       | iOS/Android | yes               |
|toggle      |show or hide picker                     | function | no       | iOS/Android | yes               |
|show        |show picker                             | function | no       | iOS/Android | yes               |
|hide        |hide picker                             | function | no       | iOS/Android | yes               |
|select      |select a row                            | function | no       | iOS/Android | yes                |
|isPickerShow|get status of picker, return a boolean  | function | no       | iOS/Android | yes               |

## 遗留问题

- [ ] 当前picker是使用的TextPicker实现，TextPicker并未提供每列设置宽度的方法，因此暂不能支持wheelFlex。[issue#6](https://github.com/react-native-oh-library/react-native-picker/issues/6)
- [ ] 当前TextPicker的字体设置目前只支持大小和字体粗细，不支持pickerFontFamily。[issue#7](https://github.com/react-native-oh-library/react-native-picker/issues/7)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://mit-license.org/) ，请自由地享受和参与开源。