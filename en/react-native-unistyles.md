> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-unistyles</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jpudysz/react-native-unistyles">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jpudysz/react-native-unistyles/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-unistyles)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-unistyles Releases](https://github.com/react-native-oh-library/react-native-unistyles/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-unistyles
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-unistyles
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {
  StatusBar,
  StyleSheet,
  Text,
  View,
  Button,
  ScrollView,
  PixelRatio,
} from "react-native";
import {
  UnistylesRuntime,
  createStyleSheet,
  useStyles,
  UnistylesRegistry,
  mq,
  UnistylesPlugin,
} from "react-native-unistyles";
import React, { useEffect } from "react";
const basic_styles = StyleSheet.create({
  consta: { backgroundColor: "#F5FCFF" },
  titleStyle: { fontSize: 16, fontWeight: "500" },
});

export function UnistylesExample() {
  let anti_shake = true;
  const hasSomeCoolFeatures = true;
  const { styles, theme } = useStyles(stylesheet, {
    colors: hasSomeCoolFeatures,
    sizes: !hasSomeCoolFeatures,
  });
  let status_color = true;
  const renderCount = React.useRef(1);
  useEffect(
    () => () => {
      UnistylesRuntime.removePlugin(autoGuidelinePlugin);
    },
    []
  );
  const isAutoGuidelinePluginEnabled = UnistylesRuntime.enabledPlugins.includes(
    autoGuidelinePlugin.name
  );

  return (
    <ScrollView>
      <View style={basic_styles.consta}>
        <StatusBar barStyle="light-content"></StatusBar>
        <Text style={basic_styles.titleStyle}>
          {"Change the color of the status bar:"}
        </Text>
        <Button
          title="status"
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              UnistylesRuntime.statusBar.setColor(
                status_color ? sharedColors.barbie : sharedColors.aloes
              );
              status_color = !status_color;
            }
          }}
        ></Button>

        <Text style={basic_styles.titleStyle}>
          {"Change the theme object:"}
        </Text>
        <View style={styles.container}>
          <Text style={styles.text}>
            {" "}
            Current topic:{UnistylesRuntime.themeName} The number of times to re
            render:{renderCount.current++}
          </Text>
          <Text style={styles.theme}>
            {" "}
            Colors: {JSON.stringify(theme.colors, null, 2)}{" "}
          </Text>
          <Button
            title="Change the light theme"
            onPress={() => {
              anti_shake = !anti_shake;
              if (anti_shake) {
                UnistylesRuntime.setAdaptiveThemes(false);
                UnistylesRuntime.setTheme("light");
                UnistylesRuntime.updateTheme("light", (theme) => ({
                  ...theme,
                  colors: {
                    ...theme.colors,
                    typography:
                      theme.colors.typography === "#000000"
                        ? theme.colors.blood
                        : "#000000",
                  },
                }));
              }
            }}
          />
        </View>

        <Text style={basic_styles.titleStyle}>{"Change page style:"}</Text>
        <Text style={styles.text}>
          {" "}
          This page is currently in use {UnistylesRuntime.themeName} .
        </Text>
        <Button
          title="Change page theme"
          color={theme.colors.accent}
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              UnistylesRuntime.setAdaptiveThemes(false);
              UnistylesRuntime.setTheme(
                UnistylesRuntime.themeName === "light" ? "premium" : "light"
              );
            }
          }}
        />

        <Text style={basic_styles.titleStyle}>{"Adaptive Theme:"}</Text>
        <Text style={styles.container}>
          {" System Theme:" + UnistylesRuntime.colorScheme}
        </Text>
        <Button
          title="Enable adaptive themes"
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              UnistylesRuntime.setAdaptiveThemes(true);
            }
          }}
        />

        <Text style={basic_styles.titleStyle}>{"plug-in unit:"}</Text>
        <View style={styles.unscaledBox}></View>
        <Text>
          Styles with the prefix unscaled will be skipped by the plugin, while
          plugins that have already been enabled will be skipped
          {UnistylesRuntime.enabledPlugins}
        </Text>
        <Button
          title={
            isAutoGuidelinePluginEnabled ? "Close plugin" : "Enable plugins"
          }
          onPress={() => {
            anti_shake = !anti_shake;
            if (anti_shake) {
              isAutoGuidelinePluginEnabled
                ? UnistylesRuntime.removePlugin(autoGuidelinePlugin)
                : UnistylesRuntime.addPlugin(autoGuidelinePlugin);
            }
          }}
        />

        <Text style={basic_styles.titleStyle}>
          {"Using runtime in StyleSheets:"}
        </Text>
        <View style={styles.box}>
          <Text>
            The width of the square occupying half the size of the screen:
            {styles.box.width} 861 height:
            {styles.box.height}
          </Text>
        </View>

        <Text style={basic_styles.titleStyle}>
          {"Dynamic functional style sheet:"}
        </Text>
        <View style={styles.dynamicFunction(2)}>
          <Text>accent</Text>
        </View>
        <View style={styles.dynamicFunction(1)}>
          <Text>barbie</Text>
        </View>

        <Text style={basic_styles.titleStyle}>{"Media inquiry:"}</Text>
        <View style={styles.container1}>
          <Text>
            What is the size of your screen:{UnistylesRuntime.screen.width}x
            {UnistylesRuntime.screen.height};When the width is greater than 500,
            the background is
            {theme.colors.backgroundColor}，When the width is greater than 900, the
            background is
            {theme.colors.aloes}
          </Text>
        </View>

        <Text style={basic_styles.titleStyle}>
          {"Using variables in StyleSheets:"}
        </Text>
        <View style={styles.box_variants}></View>
        <Text style={basic_styles.titleStyle}>{":"}</Text>

        <Text style={basic_styles.titleStyle}>{"Font size preference:"}</Text>
        <Text>
          {"The current font size preference is set to:" +
            UnistylesRuntime.contentSizeCategory}
        </Text>
      </View>
    </ScrollView>
  );
}

