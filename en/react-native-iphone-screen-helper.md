模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-iphone-screen-helper</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/chlee1001/react-native-iphone-screen-helper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/chlee1001/react-native-iphone-screen-helper/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-iphone-screen-helper)


## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-iphone-screen-helper Releases](https://github.com/react-native-oh-library/react-native-iphone-screen-helper/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-iphone-screen-helper
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-iphone-screen-helper
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useEffect } from 'react';
import { getStatusBarHeight } from 'react-native-iphone-screen-helper'
import { View } from 'react-native';

const ScreenHelperDemo: React.FC = (): JSX.Element => {
    const [currentHeight, setCurrentHeight] = useState<number>(0)

    useEffect(() => {
        const barHeight = getStatusBarHeight()
        setCurrentHeight(barHeight)
    }, [])

    return (
        <>
            <View style={{ height: currentHeight, borderBottomWidth: 1 }} />
        </>
    )
}

export default ScreenHelperDemo;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-iphone-screen-helper Releases](https://github.com/react-native-oh-library/react-native-iphone-screen-helper/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| :---  | :---------- | ---- | -------- | ---- | ------------ |
| isIphoneX         | **returns** - `true` if you're running on an iPhone X or a newer model with a notch or dynamic island. | boolean | No       | All      | Yes               |
| isDynamicIsland | **returns** - `true` if you're running on an iPhone X or dynamic island. | boolean | No       | All      | Yes               |
| ifIphoneX | This method is for creating stylesheets with the iPhone X and later models, including those with dynamic islands, in mind. | stylesheets | No       | All      | Yes               |
| getStatusBarHeight | **returns** - the height of the status bar | number | No | All | Yes |
| getBottomSpace | **returns** - the height of the bottom to fit the safe area: `34` for iPhone X and newer models with a notch or dynamic island, and `0` for other devices. | number | No | All | Yes |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/chlee1001/react-native-iphone-screen-helper/blob/master/LICENSE) ，请自由地享受和参与开源。