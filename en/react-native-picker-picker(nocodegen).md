> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/picker)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/picker Releases](https://github.com/react-native-oh-library/picker/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
        
    "@react-native-oh-tpl/picker": "file:../../node_modules/@react-native-oh-tpl/picker/harmony/picker.har",
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

### 3. Configuring CMakeLists and Introducing PickerPackge

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
+     std::make_shared<PickerPackage>(ctx)
    };
}
```

### 4. Introducing picker Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

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

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ PICKER_TYPE
  ];
```

### 5. Introducing RNCPickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 6. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/picker Releases](https://github.com/react-native-oh-library/picker/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                     | Type     | Required | Platform | HarmonyOS Support |
|---------|---------------------------------|----------|----------|----------|-------------------|
| `blur`  | Programmatically closes picker. | function | No       | Android  | No                |
| `focus` | Programmatically opens picker.  | function | No       | Android  | No                |

## Known Issues

- [ ] numberOfLines 属性不支持[issue#2](https://github.com/react-native-oh-library/picker/issues/2)
- [ ] PickerItemProps 的 color 和 fontFamily 不支持（OH 的 Picker 组件不支持单独设置 PickerItem 的样式） [issue#21](https://github.com/react-native-oh-library/picker/issues/21)
- [ ] themeVariant 属性不支持[issue#22](https://github.com/react-native-oh-library/picker/issues/22)
- [ ] itemStyle 不支持设置 textAlign（OH 的 Picker 不支持设置）[issue#23](https://github.com/react-native-oh-library/picker/issues/23)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/picker/blob/sig/LICENSE).
