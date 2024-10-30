> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-vconsole</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kafudev/react-native-vconsole">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kafudev/react-native-vconsole/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/kafudev/react-native-vconsole)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @kafudev/react-native-vconsole@0.1.11
```

#### **yarn**

```bash
yarn add @kafudev/react-native-vconsole@0.1.11
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js

import React from 'react';
import { StyleSheet, View } from 'react-native';
import Vconsole from '@kafudev/react-native-vconsole';

export const ConsoleDemo = () => {
    return (
        <View style={styles.container}>
            <PropsType />
        </View>
    );
};

function PropsType() {
    const appInfo = {
        Native build type: "1",
        Native version number: "ConfigReader.VERSION_NAME",
        Native build time: "ConfigReader.BUILD_TIME",
        Hot update version number: "codePushStore.info.label",
        Hot update details: "codePushStore.info.desc"
    }

    return (
        <View style={styles.container1}>
            <Vconsole appInfo={appInfo} console={true} showBtn={true} />
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        position: 'absolute',
        bottom: 180,
        width: '100%',
        height: 200,
        borderWidth: 1,
        button: 0
    },
    container1: {
        width: '100%',
        height: 200,
        borderWidth: 1,
        paddingVertical: 20,
        button: 0
    },
    box: {
        width: 60,
        height: 60,
    },
});
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK: HarmonyOS-Next-DB6 5.0.0.61; IDE: DevEco Studio 5.0.3.706; ROM: 3.0.0.65;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                              | Type    | Required | Platform | HarmonyOS Support |
| ------- | ---------------------------------------- | ------- | -------- | -------- | ----------------- |
| appInfo | Customized Version Info you want to show | json    | no       | All      | yes               |
| console | Whether to show console                  | boolean | no       | All      | yes               |
| showBtn | Whether to show buttons                  | boolean | no       | All      | yes               |
| panels  | Custom panels                            | json    | no       | All      | yes               |

## Known Issues

- [ ] 本库在 HarmonyOS 存在 Clipboard 无法使用的问题，其已从新版 rn 框架中移除，依赖 Clipboard 的相关功能，监控面板 network 标签页 Copy cURL to clipboard、Copy request query to clipboard、Copy response to clipboard 均无法正常复制以及粘贴，问题: [issue#2](https://github.com/kafudev/react-native-vconsole/issues/2)
- [ ] 本库在 HarmonyOS 存在 DevMenu 菜单无法启用的问题，新版本 rn 框架中已经将其从 NativeModules 移除，DevMenu 菜单里的 ReLoad、Fps 等调试相关功能均无法正常使用， 问题: [issue#3](https://github.com/kafudev/react-native-vconsole/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/kafudev/react-native-vconsole/blob/main/LICENSE) ，请自由地享受和参与开源
