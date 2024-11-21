> Template version: v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-get-random-values</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/LinusU/react-native-get-random-values">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/LinusU/react-native-get-random-values/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-get-random-values)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-get-random-values](https://github.com/react-native-oh-library/react-native-get-random-values/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-get-random-values
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-get-random-values
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { View, Text, StyleSheet, Button } from "react-native";
import "react-native-get-random-values";

export const GetRandomValues = () => {
  const [randomValue, setRandomValue] = useState < any > [];
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
      backgroundColor: "#F5FCFF",
    },
  });

  const clickBtn = () => {
    const getRandomValues = global?.crypto?.getRandomValues(new Uint8Array(4));
    console.log(JSON.stringify(getRandomValues), "click");

    const array = Object.values(getRandomValues);
    console.log(array, "click");

    setRandomValue(array);
  };
  return (
    <View style={styles.container}>
      <Text style={{ fontSize: 20 }}> click to get random number </Text>
      <Button onPress={clickBtn} title="click" />
      {randomValue?.map((item: any, index: number) => {
        return <Text key={index}>{item}</Text>;
      })}
    </View>
  );
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
    "@react-native-oh-tpl/react-native-get-random-values": "file:../../node_modules/@react-native-oh-tpl/react-native-get-random-values/harmony/get_random_values.har"
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

### 3. Introducing RNGetRandomValuesPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNGetRandomValuesPackage } from "@react-native-oh-tpl/react-native-get-random-values/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNGetRandomValuesPackage(ctx)
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

This document is verified based on the following versions:

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.
>
> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
>
> | Name                          | Description                                          | Type    | Required | Platform    | HarmonyOS Support |
> | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
> | global.crypto.getRandomValues | lets you get cryptographically strong random values. | funtion | no       | IOS/Android | yes               |

## License

This project is licensed under [The MIT License (MIT)](https://github.com/LinusU/react-native-get-random-values/blob/master/LICENSE).
