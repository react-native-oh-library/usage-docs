> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-theme-switch-animation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/WadhahEssam/react-native-theme-switch-animation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/WadhahEssam/react-native-theme-switch-animation/blob/main/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-theme-switch-animation)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-theme-switch-animation Releases](https://github.com/react-native-oh-library/react-native-theme-switch-animation/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-theme-switch-animation
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-theme-switch-animation
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import { StyleSheet, View, Button, Text } from "react-native";
import switchTheme from "react-native-theme-switch-animation";

export function ReactNativeThemeSwitchAnimationDemo() {
  const [theme, setTheme] = React.useState("light");

  return (
    <View
      style={{
        ...styles.container,
        backgroundColor: theme === "light" ? "white" : "black",
      }}
    >
      <View
        style={{
          borderWidth: 1,
          borderColor: theme === "light" ? "black" : "white",
          borderRadius: 1.4,
          padding: 50,
        }}
      >
        <Text
          style={{
            color: theme === "light" ? "black" : "white",
          }}
        >
          tests
        </Text>
      </View>

      <View style={{ marginTop: 10 }}>
        <Button
          title="start"
          onPress={() => {
            switchTheme({
              switchThemeFunction: () => {
                setTheme(theme === "light" ? "dark" : "light");
              },
              animationConfig: {
                type: "inverted-circular",
                duration: 2000,
                startingPoint: {
                  cxRatio: 0.5,
                  cyRatio: 0.5,
                },
              },
            });
          }}
        />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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

    "@react-native-oh-tpl/react-native-theme-switch-animation": "file:../../node_modules/@react-native-oh-tpl/react-native-theme-switch-animation/harmony/react_native_theme_switch.har"
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

### 3. Introducing RNThemeSwitch Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+ import { RNThemeSwitchPackage } from "@react-native-oh-tpl/react-native-theme-switch-animation/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNThemeSwitchPackage(ctx),
  ];
}

```

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Precautions

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-safe-area-context. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-safe-area-context](/en/react-native-safe-area-context.md) to add it to your project.

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-theme-switch-animation Releases](https://github.com/react-native-oh-library/react-native-theme-switch-animation/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**switchTheme Function Props**

| Prop                  | Description                                                                                                                   | Type            | Required | Platform | HarmonyOS Support |
| --------------------- | ----------------------------------------------------------------------------------------------------------------------------- | --------------- | -------- | -------- | ----------------- |
| `switchThemeFunction` | Adds the function you use in your app to switch themes, doesn't matter if you use redux/context/zustand/mobx or any other way | () => void      | no       | All      | yes               |
| `animationConfig`     | Configuration for the animation -> type, duration, starting point                                                             | AnimationConfig | no       | All      | yes               |

**animationConfig options**

| Prop            | Description                                                                            | Type                            | Required | Platform | HarmonyOS Support |
| --------------- | -------------------------------------------------------------------------------------- | ------------------------------- | -------- | -------- | ----------------- |
| `type`          | Specifies animation type                                                               | fade circular inverted-circular | no       | All      | yes               |
| `duration`      | Specifies duration in milliseconds                                                     | number                          | no       | All      | yes               |
| `startingPoint` | Configuration for the circular animation, where does the animation start in the screen | StartingPointConfig             | no       | All      | yes               |

**startingPoint options**

| Prop      | Description                                                                                                               | Type   | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| `cx`      | Specifies starting x point for circular and inverted-circular animation (should not exceed your screen width)             | number | no       | All      | yes               |
| `cy`      | Specifies starting y point for circular and inverted-circular animation (should not exceed your screen height)            | number | no       | All      | yes               |
| `cxRatio` | Specifies starting percentage of x point for circular and inverted-circular animation (should be number between -1 and 1) | number | no       | All      | yes               |
| `cyRatio` | Specifies starting percentage of y point for circular and inverted-circular animation (should be number between -1 and 1) | number | no       | All      | yes               |

## Known Issues

- [ ] circular 动画效果动画开始前有一个闪屏的问题，后续需要提供在图片上剪裁出一个圆形，透过圆形可以看到下方节点的接口或方法。[issue#6](https://github.com/react-native-oh-library/react-native-theme-switch-animation/issues/6)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/WadhahEssam/react-native-theme-switch-animation/blob/main/LICENSE).
