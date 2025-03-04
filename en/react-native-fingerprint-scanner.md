> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fingerprint-scanner</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hieuvp/react-native-fingerprint-scanner">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [GitHub address](https://github.com/react-native-oh-library/react-native-fingerprint-scanner)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-fingerprint-scanner Releases](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-fingerprint-scanner
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-fingerprint-scanner
```

<!-- tabs:end -->

Quick use:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { View, Button } from "react-native";
import FingerprintScanner from "react-native-fingerprint-scanner";

export default function App() {
  const handleClick = () => {
    FingerprintScanner.isSensorAvailable()
      .then((Biometrics) => {})
      .catch((err) => {});
  };
  const handleScanner = () => {
    FingerprintScanner.authenticate({ title: "1111" })
      .then(() => {})
      .catch((err) => {});
  };
  const handleAttempt = () => {
    let eror = FingerprintScanner.onAttempt();
  };
  const handleRelease = () => {
    FingerprintScanner.release();
  };
  return (
    <View>
      <Button title="authenticate" onPress={() => handleScanner()} />
      <Button title="isSensorAvailable" onPress={() => handleClick()} />
      <Button title="onAttempt" onPress={() => handleAttempt()} />
      <Button title="release" onPress={() => handleRelease()} />
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
    "@react-native-oh-tpl/react-native-fingerprint-scanner": "file:../../node_modules/@react-native-oh-tpl/react-native-fingerprint-scanner/harmony/fingerprint_scanner.har"
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

### 3. Introducing FingerprintScannerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import { RNFingerprintScannerPackage } from '@react-native-oh-tpl/react-native-fingerprint-scanner/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFingerprintScannerPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-fingerprint-scanner Releases](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/releases)

### Permission Requirements

> [!tip] The permission level of **ohos.permission.ACCESS_BIOMETRIC** is <B>system_basic</B>.
> Add the configuration to the `YourProject/entry/src/main/module.json5` file.

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.ACCESS_BIOMETRIC" },
    ]
  }
}
```

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                    | Description                                                  | Type     | Required | Platform  | HarmonyOS Support |
| ------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | --------- | ----------------- |
| `authenticate: (value: authenticate) => Promise<void>;` | Starts Fingerprint authentication                            | function | No       | All       | YES               |
| `isSensorAvailable: () => Promise<string>`              | Checks if Fingerprint Scanner is able to be used by now.     | function | No       | All       | YES               |
| `release: () => void`                                   | Stops fingerprint scanner listener, releases cache of internal state in native code | function | No       | All       | YES               |
| `onAttempt: () => {message?: string}`                   | when users are trying to scan their fingerprint but failed   | function | No       | HarmonyOS | YES               |

###### **Parameters of the authenticate API**

| Name              | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `title`           | the title text to display in the native                      | string   | no       | Android  | yes               |
| `subTitle`        | the sub title text to display in the native                  | string   | no       | Android  | no                |
| `description`     | the description text to display in the native                | string   | no       | All      | no                |
| `cancelButton`    | e cancel button text to display in the native                | string   | no       | Android  | no                |
| `onAttempt`       | a callback function when users are trying to scan their fingerprint but failed. | function | no       | Android  | no                |
| `fallbackEnabled` | default to true, whether to display fallback button          | boolean  | no       | IOS      | no                |

## Known Issues

- [ ] Only title can be modified for HarmonyOS fingerprint authentication. subTitle, description, cancelButton, fallbackEnabled are not supported: [issue#8](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/issues/8)
- [ ] The callback function onAttempt should be separated out and not passed as a parameter to the authenticate method because authenticate does not support parameters of the function type: [issue#7](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/issues/7)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://www.mit-license.org).
