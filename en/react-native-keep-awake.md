> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-keep-awake</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/corbt/react-native-keep-awake">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/corbt/react-native-keep-awake/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-keep-awake)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-keep-awake Releases](https://github.com/react-native-oh-library/react-native-keep-awake/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keep-awake
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keep-awake
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from "react";
import { Text, Button } from "react-native";

import KeepAwake, {
  activateKeepAwake,
  deactivateKeepAwake,
  useKeepAwake,
} from "react-native-keep-awake";

export function KeepAwakeExample() {
  useKeepAwake();

  const handleClick = (buttonId: number) => {
    switch (buttonId) {
      case 1:
        deactivateKeepAwake();
        break;
      case 2:
        activateKeepAwake();
        break;
      case 3:
        deactivateKeepAwake();
        break;
      case 4:
        KeepAwake.activate();
        break;
      case 5:
        KeepAwake.deactivate();
        break;
      default:
        break;
    }
  };

  return (
    <>
      <Text style={{ color: "blue" }}>
        Button 1: Hook default method enabled (always
        on),----useKeepAwake(),Click button 1 to turn off the constant light
      </Text>
      <Button title="Button 1" onPress={() => handleClick(1)}></Button>

      <Text style={{ color: "blue" }}>
        Button 2: Enable functions method----activateKeepAwake()
      </Text>
      <Button title="Button 2" onPress={() => handleClick(2)}></Button>

      <Text style={{ color: "blue" }}>
        Button 3: Close the function method----deactivateKeepAwake()
      </Text>
      <Button title="Button 3" onPress={() => handleClick(3)}></Button>

      <Text style={{ color: "blue" }}>
        Button 4: Old interface method----KeepAwake.activate()
      </Text>
      <Button title="Button 4" onPress={() => handleClick(4)}></Button>

      <Text style={{ color: "blue" }}>
        Button 5: Old interface method----KeepAwake.deactivate()
      </Text>
      <Button title="Button 5" onPress={() => handleClick(5)}></Button>
    </>
  );
}
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

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
    "@react-native-oh-tpl/react-native-keep-awake": "file:../../node_modules/@react-native-oh-tpl/react-native-keep-awake/harmony/keep_awake.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-keep-awake": "file:../../node_modules/@react-native-oh-tpl/react-native-keep-awake/harmony/keep_awake"
  }
```

run the following instruction on the terminal:

```bash
cd entry
ohpm install --no-link
```

### 3. Introducing RNKeepAwakePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNKeepAwakePackage } from "@react-native-oh-tpl/react-native-keep-awake/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNKeepAwakePackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-keep-awake Releases](https://github.com/react-native-oh-library/react-native-keep-awake/releases)

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18、HarmonyOS NEXT Developer Preview0 B.0.60、HarmonyOS NEXT Developer Preview2 B.0.73; IDE: DevEco Studio 5.0.3.200; ROM: 2.0.0.18;

## 使用方法

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] 功能函数形式使用下，新老接口均可使用。

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                   | Description                                    | Required | Platform | HarmonyOS Support |
| ---------------------- | ---------------------------------------------- | -------- | -------- | ----------------- |
| `<KeepAwake/>`         | 组件形式使用，开启当前屏幕常亮模式             | No       | All      | yes               |
| KeepAwake.activate()   | 功能函数形式使用，开启当前屏幕常亮模式(老接口) | No       | All      | yes               |
| KeepAwake.deactivate() | 功能函数形式使用，开启当前屏幕常亮模式(老接口) | No       | All      | yes               |
| useKeepAwake()         | hooks 形式使用                                 | No       | All      | yes               |
| activateKeepAwake()    | 功能函数形式使用，开启当前屏幕常亮模式(新接口) | No       | All      | yes               |
| deactivateKeepAwake()  | 功能函数形式使用，关闭当前屏幕常亮模式(新接口) | No       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/corbt/react-native-keep-awake/blob/master/LICENCE).
