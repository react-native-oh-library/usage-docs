> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>@react-native-picker/picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-picker/picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20macos%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-picker/picker/blob/main/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-picker/picker.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/picker)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add @react-native-picker/picker@npm:@react-native-oh-library/picker
```

#### **npm**

```bash
npm install @react-native-picker/picker@npm:@react-native-oh-library/picker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import {Picker} from '@react-native-picker/picker';

const [selectedLanguage, setSelectedLanguage] = useState();

<Picker
  selectedValue={selectedLanguage}
  onValueChange={(itemValue, itemIndex) =>
    setSelectedLanguage(itemValue)
  }>
  <Picker.Item label="Java" value="java" />
  <Picker.Item label="JavaScript" value="js" />
</Picker>
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
    "rnoh-picker": "file:../../node_modules/@react-native-picker/picker/harmony/picker.har"
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
    "rnoh-picker": "file:../../node_modules/@react-native-picker/picker/harmony/picker"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 PickerPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-picker/src/main/cpp" ./picker)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_picker)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "PickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<PickerPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 PickerPackage 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
...
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
+ import { RNCPicker, PICKER_TYPE } from "rnoh-picker"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === PICKER_TYPE) {
+   RNCPicker({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag
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

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/picker Releases](https://github.com/react-native-oh-library/picker/releases)

## 属性

> [!tip] "鸿蒙支持"列为 yes 的 API 表示支持鸿蒙平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                              | Type          | Required | Platform | HarmonyOS Support |
| --------------- | ---------------------------------------- | ------------- | -------- | -------- | ----------------- |
| `onValueChange` | Callback for when an item is selected.   | function      | No       | All      | yes               |
| `selectedValue` | Value matching value of one of the items | any           | No       | All      | yes               |
| `label`         | Displayed value on the Picker Itemtests. | string        | yes      | All      | yes               |
| `value`         | Actual value on the Picker Item.         | number,string | yes      | All      | yes               |

## 遗留问题

- [ ] 部分接口，未适配

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/picker/blob/harmony/LICENSE) ，请自由地享受和参与开源。