> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-touch-id</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/naoufal/react-native-touch-id">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-touch-id)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-touch-id Releases](https://github.com/react-native-oh-library/react-native-touch-id/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.


Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-touch-id
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-touch-id
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component, useState } from 'react';
import { Alert, View, Button, Text } from 'react-native';
import TouchID from 'react-native-touch-id';

const App = () => {
  const [result, setResult] = useState<string>('')
  return (
     <View>
      <Text style={{ height: 40, backgroundColor: 'white', textAlign: 'center' }}>{result}</Text>
      <Button title='check whether you have fingerprint permission'
        onPress={() => {
          TouchID.isSupported({ unifiedErrors: false }).then((res: any) => {
            setResult(res)
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
      <Button title='check fingerprint'
        onPress={() => {
          TouchID.authenticate().then((res: boolean) => {
            setResult('Authentication successful')
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
    </View>
  )
};

export default App;

```
## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Open `entry/oh-package.json5` file and add the following dependencies:

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
    "@react-native-oh-tpl/react-native-touch-id": "file:../../node_modules/@react-native-oh-tpl/react-native-touch-id/harmony/touch_id.har"
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


### 3. Introducing TouchIdPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { TouchIdPackage } from "@react-native-oh-tpl/react-native-touch-id/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new TouchIdPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-touch-id Releases](https://github.com/react-native-oh-library/react-native-touch-id/releases)


### Permission Requirements

(Enter the related permission configuration.)

Add the following permissions to their respective files:

In your `module.json5`

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCESS_BIOMETRIC"
      }
    ]
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isSupported  | Whether touchid is supported | function  | yes | ios/andriod      | yes |
| authenticate  | Verify touchid | function  | yes | ios/andriod      | yes |
## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Errors

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Touch ID Error  | Permission verification failed | string  | no | harmonry      | yes |
| Touch ID Error  | Incorrect parameters | string  | no | harmonry      | yes |
| Touch ID Error  | Authentication failed  | string  | no | harmonry  | yes |
| Touch ID Error  | The operation is canceled   | string  | no | harmonry  | yes |
| Touch ID Error  | The operation is time-out | string  | no | harmonry  | yes |
| Touch ID Error  | The authentication type is not supported   | string | no | harmonry  | yes |
| Touch ID Error  | The authentication trust level is not supported | string  | no | harmonry      | yes |
| Touch ID Error  | The authentication task is busy | string  | no | harmonry      | yes |
| Touch ID Error  | The authenticator is locked  | string  | no | harmonry  | yes |
| Touch ID Error  | General operation error   | string  | no | harmonry  | no |
| Touch ID Error  | The authentication type is not supported | string  | no | harmonry  | yes |
| Touch ID Error  | The type of credential has not been enrolled   | string | no | harmonry  | yes |
| Touch ID Error  | The authentication is canceled from widget's navigation button   | string | no | harmonry  | yes |
| Touch ID Error  | Indicates that current authentication failed because of PIN expired   | string | no | harmonry  | yes |
## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license).
