> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/checkbox</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-checkbox/react-native-checkbox">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-checkbox/react-native-checkbox/blob/develop/LICENSE">
        <img src="https://img.shields.io/npm/l/@react-native-community/checkbox.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-checkbox)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/checkbox Releases](https://github.com/react-native-oh-library/react-native-checkbox/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/checkbox
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/checkbox
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import CheckBox from "@react-native-community/checkbox";
import { useState } from "react";

export default function CheckBoxExample() {
    const [value, setValue] = useState<boolean>(false)
    const [toggleCheckBox, setToggleCheckBox] = useState<boolean>(false)
    return (
        <CheckBox
            disabled={false}
            value={toggleCheckBox}
            style={{ width: 70, height: 70 }}
            tintColor={"red"}
            onCheckColor={"green"}
            onChange={(event) => {
                setValue(event.nativeEvent.value);
            }}
            onValueChange={(newValue) => {
                setToggleCheckBox(newValue);
            }}
        />
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/checkbox": "file:../../node_modules/@react-native-oh-tpl/checkbox/harmony/checkbox.har",
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

### 3.配置 CMakeLists 和引入 CheckboxPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/checkbox/src/main/cpp" ./checkbox)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_checkbox)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "CheckboxPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<CheckboxPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 Checkbox 组件

找到 `function buildCustomComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
    ...
+ import { RNCCheckbox, CHECKBOX_TYPE } from "@react-native-oh-tpl/checkbox"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    ...
+   if (ctx.componentName === CHECKBOX_TYPE) {
+     RNCCheckbox({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
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
+ CHECKBOX_TYPE
  ];
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/checkbox Releases](https://github.com/react-native-oh-library/react-native-checkbox/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                                                                                                                                   | Type     | Required | Platform    | HarmonyOS Support |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| -------- | -------- |-------------|------------------|
| `value`             | The value of the checkbox. If true the checkbox will be turned on. Default value is false.                                                                                                    | boolean  | No       | Android、iOS | yes              |
| `testID`            | Used to locate this view in end-to-end tests.                                                                                                                                                 | string   | No       | Android、iOS | yes              |
| `disabled`          | If true the user won't be able to toggle the checkbox. Default value is false.                                                                                                                | bool     | No       | Android、iOS | yes              |
| `onCheckColor`      | Color of the check box when it is selected.                                                                                                                                                   | Color    | No       | iOS         | yes              |
| `tintColor`         | Border color of the check box when it is not selected.                                                                                                                                        | Color    | No       | iOS         | yes              |
| `shape`             | Sets component shapes, including circles and rounded squares. Default value is 0.                                                                                                             | int      | No       | harmony     | yes              |
| `markSize`          | Size of the internal mark. The default size is the same as the width of the check box.This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used. | number   | No       | harmony     | yes              |
| `strokeWidth`       | Stroke width of the internal mark. This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used.                                                   | number   | No       | harmony     | yes              |
| `strokeColor`       | Color of the internal mark.                                                                                                                                                                   | Color    | No       | harmony     | yes              |
| `lineWidth`         | The width of the lines of the check mark and box. Defaults to 2.0.                                                                                                                            | number    | No       | iOS         | No               |
| `hideBox`           | Control if the box should be hidden or not. Defaults to false.                                                                                                                                | boolean    | No       | iOS         | No              |
| `onFillColor`       | The color of the inside of the box when it is On. Defaults to transparent.                                                                                                                    | string      | No       | iOS      | No              |
| `onTintColor`       | The color of the line around the box when it is On. Defaults to '#007aff'.                                                                                                                    | string   | No       | iOS      | No              |
| `animationDuration` | The duration in seconds of the animations. Defaults to 0.5.                                                                                                                                   | number   | No       | iOS     | No              |
| `onAnimationType`   | The type of animation to use when the checkbox gets checked. Default to 'stroke'.                                                                                                             | 'stroke' or 'fill' or 'bounce' or 'flat' or 'one-stroke' or 'fade'   | No       | iOS     | No              |
| `offAnimationType`   | The type of animation to use when the checkbox gets unchecked. 'stroke'.                                                                                                                      | 'stroke' or 'fill' or 'bounce' or 'flat' or 'one-stroke' or 'fade'   | No       | iOS     | No              |
## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                                                                                                                                                    | Type     | Required | Platform      | HarmonyOS Support |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------- | ----------------- |
| `onChange`      | Invoked on change with the native event.                                                                                                                                                       | function | No       | Android、iOS   | yes               |
| `onValueChange` | Invoked with the new boolean value when it changes.                                                                                                                                            | function | No       | Android、iOS   | yes               |

## 遗留问题
- [ ] 设置lineWidth属性，该属性用来控制复选框的线条宽度，未实现HarmonyOS化: [issue#3](https://github.com/react-native-oh-library/react-native-checkbox/issues/3)
- [ ] 设置hideBox属性，该属性用来控制复选框的显示与隐藏，未实现HarmonyOS化: [issue#4](https://github.com/react-native-oh-library/react-native-checkbox/issues/4)
- [ ] 设置onTintColor属性，该属性用来控制复选框的选中时边框的颜色，未实现HarmonyOS化: [issue#5](https://github.com/react-native-oh-library/react-native-checkbox/issues/5)
- [ ] 设置onFillColor属性，该属性用来控制复选框未选中时框内部的颜色，未实现HarmonyOS化: [issue#9](https://github.com/react-native-oh-library/react-native-checkbox/issues/9)
- [ ] 设置animationDuration属性，该属性用来控制选中和取消选中的动画持续时间，未实现HarmonyOS化: [issue#6](https://github.com/react-native-oh-library/react-native-checkbox/issues/6)
- [ ] 设置onAnimationType属性，该属性用来控制选中时的动画类型，未实现 HarmonyOS化: [issue#7](https://github.com/react-native-oh-library/react-native-checkbox/issues/7)
- [ ] 设置offAnimationType属性，该属性用来控制取消选中时的动画类型，未实现 HarmonyOS化: [issue#8](https://github.com/react-native-oh-library/react-native-checkbox/issues/8)
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-checkbox/blob/harmony/LICENSE) ，请自由地享受和参与开源。