> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-snackbar</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cooperka/react-native-snackbar">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cooperka/react-native-snackbar/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-snackbar)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-snackbar Releases](https://github.com/react-native-oh-library/react-native-snackbar/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-snackbar@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-snackbar@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, StyleSheet, Button, ScrollView } from "react-native";
import Snackbar from "react-native-snackbar";

export const SnackbarTest = () => {
  return (
    <View
      style={{
        width: "100%",
        height: "100%",
        backgroundColor: "white",
        flex: 1,
      }}
    >
      <ScrollView style={styles.container}>
        <Button
          title="click to display components"
          onPress={() => {
            Snackbar.show({
              text: "Hello harmony",
              marginBottom: 300,
            });
          }}
        />
      </ScrollView>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    width: "100%",
    backgroundColor: "#333",
    flex: 1,
  },
  Snackbar: {
    width: "100%",
    backgroundColor: "white",
  },
});
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-oh-tpl/react-native-snackbar": "file:../../node_modules/@react-native-oh-tpl/react-native-snackbar/harmony/snackbar.har"
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

### 3. Introducing RNSnackbarPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...
+ import {RNSnackbarPackage} from '@react-native-oh-tpl/react-native-snackbar/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSnackbarPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-snackbar Releases](https://github.com/react-native-oh-library/react-native-snackbar/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Snackbar.show(options)

| Name              | Description                                                                                                     | Type                       | Required | Platform    | HarmonyOS Support |
| ----------------- | --------------------------------------------------------------------------------------------------------------- | -------------------------- | -------- | ----------- | ----------------- |
| `text`            | The message to show.                                                                                            | `string`                   | yes      | Android iOS | yes               |
| `duration`        | How long to display the Snackbar                                                                                | See below                  | no       | Android iOS | no                |
| `numberOfLines`   | The max number of text lines to allow before ellipsizing                                                        | `number`                   | no       | Android iOS | no                |
| `marginBottom`    | Margin from bottom                                                                                              | `number`                   | no       | Android iOS | yes               |
| `textColor`       | The color of the message text.                                                                                  | `string` or `style`        | no       | Android iOS | no                |
| `backgroundColor` | The background color for the whole Snackbar                                                                     | `string` or `style`        | no       | Android iOS | no                |
| `fontFamily`      | [Android only] The basename of a .ttf font from assets/fonts/                                                   | `string`                   | no       | Android     | no                |
| `rtl`             | [Android only, API 17+] Whether the Snackbar should render right-to-left (requires android:supportsRtl="true"). | `boolean`                  | no       | Android     | no                |
| `action`          | Optional config for the action button (described below)                                                         | `object` (described below) | no       | Android iOS | no                |

Where `duration` can be one of the following (timing may vary based on device):

- `Snackbar.LENGTH_SHORT` (just over a second)
- `Snackbar.LENGTH_LONG` (about three seconds)
- `Snackbar.LENGTH_INDEFINITE` (stays on screen until dismissed, replaced, or action button is tapped)

The optional `action` object can contain the following options:

| Key         | Type                      | Description                                   | Platform    | HarmonyOS Support |
| ----------- | ------------------------- | --------------------------------------------- | ----------- | ----------------- |
| `text`      | `string` The button text. | The button text.                              | Android iOS | no                |
| `textColor` | `string` or `style`       | The color of the button text.                 | Android iOS | no                |
| `onPress`   | `function`                | A callback for when the user taps the button. | Android iOS | no                |

### Snackbar events

You can have information on snackbar visibility.

```js
  componentDidMount() {
    const SnackbarEventEmitter = new NativeEventEmitter(
      NativeModules.RNSnackbar,
    );
    this.eventListener = SnackbarEventEmitter.addListener('onSnackbarVisibility', (event) => {
      console.log(event.event);
    });
  }

  componentWillUnmount() {
    this.eventListener.remove();
  }
```

Or, with functional components:

```js
useEffect(() => {
  const subscription = new NativeEventEmitter(
    NativeModules.RNSnackbar
  ).addListener("onSnackbarVisibility", (event) => {
    console.log(event.event);
  });
  return () => {
    subscription.remove();
  };
}, []);
```

Where event is one of the following options :

| Key                                  | Type     | Value | Description                                                                | Platform    | HarmonyOS Support |
| ------------------------------------ | -------- | ----- | -------------------------------------------------------------------------- | ----------- | ----------------- |
| `Snackbar.DISMISS_EVENT_SWIPE`       | `number` | 0     | Indicates that the Snackbar was dismissed via a swipe.                     | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_ACTION`      | `number` | 1     | Indicates that the Snackbar was dismissed via an action click.             | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_TIMEOUT`     | `number` | 2     | Indicates that the Snackbar was dismissed via a timeout.                   | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_MANUAL`      | `number` | 3     | Indicates that the Snackbar was dismissed via Snackbar.dismiss() call.     | Android iOS | no                |
| `Snackbar.DISMISS_EVENT_CONSECUTIVE` | `number` | 4     | Indicates that the Snackbar was dismissed from a new Snackbar being shown. | Android iOS | no                |
| `Snackbar.SHOW_EVENT`                | `number` | 5     | Indicates that Snackbar appears                                            | Android iOS | no                |

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                       | Type     | Required | Platform    | HarmonyOS Support |
| ------- | --------------------------------- | -------- | -------- | ----------- | ----------------- |
| show    | Shows a Snackbar                  | function | yes      | Android iOS | yes               |
| dismiss | Dismisses any existing Snackbars. | function | yes      | Android iOS | no                |

### show()

| Name    | Description | Type   | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------ | -------- | ----------- | ----------------- |
| options | options     | object | yes      | Android iOS | partially         |

## Known Issues

- [ ] 不支持 duration、numberOfLines、textColor、backgroundColor、fontFamily、rtl、action 等参数以及 dismiss()接口: [issue#1](https://github.com/react-native-oh-library/react-native-snackbar/issues/1)
- [ ] 与 Android 和 iOS 的样式有一定的差异: [issue#2](https://github.com/react-native-oh-library/react-native-snackbar/issues/2)
- [ ] 无法实现 Snackbar events：[issue#3](https://github.com/react-native-oh-library/react-native-snackbar/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/cooperka/react-native-snackbar/blob/main/LICENSE).
