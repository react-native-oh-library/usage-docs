> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-config</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lugg/react-native-config">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lugg/react-native-config/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-config)

## Basic Usage

Create an `.env` file in the root directory of the React Native application.

```bash
API_URL=https://myapi.com
GOOGLE_MAPS_API_KEY=abcdefgh
```

Access the variables defined in the file from your application.

```bash
import Config from "react-native-config";

Config.API_URL; // 'https://myapi.com'
Config.GOOGLE_MAPS_API_KEY; // 'abcdefgh'
```

Note that this module does not obfuscate or encrypt secrets for packaging, so do not store sensitive keys in the `.env` file because it is basically impossible to [prevent users from reverse engineering of mobile application secrets](https://rammic.github.io/2015/07/28/hiding-secrets-in-android-apps/). Keep this in mind when designing applications (and APIs).

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-config Releases](https://github.com/react-native-oh-library/react-native-config/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



#### npm

```bash
npm install @react-native-oh-tpl/react-native-config
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-config
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```
import React, {Component} from 'react';
import {StyleSheet, Text, View} from 'react-native';

import Config from 'react-native-config';

export default class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>API_URL={Config.API_URL}</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  text: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
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

This library can be imported only in the form of source code.

#### Description of Direct Linking to Source Code

Currently, DevEco Studio does not support the introduction of external modules through source code. Perform the following steps to change the source code to an internal module of the **harmony** project.

> [!TIP] The source code is stored in the **harmony** directory in the installation path of the third-party library.

Copy the source code `<config>` in the `<RN project>/node_modules/@react-native-oh-tpl/react-native-config/harmony/` directory to the root directory of the `harmony` project.

In the root directory of the `harmony` project, add the following modules to `build-profile.template.json5` (if any) and `build-profile.json5`:

```json
modules:[
  ...
  {
    name: 'config',
    srcPath: './config',
  }
]
```

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-config": "file:../config"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

### 3. Introducing RNConfigPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import type { RNPackageContext, RNPackage } from 'rnoh/ts';
  ...
+ import { RNConfigPackage } from '@react-native-oh-tpl/react-native-config/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNConfigPackage(ctx)
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

### Multi-environment Configuration

Save the configurations of different environments in different files, such as `.env.staging` and `.env.production`.
By default, `react-native-config` is read from the `.env` file. The simplest way is to use an environment variable to specify the file to be read. It is not recommended to use `hvigor.js` in DevEco Studio to obtain the file.

Example:

Run the `cd harmony` command in the `CMD` window to enter the **harmony** directory from the the RN project root directory.

Stop all daemons.

```bash
"D:\DevEcoStudio\tools\node\node.exe" "D:\DevEcoStudio\tools\hvigor\bin\hvigorw.js" --stop-daemon-all
```

\*Note that the paths of `node.exe` and `hvigor.js` in the command are in the `tools` directory under the DevEco Studio installation directory. You can change them as required.

Set the environment variable `ENVFILE` to the name of the configuration file to be specified (do not add spaces after the file name), and use `hvigor.js` to build a project. For example:

```bash
set ENVFILE=.env.staging&&"D:\DevEcoStudio\tools\node\node.exe" "D:\DevEcoStudio\tools\hvigor\bin\hvigorw.js"  --mode module -p module=entry@default -p product=default -p requiredDeviceType=phone assembleHap --analyze=normal --parallel --increm
```

Then, open `DevEco Studio` to build and run the project. To ensure that the configured environment variables and the project are built in the same process, do not run the **hvigor** command in `DevEco Studio` to build the project.

#### Creating a Mapping

Alternatively, you can add the **buildProfileFields** field in `harmony` > `build-profile.json5` > `products` > `buildOption` > `arkOptions` to define a mapping to associate the build with the environment file. The field is configured in key-value pairs, where **key** indicates the project build type in lowercase and **value** indicates the name of the file to be read under the build type.

```json
"products": [
      {
        "name": "default",
        "signingConfig": "default",
        "compatibleSdkVersion": "5.0.0(12)",
        "runtimeOS": "HarmonyOS",
        "buildOption": {
          "arkOptions": {
            "buildProfileFields": {
              "debug": ".env.development",
              "release": ".env.production"
            }
          }
        }
      }
    ]
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-config Releases](https://github.com/react-native-oh-library/react-native-config/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                                   | Type   | Required | Platform    | HarmonyOS Support |
| ------ | --------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| Config | The property name and value in the class correspond to the key-value pair defined in the **.env** file.| Object | no       | Android/iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lugg/react-native-config/blob/master/LICENSE).
