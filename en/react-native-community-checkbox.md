> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/checkbox</code> </h1>
</p>

This project is based on [@react-native-community/checkbox](https://github.com/react-native-checkbox/react-native-checkbox).


This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is:`@react-native-ohos/checkbox`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 0.5.16-0.1.0@deprecated | @react-native-oh-tpl/checkbox | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-checkbox) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-checkbox/releases) |
| >= 0.5.17                   | @react-native-ohos/checkbox   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-checkbox) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-checkbox/releases) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/checkbox
```

#### **yarn**

```bash
yarn add @react-native-ohos/checkbox
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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1. Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2. Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/checkbox": "file:../../node_modules/@react-native-ohos/checkbox/harmony/checkbox.har",
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

### 2.3. Configuring CMakeLists and Introducing CheckboxPackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/checkbox/src/main/cpp" ./checkbox)
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

### 2.4. Introducing RNCCheckBoxPackage to ArkTS

> [!TIP] Required for version `v0.5.17` and above

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:

```diff
  ...
+ import { RNCCheckBoxPackage } from '@react-native-ohos/checkbox/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNCCheckBoxPackage(ctx)
  ];
}
```

### 2.5. Introducing RNCCheckbox Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
    ...
+ import { RNCCheckbox, CHECKBOX_TYPE } from "@react-native-ohos/checkbox"

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

### 2.6. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1. Compatibility

Check the release version information in the release address of the third-party library: [@react-native-ohos/checkbox Releases](https://gitee.com/openharmony-sig/rntpc_react-native-checkbox/releases)

## 4. Properties

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!TIP] `shape` is about to be deprecated, please use `boxType` instead 
> [!TIP] `strokeWidth` is about to be deprecated, please use `lineWidth` instead


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

## 5. Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                                                                                                                                                                                    | Type     | Required | Platform      | HarmonyOS Support |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------- | ----------------- |
| `onChange`      | Invoked on change with the native event.                                                                                                                                                       | function | No       | Android、iOS   | yes               |
| `onValueChange` | Invoked with the new boolean value when it changes.                                                                                                                                            | function | No       | Android、iOS   | yes               |

## 6. Known Issues

- [x] Set the lineWidth attribute, which is used to control the line width of the check box. It is not implemented in HarmonyOS. [issue#3](https://github.com/react-native-oh-library/react-native-checkbox/issues/3)
- [ ] Set the hideBox attribute, which is used to control the display and hiding of the check box. It is not implemented in HarmonyOS. [issue#4](https://github.com/react-native-oh-library/react-native-checkbox/issues/4)
- [ ] Set the onTintColor attribute, which is used to control the color of the border when the check box is selected. HarmonyOS is not implemented. [issue#5](https://github.com/react-native-oh-library/react-native-checkbox/issues/5)
- [ ] Set the onFillColor attribute, which is used to control the color inside the box when the check box is not selected. HarmonyOS is not implemented. [issue#9](https://github.com/react-native-oh-library/react-native-checkbox/issues/9)
- [ ] Set the animationDuration attribute, which is used to control the animation duration of selection and deselection. HarmonyOS is not implemented. [issue#6](https://github.com/react-native-oh-library/react-native-checkbox/issues/6)
- [ ] Set the onAnimationType attribute, which is used to control the animation type when selected. HarmonyOS is not implemented. [issue#7](https://github.com/react-native-oh-library/react-native-checkbox/issues/7)
- [ ] Set the offAnimationType attribute. This attribute is used to control the animation type when deselecting. It is not implemented in HarmonyOS. [issue#8](https://github.com/react-native-oh-library/react-native-checkbox/issues/8)

## 7. Others

## 8. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-checkbox/blob/master/LICENSE).
