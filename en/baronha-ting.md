> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@baronha/ting</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/<原库源码仓地址>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/baronha/ting/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/ting)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/ting Releases](https://github.com/react-native-oh-library/ting/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/ting
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/ting
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { View } from "react-native";
import {
    ToastOptions,
    toast
} from '@baronha/ting';

function handleToast(options: ToastOptions) {
    toast(options);
}

const App = () => {
  return (
    <View>
        <Button
            title="defalut"
            onPress={() => {
                const options: ToastOptions = {
                    title: 'title-Toast',
                    message: 'message-Toast',
                };
                handleToast(options);
            }}
        />
    </View>
};

export default App;
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
    "@react-native-oh-tpl/ting": "file:../../node_modules/@react-native-oh-tpl/ting/harmony/ting.har"
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

### 3. Introducing RNTingPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNTingPackage} from '@react-native-oh-tpl/ting';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTingPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/ting Releases](https://github.com/react-native-oh-library/ting/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### ToastOptions

| Name                | Description                                                                                                                    | Type    | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| title               | The text for the toast’s title                                                                                                 | string  | no       | All      | yes               |
| message             | The text for the toast’s message                                                                                               | string  | no       | All      | yes               |
| titleColor          | The color of the title text in hexadecimal format                                                                              | string  | no       | All      | yes               |
| messageColor        | The color of the message text in hexadecimal format                                                                            | string  | no       | All      | yes               |
| preset              | The preset style of the toast. Options include done (success), error (error), none (no style), or spinner (loading spinner)    | string  | no       | All      | partially         |
| duration            | The lifetime of the toast (seconds)                                                                                            | number  | no       | All      | yes               |
| haptic              | The type of haptic feedback. Options include success (success), warning (warning), error (error), or none (no haptic feedback) | string  | no       | iOS      | yes               |
| shouldDismissByDrag | Whether the toast can be dismissed by dragging                                                                                 | boolean | no       | All      | yes               |
| position            | Toast is displayed from top or bottom                                                                                          | string  | no       | All      | yes               |
| backgroundColor     | The background color of the toast in hexadecimal format                                                                        | string  | no       | All      | yes               |
| icon                | A custom icon for the toast                                                                                                    | object  | no       | All      | yes               |
| progressColor       | The color of the progress spinner for the spinner preset style                                                                 | string  | no       | Android  | yes               |

### AlertOptions

| Name               | Description                                                                                                                    | Type    | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------------------------------------------------------------------------------------------------------------------ | ------- | -------- | -------- | ----------------- |
| title              | The text for the toast’s title                                                                                                 | string  | no       | All      | yes               |
| message            | The text for the toast’s message                                                                                               | string  | no       | All      | yes               |
| titleColor         | The color of the title text in hexadecimal format                                                                              | string  | no       | All      | yes               |
| messageColor       | The color of the message text in hexadecimal format                                                                            | string  | no       | All      | yes               |
| preset             | The preset style of the toast. Options include done (success), error (error), none (no style), or spinner (loading spinner)    | string  | no       | All      | partially         |
| duration           | The lifetime of the toast (seconds)                                                                                            | number  | no       | All      | yes               |
| haptic             | The type of haptic feedback. Options include success (success), warning (warning), error (error), or none (no haptic feedback) | string  | no       | iOS      | yes               |
| shouldDismissByTap | Whether the toast can be dismissed by tapping                                                                                  | boolean | no       | All      | yes               |
| backgroundColor    | The background color of the toast in hexadecimal format                                                                        | string  | no       | All      | yes               |
| borderRadius       | The border radius of the toast box, which determines how rounded the corners are                                               | number  | no       | All      | yes               |
| blurBackdrop       | The intensity of the background blur effect on Android platforms                                                               | number  | no       | Android  | no                |
| backdropOpacity    | The opacity of the background blur effect on Android platforms, with a range from 0 (fully transparent) to 1 (fully opaque)    | number  | no       | All      | yes               |
| icon               | A custom icon for the toast                                                                                                    | object  | no       | All      | yes               |
| progressColor      | The color of the progress spinner for the spinner preset style                                                                 | string  | no       | Android  | yes               |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name         | Description                                    | Type     | Required | Platform | HarmonyOS Support |
| ------------ | ---------------------------------------------- | -------- | -------- | -------- | ----------------- |
| toast        | Displays a Toast notification                  | function | yes      | All      | yes               |
| alert        | Displays an Alert dialog                       | function | yes      | All      | yes               |
| dismissAlert | Closes the currently displayed Alert dialog    | function | yes      | All      | yes               |
| setup        | Configures global settings for Toast and Alert | function | yes      | All      | yes               |

## Known Issues

- [ ] AlertOptions 和 ToastOptions 中的 preset：done，动画效果未实现。[issue#3](https://github.com/react-native-oh-library/ting/issues/3)

## Others

- AlertOptions 中的 blurBackdrop 参数配置后，iOS 不支持，Android 无效果。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/baronha/ting/blob/main/LICENSE).
