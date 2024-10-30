> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-haptic-feedback</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/mkuczera/react-native-haptic-feedback">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mkuczera/react-native-haptic-feedback/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-haptic-feedback)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-haptic-feedback Releases](https://github.com/react-native-oh-library/react-native-haptic-feedback/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-haptic-feedback@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-haptic-feedback@file:#
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { SafeAreaView, ScrollView, Button } from "react-native";
import ReactNativeHapticFeedback from "react-native-haptic-feedback";
const options = {
  enableVibrateFallback: false,
  ignoreAndroidSystemSettings: false,
};

const methods = [
  "impactLight",
  "impactMedium",
  "impactHeavy",
  "notificationSuccess",
  "notificationWarning",
  "notificationError",
  "rigid",
  "soft",
  "selection",
  "clockTick",
  "contextClick",
  "keyboardPress",
  "keyboardRelease",
  "keyboardTap",
  "longPress",
  "textHandleMove",
  "virtualKey",
  "virtualKeyRelease",
  "effectClick",
  "effectDoubleClick",
  "effectHeavyClick",
  "effectTick",
];

export const HapticFeedbackExample = () => {
  return (
    <SafeAreaView>
      <ScrollView>
        {methods.map((item) => {
          return (
            <Button
              title={item}
              onPress={() => ReactNativeHapticFeedback.trigger(item, options)}
              key={item}
            ></Button>
          );
        })}
      </ScrollView>
    </SafeAreaView>
  );
};
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

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
    "@react-native-oh-tpl/react-native-haptic-feedback": "file:../../node_modules/@react-native-oh-tpl/react-native-haptic-feedback/harmony/haptic_feedback.har"

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

### 3. Introducing RNHapticFeedbackPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+  import { RNHapticFeedbackPackage } from '@react-native-oh-tpl/react-native-haptic-feedback/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNHapticFeedbackPackage(ctx)
  ]
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-haptic-feedback Releases](https://github.com/react-native-oh-library/react-native-haptic-feedback/releases)

### Permission Requirements

在 entry/src/main/module.json5 补上配置

```js
"requestPermissions": [ { "name": "ohos.permission.VIBRATE" }, ]
```

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Available Methods

`trigger(method, options)`
Use this method to trigger haptic feedback

| Name                                  | Description                                                                                                                           | Type    | Required | Platform    | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| `method`                              | Specifies the type of haptic feedback. See the list of available methods below.                                                       | string  | yes      | iOS/Android | yes               |
| `options.enableVibrateFallback`       | iOS only. If haptic feedback is unavailable (iOS < 10 OR Device < iPhone6s), vibrate with default method (heavy 1s) (default: false). | boolean | no       | iOS         | no                |
| `options.ignoreAndroidSystemSettings` | Ignoreing phone mute mode setting and triggering haptic feedback. (default: false).                                                   | boolean | no       | Android     | yes               |

### method Overview

Here's an overview of the available methods and their compatibility
| Name | Description | Type |Required|Platform|HarmonyOS Support|
| ---- | :-----: | :----: |:---: |:----: |:------: |
| `impactLight` | impactLight feedback | string |no|iOS/Android|yes|
| `impactMedium` | impactMedium feedback | string |no|iOS/Android|yes|
| `impactHeavy` | impactHeavy feedback | string |no|iOS/Android|yes|
| `rigid` | rigid feedback | string |no|iOS/Android|yes|
| `soft` | soft feedback | string |no|iOS/Android|yes|
| `notificationSuccess` | notificationSuccess feedback | string |no|iOS/Android|yes|
| `notificationWarning` | notificationWarning feedback | string |no|iOS/Android|yes|
| `notificationError` | notificationError feedback | string |no|iOS/Android|yes|
| `selection` | selection feedback | string |no|iOS|yes|
| `clockTick` | clockTick feedback | string |no|Android|yes|
| `contextClick` | contextClick feedback | string |no|Android|yes|
| `keyboardPress` | keyboardPress feedback | string |no|Android|yes|
| `keyboardRelease` | keyboardRelease feedback | string |no|Android|yes|
| `keyboardTap` | keyboardTap feedback | string |no|Android|yes|
| `longPress` | longPress feedback | string |no|Android|yes|
| `textHandleMove` | textHandleMove feedback | string |no|Android|yes|
| `virtualKey` | virtualKey feedback | string |no|Android|yes|
| `virtualKeyRelease` | virtualKeyRelease feedback | string |no|Android|yes|
| `effectClick` | effectClick feedback | string |no|Android|yes|
| `effectDoubleClick` | effectDoubleClick feedback | string |no|Android|yes|
| `effectHeavyClick` | effectHeavyClick feedback | string |no|Android|yes|
| `effectTick` | effectTick feedback | string |no|Android|yes|

## Known Issues

- [ ] 自定义振动文件配置问题: [issue#6](https://github.com/react-native-oh-library/react-native-haptic-feedback/issues/6)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mkuczera/react-native-haptic-feedback/blob/master/LICENSE).
