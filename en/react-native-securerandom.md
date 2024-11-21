> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-securerandom</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/robhogan/react-native-securerandom">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/robhogan/react-native-securerandom/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-securerandom)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-securerandom Releases](https://github.com/react-native-oh-library/react-native-securerandom/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-securerandom
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-securerandom
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import {
  Text,
  TouchableOpacity,
  View,
  TextInput,
  StyleSheet,
} from "react-native";
import { generateSecureRandom } from "react-native-securerandom";

export default function secureRandomDemo(): JSX.Element {
  const [secureRandom, setSecureRandom] = useState("");
  const [size, setSize] = useState("30");

  return (
    <View>
      <ScrollView style={{ height: 60 }}>
        <Text>{secureRandom}</Text>
      </ScrollView>

      <TextInput
        style={styles.TextInput}
        value={size}
        onChangeText={(s) => {
          setSize(s);
        }}
      ></TextInput>
      <TouchableOpacity
        onPress={() => {
          generateSecureRandom(Number(size))
            .then((myRandom: any) => {
              setSecureRandom(`${JSON.stringify(myRandom?.data)}`);
            })
            .catch((err) => {
              console.log(err, "err");
            });
        }}
        style={styles.btn}
      >
        <Text style={styles.btnText}>secureRandom</Text>
      </TouchableOpacity>
    </View>
  );
}
const styles = StyleSheet.create({
  TextInput: {
    height: 40,
    borderColor: "#ccc",
    borderWidth: 1,
    borderRadius: 4,
    width: "90%",
  },
  btn: {
    borderRadius: 10,
    display: "flex",
    justifyContent: "center",
    alignItems: "center",
    padding: 10,
    margin: 10,
    backgroundColor: "blue",
  },
  btnText: { fontWeight: "bold", color: "#fff", fontSize: 20 },
});
```

### Use Codegen

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

### 2.  Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-securerandom": "file:../../node_modules/@react-native-oh-tpl/react-native-securerandom/harmony/secure_random.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing SecureRandomPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { SecureRandomPackage } from '@react-native-oh-tpl/react-native-securerandom/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SecureRandomPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-securerandom Releases](https://github.com/react-native-oh-library/react-native-securerandom/releases)

## API

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                 | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | ----------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| generateSecureRandom | A library to generate cryptographically-secure random byte. | Function | No       | ios/Android | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/robhogan/react-native-securerandom/blob/main/LICENSE).