const stylesheet = createStyleSheet((theme, runtime) => ({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    paddingHorizontal: 20,
    backgroundColor: theme.colors.backgroundColor,
    rowGap: 20,
  },
  text: {
    textAlign: "center",
    color: theme.colors.typography,
    fontSize: 14,
  },
  bold: {
    fontWeight: "bold",
  },
  container1: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    paddingHorizontal: 20,
    backgroundColor: {
      [mq.width(undefined, 500).and.height(undefined, 1000)]:
        theme.colors.backgroundColor,
      [mq.only.width(932)]: theme.colors.aloes,
    },
    rowGap: 20,
  },
  theme: {
    color: theme.colors.typography,
  },
  box: {
    justifyContent: "center",
    alignItems: "center",
    padding: 20,
    marginTop: 50,
    width: runtime.screen.width / 2,
    height: runtime.screen.height / 2,
    backgroundColor:
      runtime.orientation === "portrait"
        ? theme.colors.accent
        : theme.colors.oak,
  },
  dynamicFunction: (index: number) => ({
    backgroundColor:
      index % 2 === 0 ? theme.colors.accent : theme.colors.barbie,
  }),
  box_variants: {
    borderRadius: 10,
    variants: {
      colors: {
        true: { backgroundColor: theme.colors.barbie },
        false: { backgroundColor: theme.colors.blood },
        default: { backgroundColor: theme.colors.sky },
        other: { backgroundColor: theme.colors.typography },
      },
      sizes: {
        true: { width: 200, height: 200 },
        false: { width: 50, height: 50 },
        default: { width: 100, height: 100 },
        other: { width: 150, height: 150 },
      },
    },
  },
  unscaledBox: { width: 100, height: 100, backgroundColor: theme.colors.blood },
}));

const sharedColors = {
  barbie: "#ff9ff3",
  oak: "#1dd1a1",
  sky: "#48dbfb",
  fog: "#c8d6e5",
  aloes: "#00d2d3",
  blood: "#ff6b6b",
};
const lightTheme = {
  colors: {
    ...sharedColors,
    backgroundColor: "#ffffff",
    typography: "#000000",
    accent: sharedColors.blood,
  },
};
const darkTheme = {
  colors: {
    ...sharedColors,
    backgroundColor: "#000000",
    typography: "#ffffff",
    accent: sharedColors.barbie,
  },
};
const premiumTheme = {
  colors: {
    ...sharedColors,
    backgroundColor: sharedColors.barbie,
    typography: "#76278f",
    accent: "#000000",
  },
};
const breakpoints = { xs: 0, sm: 300, md: 500, lg: 800, xl: 1200 };
UnistylesRegistry.addThemes({
  light: lightTheme,
  dark: darkTheme,
  premium: premiumTheme,
})
  .addBreakpoints(breakpoints)
  .addConfig({ adaptiveThemes: true, initialTheme: "light" });

const REFERENCE_WIDTH = 300;
const REFERENCE_HEIGHT = 800;

