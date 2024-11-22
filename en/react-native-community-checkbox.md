> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-checkbox)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/checkbox Releases](https://github.com/react-native-oh-library/react-native-checkbox/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

    "@react-native-oh-tpl/checkbox": "file:../../node_modules/@react-native-oh-tpl/checkbox/harmony/checkbox.har",
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

### 3. Configuring CMakeLists and Introducing CheckboxPackge

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4.Introducing RNCCheckBoxPackage Component to ArkTS
> [!TIP] Required for version `v0.5.16-0.1.0` and above

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
+ import { RNCCheckBoxPackage } from '@react-native-oh-tpl/checkbox/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNCCheckBoxPackage(ctx)
  ];
}

### 5.Introducing Checkbox Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

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

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ CHECKBOX_TYPE
  ];
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/checkbox Releases](https://github.com/react-native-oh-library/react-native-checkbox/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!tip] `shape` is about to be deprecated, please use `boxType` instead 
> [!tip] `strokeWidth` is about to be deprecated, please use `lineWidth` instead


| Name                | Description                                                                                                                                                                                   | Type     | Required | Platform    | HarmonyOS Support |
|---------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------| -------- | -------- |-------------|------------------|
| `value`             | The value of the checkbox. If true the checkbox will be turned on. Default value is false.                                                                                                    | boolean  | No       | Android、iOS | yes              |
| `testID`            | Used to locate this view in end-to-end tests.                                                                                                                                                 | string   | No       | Android、iOS | yes              |
| `disabled`          | If true the user won't be able to toggle the checkbox. Default value is false.                                                                                                                | bool     | No       | Android、iOS | yes              |
| `onCheckColor`      | Color of the check box when it is selected.Defaults to '#007aff'                                                                                                                                                   | Color    | No       | iOS         | yes              |
| `tintColor`         | Border color of the check box when it is not selected. Defaults to '#aaaaaa'                                                                                                                                        | Color    | No       | iOS         | yes              |
| `shape` @deprecated             | Sets component shapes, including circles and rounded squares. Default value is 0.                                                                                                             | int      | No       | harmony     | yes              |
| `markSize`          | Size of the internal mark. The default size is the same as the width of the check box.This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used. | number   | No       | harmony     | yes              |
| `strokeWidth` @deprecated       | Stroke width of the internal mark. This parameter cannot be set in percentage. If it is set to an invalid value, the default value is used.                                                   | number   | No       | harmony     | yes              |
| `strokeColor`       | Color of the internal mark.Defaults to '#ffffff'                                                                                                                                                                   | Color    | No       | harmony     | yes              |
| `lineWidth`         | The width of the lines of the check mark and box. Defaults to 2.0.                                                                                                                            | number    | No       | iOS         | yes               |
| `hideBox`           | Control if the box should be hidden or not. Defaults to false.                                                                                                                                | boolean    | No       | iOS         | No              |
| `boxType`              | The type of box to use. Defaults to 'circle'      | 'circle' or 'square'      | No       | iOS     | yes              |
| `onFillColor`       | The color of the inside of the box when it is On. Defaults to transparent.                                                                                                                    | string      | No       | iOS      | No              |
| `onTintColor`       | The color of the line around the box when it is On. Defaults to '#007aff'.                                                                                                                    | string   | No       | iOS      | No              |
| `animationDuration` | The duration in seconds of the animations. Defaults to 0.5.                                                                                                                                   | number   | No       | iOS     | No              |
| `onAnimationType`   | The type of animation to use when the checkbox gets checked. Default to 'stroke'.                                                                                                             | 'stroke' or 'fill' or 'bounce' or 'flat' or 'one-stroke' or 'fade'   | No       | iOS     | No              |
| `offAnimationType`   | The type of animation to use when the checkbox gets unchecked. 'stroke'.                                                                                                                      | 'stroke' or 'fill' or 'bounce' or 'flat' or 'one-stroke' or 'fade'   | No       | iOS     | No              |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                                                                                                                                                                                    | Type     | Required | Platform      | HarmonyOS Support |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------- | ----------------- |
| `onChange`      | Invoked on change with the native event.                                                                                                                                                       | function | No       | Android、iOS   | yes               |
| `onValueChange` | Invoked with the new boolean value when it changes.                                                                                                                                            | function | No       | Android、iOS   | yes               |

## Known Issues

- [x] Set the lineWidth attribute, which is used to control the line width of the check box. It is not implemented in HarmonyOS. [issue#3](https://github.com/react-native-oh-library/react-native-checkbox/issues/3)
- [ ] Set the hideBox attribute, which is used to control the display and hiding of the check box. It is not implemented in HarmonyOS. [issue#4](https://github.com/react-native-oh-library/react-native-checkbox/issues/4)
- [ ] Set the onTintColor attribute, which is used to control the color of the border when the check box is selected. HarmonyOS is not implemented. [issue#5](https://github.com/react-native-oh-library/react-native-checkbox/issues/5)
- [ ] Set the onFillColor attribute, which is used to control the color inside the box when the check box is not selected. HarmonyOS is not implemented. [issue#9](https://github.com/react-native-oh-library/react-native-checkbox/issues/9)
- [ ] Set the animationDuration attribute, which is used to control the animation duration of selection and deselection. HarmonyOS is not implemented. [issue#6](https://github.com/react-native-oh-library/react-native-checkbox/issues/6)
- [ ] Set the onAnimationType attribute, which is used to control the animation type when selected. HarmonyOS is not implemented. [issue#7](https://github.com/react-native-oh-library/react-native-checkbox/issues/7)
- [ ] Set the offAnimationType attribute. This attribute is used to control the animation type when deselecting. It is not implemented in HarmonyOS. [issue#8](https://github.com/react-native-oh-library/react-native-checkbox/issues/8)

## Others

## License


This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-checkbox/blob/harmony/LICENSE).
