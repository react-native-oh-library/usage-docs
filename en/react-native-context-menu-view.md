> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-context-menu-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mpiannucci/react-native-context-menu-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mpiannucci/react-native-context-menu-view/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-context-menu-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-context-menu-view Releases](https://github.com/react-native-oh-library/react-native-context-menu-view/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-context-menu-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-context-menu-view@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import ContextMenu from "react-native-context-menu-view";

const Example = () => {
  return (
    <ContextMenu
      actions={[{ title: "Title 1" }, { title: "Title 2" }]}
      onPress={(e) => {
        console.warn(
          `Pressed ${e.nativeEvent.name} at index ${e.nativeEvent.index}`
        );
      }}
    >
      <View style={styles.yourOwnStyles} />
    </ContextMenu>
  );
};
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
    "@react-native-oh-tpl/react-native-context-menu-view": "file:../../node_modules/@react-native-oh-tpl/react-native-context-menu-view/harmony/context_menu.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Configuring CMakeLists and Introducing ContextMenuPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-context-menu-view/src/main/cpp" ./context_menu)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_context_menu)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ContextMenuPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ContextMenuPackage>(ctx),
    };
}
```

### 4. Introducing ContextMenuPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ContextMenuPackage} from '@react-native-oh-tpl/react-native-context-menu-view/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ContextMenuPackage(ctx)
  ];
}
```

### 5. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-context-menu-view Releases](https://github.com/react-native-oh-library/react-native-context-menu-view/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                                                                | Type     | Required | Platform               | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------ | -------- | -------- | ---------------------- | ----------------- |
| title                  | The title above the popup menu.                                                            | string   | no       | Android/iOS            | yes               |
| actions                | Menu props.                                                                                | array    | no       | Android(partially)/iOS | partially         |
| previewBackgroundColor | The background color of the preview.                                                       | string   | no       | NA                     | no                |
| dropdownMenuMode       | When set to true, the context menu is triggered with a single tap instead of a long press. | boolean  | no       | Android/iOS            | yes               |
| disabled               | Disable menu interaction.                                                                  | boolean  | no       | Android/iOS            | yes               |
| onPress                | When the popup is opened and the user picks an option.                                     | callback | no       | Android/iOS            | yes               |
| onPreviewPress         | When the context menu preview is tapped.                                                   | callback | no       | iOS                    | yes               |
| onCancel               | When the popup is opened and the user cancels.                                             | callback | no       | Android/iOS            | yes               |

## actions

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name           | Description                                                                                                                    | Type    | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| title          | the title of the action                                                                                                        | string  | no       | Android/iOS | yes               |
| subtitle       | the subtitle of the action                                                                                                     | string  | no       | iOS 15+     | yes               |
| systemIcon     | refers to an icon name within [SF Symbols](https://developer.apple.com/design/human-interface-guidelines/sf-symbols/overview/) | string  | no       | iOS         | yes               |
| icon           | Custom Icons.                                                                                                                  | string  | no       | Android/iOS | yes               |
| iconColor      | will change the color of the icon provided to the `icon` prop and has no effect on `systemIcon` (default: black)               | string  | no       | Android/iOS | yes               |
| destructive    | items are rendered in red                                                                                                      | boolean | no       | iOS         | yes               |
| selected       | items have a checkmark next to them                                                                                            | boolean | no       | iOS         | yes               |
| disabled       | marks whether the action is disabled or not                                                                                    | boolean | no       | Android/iOS | yes               |
| inlineChildren | marks whether its children (if any) should be rendered inline instead of in their own child menu                               | boolean | no       | iOS         | partially         |
| actions        | will provide a one level deep nested menu                                                                                      | array   | no       | Android/iOS | partially         |

## Known Issues

## Others

1.previewBackgroundColor 属性，经过验证在 iOS 和 Android 均无效果。

2.actions 属性是个结构体函数，所以包含其他上文列举属性，例如 previewBackgroundColor 等。所以，属于部分支持

3.该库的具体逻辑实现，在不同平台，均为调用平台对应的底层 Menu 接口进行相关操作。所以，不同平台上，动效展示等会有所不同。

4.onPress 方法的 callback 参考: { nativeEvent: { index, indexPath, name } }.

5.当 systemIcon 和 icon 同时配置的时候，在 Harmony Next 平台上，systemIcon 的优先级高于 icon

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mpiannucci/react-native-context-menu-view/blob/main/LICENSE).
