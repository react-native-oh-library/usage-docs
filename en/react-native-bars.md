> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bars</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/zoontek/react-native-bars">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-bars/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-bars)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-bars Releases](https://github.com/react-native-oh-library/react-native-bars/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-bars@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-bars@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import * as React from "react";
import { Switch, Text, View } from "react-native";
import { StatusBar } from "react-native-bars";

export function BarExample() {
  const [isEnabled, setIsEnabled] = React.useState(false);
  const toggleSwitch = () => setIsEnabled((previousState) => !previousState);

  return (
    <View>
      <StatusBar barStyle={isEnabled ? "light-content" : "dark-content"} />
      <Text style={{ color: "white" }}>close dark-content/ open light-content</Text>
      <Switch
        trackColor={{ false: "#767577", true: "#81b0ff" }}
        thumbColor={isEnabled ? "#f5dd4b" : "#f4f3f4"}
        ios_backgroundColor="#3e3e3e"
        onValueChange={toggleSwitch}
        value={isEnabled}
      />
    </View>
  );
}
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
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@react-native-oh-tpl/react-native-bars": "file:../../node_modules/@react-native-oh-tpl/react-native-bars/harmony/bars.har"

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

### 3. Introducing RNBarsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNBarsPackage} from '@react-native-oh-tpl/react-native-bars/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBarsPackage(ctx)
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

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-bars Releases](https://github.com/react-native-oh-library/react-native-bars/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### StatusBar

| Name     | Description                                                                                   | Type    | Required | Platform | HarmonyOS Support |
| -------- | --------------------------------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| barStyle | Status Bar Style                                                                              | string  | yes      | all      | yes               |
| animated | Should transition between status bar property changes be animated? (has no effect on Android) | boolean | no       | all      | yes               |

### NavigationBar

| Name     | Description          | Type   | Required | Platform | HarmonyOS Support |
| -------- | -------------------- | ------ | -------- | -------- | ----------------- |
| barStyle | Navigation Bar Style | string | yes      | all      | no                |

### SystemBar

| Name     | Description                                                                                   | Type    | Required | Platform | HarmonyOS Support |
| -------- | --------------------------------------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| barStyle | System Style                                                                                  | string  | yes      | all      | no                |
| animated | Should transition between status bar property changes be animated? (has no effect on Android) | boolean | no       | all      | no                |

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### StatusBar

| Name              | Description                            | Type                                                                     | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------- | ------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| pushStackEntry    | Add an instance to the heap queue      | StatusBar.pushStackEntry(props)                                          | no       | all      | yes               |
| popStackEntry     | Delete an instance from the heap queue | StatusBar.popStackEntry(entry/_: StatusBarProps_/): void;                | no       | all      | yes               |
| replaceStackEntry | Replace an instance of the heap queue  | const entry: StatusBarProps = StatusBar.replaceStackEntry(entry ,props ) | no       | all      | yes               |

### NavigationBar

| Name              | Description                            | Type                                                                             | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------- | -------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| pushStackEntry    | Add an instance to the heap queue      | NavigationBar.pushStackEntry(props)                                              | no       | all      | no                |
| popStackEntry     | Delete an instance from the heap queue | NavigationBar.popStackEntry(entry/_: NavigationBarProps_/): void;                | no       | all      | no                |
| replaceStackEntry | Replace an instance of the heap queue  | const entry: NavigationBarProps = NavigationBar.replaceStackEntry(entry ,props ) | no       | all      | no                |

## Known Issues

- [ ] react-native-bars 不支持 NavigationBar 问题: [issue#16](https://github.com/react-native-oh-library/react-native-bars/issues/16)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/zoontek/react-native-bars/blob/main/LICENSE).

