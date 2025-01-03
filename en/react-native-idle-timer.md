> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-idle-timer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/marcshilling/react-native-idle-timer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/marcshilling/react-native-idle-timer/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-idle-timer)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package:[@react-native-oh-tpl/react-native-idle-timer Releases](https://github.com/react-native-oh-library/react-native-idle-timer/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-idle-timer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-idle-timer@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useEffect } from 'react';
import { View, Text, Button } from 'react-native';
import IdleTimerManager from 'react-native-idle-timer';

const IdleTimerExample = () => {  
  useEffect(() => {
    // Disable the idle timer to prevent the screen from dimming or locking.
    IdleTimerManager.setIdleTimerDisabled(true, "video");

    // A cleanup function to re-enable the idle timer when the component is unmounted
    return () => {
     IdleTimerManager.setIdleTimerDisabled(false, "video");
    };
  }, []);
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <Text>By default, the screen will remain on</Text>
    </View>
  );
};

export default IdleTimerExample;
```

## Use Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-idle-timer": "file:../../node_modules/@react-native-oh-tpl/react-native-idle-timer/harmony/idle_timer.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md)


### 3.Introducing RNIdleTimerPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNIdleTimerPackage}  from '@react-native-oh-tpl/react-native-idle-timer/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNIdleTimerPackage(ctx)
  ];
}
```

### 4.Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-idle-timer Releases](https://github.com/react-native-oh-library/react-native-idle-timer/releases)

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                        | Type     | Required | Platform | HarmonyOS Support |
| -------------------- | ---------------------------------- | -------- | -------- | -------- | ----------------- |
| setIdleTimerDisabled | enable/forbidden screen idle timer | function | no       | All      | yes               |

## Known Issues

## Others 

## License

This project is licensed under [The MIT License (MIT)](https://github.com/marcshilling/react-native-idle-timer/blob/master/LICENSE.md).
