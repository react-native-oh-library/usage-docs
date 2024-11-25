> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/toolbar-android</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-toolbar-android/toolbar-android">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-toolbar-android/toolbar-android/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/toolbar-android/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/toolbar-android Releases](https://github.com/react-native-oh-library/toolbar-android/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/toolbar-android
```

#### yarn

```bash
yarn add @react-native-oh-tpl/toolbar-android
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { StyleSheet, View, Text } from "react-native";
import ToolbarAndroid from "@react-native-community/toolbar-android";
function App({}): JSX.Element {
  const [state, setState] = useState<{
    message?: string;
  }>({
    message: undefined,
  });

  const { message } = state;

  return (
    <View style={styles.container}>
      <ToolbarAndroid
        navIcon={require("./assets/ic_menu_black_24dp.png")}
        logo={require("./assets/icon_app.png")}
        title={"ToolbarAndroid Example"}
        subtitle={"ToolbarAndroid Subtitle"}
        titleColor={"#FFFFFF"}
        subtitleColor={"#FF00FF"}
        contentInsetStart={10}
        contentInsetEnd={10}
        rtl={false}
        style={styles.toolbar}
        actions={[
          {
            title: "Action1",
            icon: require("./assets/icon_phone.png"),
            show: "ifRoom",
            showWithText: true,
          },
        ]}
        overflowIcon={require("./assets/relay.png")}
        onIconClicked={() => setState({ message: "Clicked nav icon" })}
        onActionSelected={(position: number) =>
          setState({ message: `Clicked Menu-${position}` })
        }
      />
      <View style={styles.centerContainer}>
        <Text style={styles.headText}>
          Click nav or action icon will trigger some events!
        </Text>
        <Text style={styles.contentText}>{message}</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  toolbar: {
    backgroundColor: "#E9EAED",
    height: 56,
  },
  centerContainer: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#F5FCFF",
  },
  headText: {
    fontSize: 16,
  },
  contentText: {
    fontSize: 18,
    fontWeight: "bold",
    color: "#ff681f",
  },
});

export default App;
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
    "@react-native-oh-tpl/toolbar-android": "file:../../node_modules/@react-native-oh-tpl/toolbar-android/harmony/toolbar_android.har"
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

### 3. Configuring CMakeLists and Introducing ToolbarAndroidPackage

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

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/toolbar-android/src/main/cpp" ./toolbar-android)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_toolbar_android)
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
...
+ #include "ToolbarAndroidPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<ToolbarAndroidPackage>(ctx),
    };
}
```

### 4. Introducing RNCToolbarAndroid Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNCToolbarAndroid, RNC_TOOLBAR_ANDROID_TYPE } from '@react-native-oh-tpl/toolbar-android/src/main/ets/RNCToolbarAndroid'

  @Builder
  function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    ...
+   if (ctx.componentName === RNC_TOOLBAR_ANDROID_TYPE) {
+     RNCToolbarAndroid({
+      ctx: ctx.rnComponentContext,
+      tag: ctx.tag
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
  ...
+ RNC_TOOLBAR_ANDROID_TYPE
];
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/toolbar-android Releases](https://github.com/react-native-oh-library/toolbar-android/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

Inherits [View Props](https://reactnative.dev/docs/view#props).

| Name              | Description                                                                                                                                                                                     | Type                                                                                                          | Required | Platform | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| actions           | Sets possible actions on the toolbar as part of the action menu. These are displayed as icons or text on the right side of the widget. If they don't fit they are placed in an 'overflow' menu. | array of object: {title: string,icon: ImageSource,show: enum('always', 'ifRoom', 'never'),showWithText: bool} | No       | Android  | yes               |
| contentInsetStart | Sets the content inset for the toolbar starting edge.                                                                                                                                           | number                                                                                                        | No       | Android  | yes               |
| contentInsetEnd   | Sets the content inset for the toolbar ending edge.                                                                                                                                             | number                                                                                                        | No       | Android  | yes               |
| logo              | Sets the toolbar logo.                                                                                                                                                                          | ImageSource                                                                                                   | No       | Android  | yes               |
| navIcon           | Sets the navigation icon.                                                                                                                                                                       | ImageSource                                                                                                   | No       | Android  | yes               |
| onActionSelected  | Callback that is called when an action is selected. The only argument that is passed to the callback is the position of the action in the actions array.                                        | function                                                                                                      | No       | Android  | yes               |
| onIconClicked     | Callback called when the icon is selected.                                                                                                                                                      | function                                                                                                      | No       | Android  | yes               |
| overflowIcon      | Sets the overflow icon.                                                                                                                                                                         | ImageSource                                                                                                   | No       | Android  | yes               |
| rtl               | Used to set the toolbar direction to RTL.                                                                                                                                                       | bool                                                                                                          | No       | Android  | yes               |
| subtitle          | Sets the toolbar subtitle.                                                                                                                                                                      | string                                                                                                        | No       | Android  | yes               |
| subtitleColor     | Sets the toolbar subtitle color.                                                                                                                                                                | string                                                                                                        | No       | Android  | yes               |
| title             | Sets the toolbar title.                                                                                                                                                                         | string                                                                                                        | Yes      | Android  | yes               |
| titleColor        | Sets the toolbar title color.                                                                                                                                                                   | string                                                                                                        | No       | Android  | yes               |

#### Props of ImageSource

| Name   | Description                                            | Type   | Required | Platform | HarmonyOS Support |
| ------ | ------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| uri    | load image from a url, e.g. require('./some_icon.png') | string | Yes      | android  | yes               |
| width  | the width of the image                                 | number | No       | android  | yes               |
| height | the height of the image                                | number | No       | android  | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-toolbar-android/toolbar-android/blob/master/LICENSE).
