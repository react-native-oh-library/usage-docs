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

## 安装与使用

目前 React-Native-OpenHarmony(RNOH) 三方库的 npm 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```bash
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-picker/picker@npm:@react-native-oh-library/picker
```

或者

```bash
npm install @react-native-picker/picker@npm:@react-native-oh-library/picker
```

下面的代码展示了这个库的基本使用场景：

```js
import { Picker } from "@react-native-picker/picker";

const [selectedLanguage, setSelectedLanguage] = useState();

<Picker
  selectedValue={selectedLanguage}
  onValueChange={(itemValue, itemIndex) => setSelectedLanguage(itemValue)}
>
  <Picker.Item label="Java" value="java" />
  <Picker.Item label="JavaScript" value="js" />
</Picker>;
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
    "rnoh-slider": "file:../../node_modules/'@react-native-picker/picker/harmony/picker.har"
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
    "rnoh-slider": "file:../../node_modules/'@react-native-picker/picker/harmony/picker"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 PickerPackge

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
+ #include "HarmonyPickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<HarmonyPickerPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 picker 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
import {
  RNApp,
  ComponentBuilderContext,
  RNAbility,
  AnyJSBundleProvider,
  MetroJSBundleProvider,
  ResourceJSBundleProvider,
} from 'rnoh'
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
import { createRNPackages } from '../RNPackagesFactory'
+ import { RNCHarmonyPicker, HARMONY_PICKER_TYPE } from "rnoh-picker"

@Entry
@Component
struct Index {
  @StorageLink('RNAbility') rnAbility: RNAbility | undefined = undefined

  @Builder
  buildCustomComponent(ctx: ComponentBuilderContext) {
    if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnohContext,
        tag: ctx.descriptor.tag,
        buildCustomComponent: this.buildCustomComponent.bind(this)
      })
    }
+   else if (ctx.descriptor.type === HARMONY_PICKER_TYPE) {
+     RNCHarmonyPicker({
+       ctx: ctx.rnohContext,
+       tag: ctx.descriptor.tag,
+       buildCustomComponent: this.buildCustomComponent.bind(this)
+     })
+   }
    ...
  }
  ...
}
```

### 运行

在右上角选择 entry 模块，运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

| `@react-native-oh-library/picker` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version  |
| ----------------------------------------- | ----------------------------- | --------------------- | ------------------------------ | --------------------- |
| `2.5.1-0.0.1`                             | `0.72.5`                      | `0.72.10`             | `4.0.3.601`                    | `OpenHarmony 4.10.10` |

## 属性

### PickerProps

| 名称                      | 说明                                                                                              | 类型                                                         | 是否必填 | 平台                  | 鸿蒙支持  |
| ------------------------- | ------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ | -------- | --------------------- | --------- |
| `onValueChange`           | Callback for when an item is selected.                                                            | function                                                     | No       | All                   | yes       |
| `selectedValue`           | Value matching value of one of the items. Can be a string or an integer.                          | any                                                          | No       | All                   | yes       |
| `style`                   | NA                                                                                                | pickerStyleType                                              | No       | All                   | yes       |
| `testID`                  | Used to locate this view in end-to-end tests.                                                     | string                                                       | No       | All                   | yes       |
| `enabled`                 | If set to false, the picker will be disabled, i.e. the user will not be able to make a selection. | bool                                                         | No       | Android, Web, Windows | no        |
| `mode`                    | On Android, specifies how to display the selection items when the user taps on the picker         | enum('dialog', 'dropdown')                                   | No       | Android               | no        |
| `dropdownIconColor`       | On Android, specifies color of dropdown triangle.                                                 | ColorValue                                                   | No       | Android               | no        |
| `dropdownIconRippleColor` | On Android, specifies ripple color of dropdown triangle.                                          | ColorValue                                                   | No       | Android               | no        |
| `prompt`                  | Prompt string for this picker, used on Android in dialog mode as the title of the dialog.         | string                                                       | No       | Android               | no        |
| `itemStyle`               | Style to apply to each of the item labels.                                                        | [text styles](https://reactnative.dev/docs/text-style-props) | No       | iOS, Windows          | partially |
| `numberOfLines`           | On Android & iOS, used to truncate the text with an ellipsis after computing the text layout.     | number                                                       | No       | Android, iOS          | no        |
| `onBlur`                  | NA                                                                                                | function                                                     | No       | Android               | no        |
| `onFocus`                 | NA                                                                                                | function                                                     | No       | Android               | no        |
| `selectionColor`          | NA                                                                                                | ColorValue                                                   | No       | iOS                   | no        |
| `themeVariant`            | NA                                                                                                | enum('light', 'dark')                                        | No       | iOS                   | no        |

### PickerItemProps

| 名称                 | 说明                                                                                                     | 类型          | 是否必填 | 平台    | 鸿蒙支持 |
| -------------------- | -------------------------------------------------------------------------------------------------------- | ------------- | -------- | ------- | -------- |
| `label`              | Displayed value on the Picker Item.                                                                      | string        | yes      | All     | yes      |
| `value`              | Actual value on the Picker Item.                                                                         | number,string | yes      | All     | yes      |
| `color`              | Displayed color on the Picker Item.                                                                      | ColorValue    | yes      | All     | no       |
| `label`              | Displayed value on the Picker Item.                                                                      | string        | no       | All     | yes      |
| `fontFamily`         | Displayed fontFamily on the Picker Item.                                                                 | string        | no       | All     | yes      |
| `style`              | Style to apply to individual item labels.                                                                | ViewStyleProp | no       | Android | yes      |
| `enabled`            | If set to false, the specific item will be disabled, i.e. the user will not be able to make a selection. | boolean       | no       | Android | no       |
| `contentDescription` | Sets the content description to the Picker Item.                                                         | string        | no       | Android | no       |

## 方法

| 名称    | 说明                            | 平台    | 鸿蒙支持 |
| ------- | ------------------------------- | ------- | -------- |
| `blur`  | Programmatically closes picker. | Android | no       |
| `focus` | Programmatically opens picker.  | Android | no       |

## 遗留问题

- [ ] numberOfLines 属性不支持[issue#2](https://github.com/react-native-oh-library/picker/issues/2)
- [ ] PickerItemProps 的 color 和 fontFamily 不支持（OH 的 Picker 组件不支持单独设置 PickerItem 的样式）
- [ ] themeVariant 属性不支持
- [ ] selectionColor 不支持
- [ ] itemStyle 不支持设置 textAlign（OH 的 Picker 不支持设置）

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。
