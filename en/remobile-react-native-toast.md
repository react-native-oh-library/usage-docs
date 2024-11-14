> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@remobile/react-native-toast</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/remobile/react-native-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/remobile/react-native-toast/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-toast)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-toast Releases](https://github.com/react-native-oh-library/react-native-toast/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-toast
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-toast
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, {Component} from 'react';
import {Text, View, Button} from 'react-native';
import Toast from '@remobile/react-native-toast';

function ToastMasterDemo() {
    return (
        <View style={{flex: 2, justifyContent: 'center', alignItems: 'center'}}>
            <Text>Tosat !</Text>
            <Button
                title={'show toast'}
                onPress={() => {
                    Toast.show('This is a toast.');
                }}
            />
            <Button
                title={'short top toast'}
                onPress={() => {
                    Toast.showShortTop('This is a top toast.');
                }}
            />
            <Button
                title={'short center toast'}
                onPress={() => {
                    Toast.showShortCenter('This is a center toast.');
                }}
            />
            <Button
                title={'short bottom toast'}
                onPress={() => {
                    Toast.showShortBottom('This is a bottom toast.');
                }}
            />
            <Button
                title={'long top toast'}
                onPress={() => {
                    Toast.showLongTop('This is a long top toast.');
                }}
            />
            <Button
                title={'long center toast'}
                onPress={() => {
                    Toast.showLongCenter('This is a long center toast.');
                }}
            />
            <Button
                title={'long bottom toast'}
                onPress={() => {
                    Toast.showLongBottom('This is a long bottom toast.');
                }}
            />
        </View>
    );
}

export default ToastMasterDemo;

```

## Use Codegen

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
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
"@react-native-oh-tpl/react-native-toast": "file:../../node_modules/@react-native-oh-tpl/react-native-toast/harmony/rn_toast.har"
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

### 3. Introducing  ToastPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ToastPackage} from '@react-native-oh-tpl/react-native-toast/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ToastPackage(ctx)
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

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-toast Releases](https://github.com/react-native-oh-library/react-native-toast/releases)


## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show()  | Displays the location of the toast, its duration, the content of the message | function  | yes | android      | yes |
| showShortTop()  | Display the top Toast for a short time | function  | yes | android      | yes |
| showShortCenter()  | Display the center Toast for a short time | function  | yes | android      | yes |
| showShortBottom()  | Display the bottom Toast for a short time | function  | yes | android      | yes |
| showLongTop()  | Display the top Toast for a long time | function  | yes | android      | yes |
| showLongCenter()  | Display the center Toast for a long time | function  | yes | android      | yes |
| showLongBottom()  | Display the bottom Toast for a long time | function  | yes | android      | yes |
| hide()  | Hide the toast that is being displayed         | function  | yes | android      | no |

## Known Issues

- [ ] Does not support hide() function to hide toast:[issue#3](https://github.com/react-native-oh-library/react-native-toast/issues/3)

## Others

## License

This project is licensed under [The MIT License](https://github.com/remobile/react-native-toast/blob/master/LICENSE).
