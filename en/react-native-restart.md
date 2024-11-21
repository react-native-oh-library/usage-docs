> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-restart</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/avishayil/react-native-restart">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/avishayil/react-native-restart/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-restart)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-restart Releases](https://github.com/react-native-oh-library/react-native-restart/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-restart
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-restart
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {Text, View, StyleSheet} from 'react-native';
import RNRestart from 'react-native-restart';

export default function RestartDemo() {
  return (
    <View>
      <Text>restart</Text>
      <Text style={styles.button} onPress={() => RNRestart.restart()}>
        restart
      </Text>
      <Text>Restart</Text>
      <Text style={styles.button} onPress={() => RNRestart.Restart()}>
        Restart
      </Text>
      <Text>The reason for the last restart(getReason)</Text>
      <Text style={styles.button} onPress={() => RNRestart.getReason()}>
        getReason
      </Text>
    </View>
  );
}

const styles = StyleSheet.create({
  button: {
    paddingVertical: 6,
    paddingHorizontal: 12,
    backgroundColor: 'hsl(193, 95%, 68%)',
    borderWidth: 2,
    borderColor: 'hsl(193, 95%, 30%)',
  },
});

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
   	"@react-native-oh-tpl/react-native-restart": "file:../../node_modules/@react-native-oh-tpl/react-native-restart/harmony/rn_restart.har",
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

### 3. Introducing RNRestartPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import type { RNPackageContext, RNPackage } from "rnoh/ts";
import { SamplePackage } from "rnoh-sample-package/ts";
+ import { RNRestartPackage } from '@react-native-oh-tpl/react-native-restart/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
      new SamplePackage(ctx), 
+     new RNRestartPackage(ctx)
  ];
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-restart Releases](https://github.com/react-native-oh-library/react-native-restart/releases)

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name      | Description                       | Type     | Required | Platform | HarmonyOS Support |
| --------- | --------------------------------- | -------- | -------- | -------- | ----------------- |
| restart   | restart your react native project | Function | no       | All      | yes               |
| Restart   | restart your react native project | Function | no       | All      | yes               |
| getReason | get the cause of the last restart | Function | no       | All      | yes               |
## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/avishayil/react-native-restart/blob/master/LICENSE)，请自由地享受和参与开源。