> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-randombytes</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mvayngrib/react-native-randombytes">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mvayngrib/react-native-randombytes/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-randombytes)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-library/react-native-randombytes Releases](https://github.com/react-native-oh-library/react-native-randombytes/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-randombytes
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-randombytes
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```tsx

import React, { useState } from "react";
import { Text, TouchableOpacity, View, TextInput, StyleSheet } from 'react-native';
import { randomBytes } from 'react-native-randombytes';

export default function randomBytesDemo(): JSX.Element {

    const [bytesString, setBytesString] = useState('');
    const [size, setSize] = useState('30');

    const nativeRandom = () => {
        randomBytes(Number(size), (err: any, bytes: any) => {
            setBytesString(JSON.stringify(bytes))
            console.log(err);       
        })
    }

    const jsRandom = () => {
        const bytes = randomBytes(Number(size))
        setBytesString(JSON.stringify(bytes))
    }

    return <View>
        <Text>
            {bytesString}
        </Text>

        <TextInput style={styles.TextInput} value={size} onChangeText={(s) => {
            setSize(s);
        }}></TextInput>
        <TouchableOpacity onPress={nativeRandom} style={styles.btn}>
        <Text
          style={styles.btnText}>
          Native RandomBytes
        </Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={jsRandom} style={styles.btn}>
        <Text
          style={styles.btnText}>
          RandomBytes
        </Text>
      </TouchableOpacity>
    </View>
}

const styles = StyleSheet.create({
  TextInput: { height: 40, borderColor: '#ccc', borderWidth: 1, borderRadius: 4, width: '90%' },
  btn: { borderRadius: 10, display: 'flex', justifyContent: 'center', alignItems: 'center', padding: 10, margin: 10, backgroundColor: 'blue' },
  btnText: { fontWeight: 'bold', color: '#fff', fontSize: 20 }
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
    "@react-native-oh-tpl/react-native-randombytes": "file:../../node_modules/@react-native-oh-tpl/react-native-randombytes/harmony/random_bytes.har"
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

### 3. Introducing RandomBytesPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RandomBytesPackage } from '@react-native-oh-tpl/react-native-randombytes/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RandomBytesPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-randombytes Releases](https://github.com/react-native-oh-library/react-native-randombytes/releases)

This document is verified based on the following versions:
1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-randombytes](https://github.com/react-native-oh-library/react-native-randombytes)

| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| randombytes    | generate secure random numbers. | function | No       | IOS/Android | yes               |
| seedSJCL       | Add entropy to the pools.       | function | No       | IOS/Android | yes               |


## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mvayngrib/react-native-randombytes/blob/master/LICENSE).

