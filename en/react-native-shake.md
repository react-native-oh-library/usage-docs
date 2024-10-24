> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shake</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Doko-Demo-Doa/react-native-shake">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Doko-Demo-Doa/react-native-shake/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-shake)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-shake Releases](https://github.com/react-native-oh-library/react-native-shake/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-shake@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-shake@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { Text, View } from "react-native";
import RNShake from "react-native-shake";

export function ShakeExample() {
  const [result, setResult] = useState < string > "";
  myComponent(setResult);
  return (
    <View style={{ backgroundColor: "white", width: "100%" }}>
      <Text>shake your phone</Text>
      <Text>{result}</Text>
    </View>
  );
}

export const myComponent = (
  setResult: React.Dispatch<React.SetStateAction<string>>
) => {
  React.useEffect(() => {
    const subscription = RNShake.addListener(() => {
      setResult("shake listen success");
    });
    return () => {
      subscription.remove();
    };
  }, []);
};
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
    "@react-native-oh-tpl/react-native-shake": "file:../../node_modules/@react-native-oh-tpl/react-native-shake/harmony/shake_package.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).。

### 3. Introducing ShakePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import { ShakePackage } from "@react-native-oh-tpl/react-native-shake/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ShakePackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-shake Releases](https://github.com/react-native-oh-library/react-native-shake/releases)

### Permission Requirements

此库接口需要 normal 权限：ohos.permission.ACCESS_BLUETOOTH，权限需配置在 entry/src/main 目录下 module.json5 文件中

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCELEROMETER"
      }
    ]
```

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description               | Type     | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------- | -------- | -------- | ----------- | ----------------- |
| addListener        | add shake event listening | function | yes      | ios/andriod | yes               |
| removeAllListeners | remove event listening    | function | yes      | ios/andriod | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Doko-Demo-Doa/react-native-shake/blob/main/LICENSE).
