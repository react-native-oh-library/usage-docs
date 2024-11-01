> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-picker/picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-picker/picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-picker/picker/blob/master/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-picker/picker.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/picker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/picker Releases](https://github.com/react-native-oh-library/picker/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/picker@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/picker@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from "react";
import { Picker } from "@react-native-oh-tpl/picker";
import { View } from "react-native";

export const PickerExample = ()=>{
  const [selectedLanguage, setSelectedLanguage] = React.useState();

  return (
    <View style={{backgroundColor:"#fff",padding:40}}>
      <Picker
        selectedValue={selectedLanguage}
        onValueChange={(itemValue, itemIndex) => setSelectedLanguage(itemValue)}>
        <Picker.Item label="Java" value="java" />
        <Picker.Item label="JavaScript" value="js" />
      </Picker>
    </View>
  )
}
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
        
    "@react-native-oh-tpl/picker": "file:../../node_modules/@react-native-oh-tpl/picker/harmony/picker.har",
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

### 3.配置 CMakeLists 和引入 PickerPackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/picker/src/main/cpp" ./picker)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_picker)
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
+     std::make_shared<PickerPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 picker 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNCPicker, PICKER_TYPE } from "@react-native-oh-tpl/picker"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    ...
+   if (ctx.componentName === PICKER_TYPE) {
+     RNCPicker({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag
+     })
+   }
    ...
  }
  ...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ PICKER_TYPE
  ];
```

### 5.在 ArkTs 侧引入 RNCPickerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNCPickerPackage } from '@react-native-oh-tpl/picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCPickerPackage(ctx)
  ];
}
```

### 6.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/picker Releases](https://github.com/react-native-oh-library/picker/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；No 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### PickerProps

| Name                      | Description                                                                                       | Type                                                         | Required | Platform              | HarmonyOS Support |
|---------------------------|---------------------------------------------------------------------------------------------------|--------------------------------------------------------------|----------|-----------------------|-------------------|
| `onValueChange`           | Callback for when an item is selected.                                                            | function                                                     | No       | All                   | Yes               |
| `selectedValue`           | Value matching value of one of the items. Can be a string or an integer.                          | any                                                          | No       | All                   | Yes               |
| `style`                   | NA                                                                                                | pickerStyleType                                              | No       | All                   | Yes               |
| `testID`                  | Used to locate this view in end-to-end tests.                                                     | string                                                       | No       | All                   | Yes               |
| `enabled`                 | If set to false, the picker will be disabled, i.e. the user will not be able to make a selection. | boolean                                                      | No       | Android, Web, Windows | Yes               |
| `mode`                    | On Android, specifies how to display the selection items when the user taps on the picker         | enum('dialog', 'dropdown')                                   | No       | Android               | No                |
| `dropdownIconColor`       | On Android, specifies color of dropdown triangle.                                                 | ColorValue                                                   | No       | Android               | No                |
| `dropdownIconRippleColor` | On Android, specifies ripple color of dropdown triangle.                                          | ColorValue                                                   | No       | Android               | No                |
| `prompt`                  | Prompt string for this picker, used on Android in dialog mode as the title of the dialog.         | string                                                       | No       | Android               | No                |
| `itemStyle`               | Style to apply to each of the item labels.                                                        | [text styles](https://reactnative.dev/docs/text-style-props) | No       | iOS, Windows          | partially         |
| `numberOfLines`           | On Android & iOS, used to truncate the text with an ellipsis after computing the text layout.     | number                                                       | No       | Android, iOS          | No                |
| `onBlur`                  | NA                                                                                                | function                                                     | No       | Android               | No                |
| `onFocus`                 | NA                                                                                                | function                                                     | No       | Android               | No                |
| `selectionColor`          | Color to apply to the selection indicator.                                                        | ColorValue                                                   | No       | iOS                   | Yes               |
| `themeVariant`            | NA                                                                                                | enum('light', 'dark')                                        | No       | iOS                   | No                |

### PickerItemProps

| Name                 | Description                                                                                              | Type          | Required | Platform | HarmonyOS Support |
|----------------------|----------------------------------------------------------------------------------------------------------|---------------|----------|----------|-------------------|
| `label`              | Displayed value on the Picker Item.                                                                      | string        | Yes      | All      | Yes               |
| `value`              | Actual value on the Picker Item.                                                                         | number,string | Yes      | All      | Yes               |
| `color`              | Displayed color on the Picker Item.                                                                      | ColorValue    | Yes      | All      | No                |
| `fontFamily`         | Displayed fontFamily on the Picker Item.                                                                 | string        | No       | All      | No                |
| `style`              | Style to apply to individual item labels.                                                                | ViewStyleProp | No       | Android  | No                |
| `enabled`            | If set to false, the specific item will be disabled, i.e. the user will not be able to make a selection. | boolean       | No       | Android  | No                |
| `contentDescription` | Sets the content description to the Picker Item.                                                         | string        | No       | Android  | No                |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description                     | Type     | Required | Platform | HarmonyOS Support |
|---------|---------------------------------|----------|----------|----------|-------------------|
| `blur`  | Programmatically closes picker. | function | No       | Android  | No                |
| `focus` | Programmatically opens picker.  | function | No       | Android  | No                |

## 遗留问题

- [ ] numberOfLines 属性不支持[issue#2](https://github.com/react-native-oh-library/picker/issues/2)
- [ ] PickerItemProps 的 color 和 fontFamily 不支持（OH 的 Picker 组件不支持单独设置 PickerItem 的样式） [issue#21](https://github.com/react-native-oh-library/picker/issues/21)
- [ ] themeVariant 属性不支持[issue#22](https://github.com/react-native-oh-library/picker/issues/22)
- [ ] itemStyle 不支持设置 textAlign（OH 的 Picker 不支持设置）[issue#23](https://github.com/react-native-oh-library/picker/issues/23)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/picker/blob/sig/LICENSE) ，请自由地享受和参与开源。