const autoGuidelinePlugin: UnistylesPlugin = {
  name: "autoGuideline",
  onParsedStyle: (styleKey, style, runtime) => {
    const pairs = Object.entries(style).map(([key, value]) => {
      if (styleKey.includes("unscaled")) {
        return [key, value];
      }

      const isNumber = typeof value === "number";

      if (!isNumber || key === "flex") {
        return [key, value];
      }

      if (key === "height") {
        const percentage = value / REFERENCE_HEIGHT;
        return [
          key,
          PixelRatio.roundToNearestPixel(runtime.screen.height * percentage),
        ];
      }
      const percentage = value / REFERENCE_WIDTH;
      return [
        key,
        PixelRatio.roundToNearestPixel(runtime.screen.width * percentage),
      ];
    });

    return Object.fromEntries(pairs);
  },
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
    "@react-native-oh-tpl/react-native-unistyles": "file:../../node_modules/@react-native-oh-tpl/react-native-unistyles/harmony/unistyles.har"
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

### 3. Configuring CMakeLists and Introducing UnistylesPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-unistyles/src/main/cpp" ./unistyles)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_unistyles)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "UnistylesPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<UnistylesPackage>(ctx),
    };
}
```

### 4. Introducing RNUnistylesPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNUnistylesPackage} from '@react-native-oh-tpl/react-native-unistyles/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNUnistylesPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-unistyles Releases](https://github.com/react-native-oh-library/react-native-unistyles/releases)

## Runtime

### UnistylesRuntime

UnistylesRuntime 是 Unitstyles 库 的一个 Host Object。它始终保持最新状态，并允许您与 Unistyles 的原生层进行交互

#### UnistylesRuntime 属性

| Name                 | Description                                                                  | Type                 | Required | Platform | HarmonyOS Support |
| -------------------- | ---------------------------------------------------------------------------- | -------------------- | -------- | -------- | ----------------- |
| screenWidth          | Screen dimensions Width                                                      | number               | no       | All      | yes               |
| screenHeight         | Screen dimensions Height                                                     | number               | no       | All      | yes               |
| enabledPlugins       | Names of currently enabled plugins                                           | boolean              | no       | All      | yes               |
| hasAdaptiveThemes    | Indicates if you have enabled adaptive themes                                | boolean              | no       | All      | yes               |
| themeName            | Name of the selected theme or an empty string if you don’t use themes        | string               | no       | All      | yes               |
| breakpoint           | Current breakpoint or always undefined if you don’t use breakpoints          | UnistylesBreakpoints | no       | All      | yes               |
| colorScheme          | Get your device’s color scheme. Available options dark, light or unspecified | string               | no       | All      | yes               |
| contentSizeCategory  | Your device’s content size category                                          | string               | no       | All      | yes               |
| insets               | Device insets which are safe to put content into                             | inset                | no       | All      | yes               |
| statusBar.width      | Status bar dimensions width                                                  | number               | no       | All      | yes               |
| statusBar.height     | Status bar dimensions height                                                 | number               | no       | All      | yes               |
| navigationBar.height | Navigation bar dimensions height                                             | number               | no       | Android  | yes               |
| navigationBar.width  | Navigation bar dimensions width                                              | number               | no       | Android  | yes               |
| ScreenOrientation    | Your device’s orientation                                                    | ScreenOrientation    | no       | All      | yes               |

目前 UnistylesRuntime 支持:

- `statusBar.setColor`
  Update statusBar color at runtime

- `navigationBar.setColor`
  Update navigationBar color at runtime

- `setAdaptiveThemes`
  Toggle adaptive themes

- `setTheme`
  Change the current theme

- `updateTheme`
  Update the theme at runtime

- `removePlugin`
  Disable a plugin

- `addPlugin`
  Enable a plugin

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### global

| Name             | Description                                                                  | Type     | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useInitialTheme  | using multiple themes and need to determine the initial theme during runtime | function | no       | All      | yes               |
| useStyles        | set current styles                                                           | function | no       | All      | yes               |
| createStyleSheet | create unistyles StyleSheet                                                  | function | no       | All      | yes               |

#### mq

| Name   | Description                   | Type     | Required | Platform | HarmonyOS Support |
| ------ | ----------------------------- | -------- | -------- | -------- | ----------------- |
| width  | width from xx onwards         | function | no       | All      | yes               |
| height | heigh from xx onwards         | function | no       | All      | yes               |
| and    | and                           | function | no       | All      | yes               |
| only   | width or height from xx to xx | function | no       | All      | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### UnistylesRegistry

| Name           | Description          | Type     | Required | Platform | HarmonyOS Support |
| -------------- | -------------------- | -------- | -------- | -------- | ----------------- |
| addThemes      | register themes      | function | no       | All      | yes               |
| addBreakpoints | register breakpoints | function | no       | All      | yes               |
| addConfig      | register config      | function | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jpudysz/react-native-unistyles/blob/main/LICENSE).
