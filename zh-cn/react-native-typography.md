> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-typography</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hectahertz/react-native-typography">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hectahertz/react-native-typography/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-typography)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-typography Releases](https://github.com/react-native-oh-library/react-native-typography/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-typography
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-typography
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变

```js
import { View, Text } from "react-native";
import React from "react";
import { iOSUIKit, material, systemWeights } from "react-native-typography";

export function TypographyExample1() {
  return (
    <View style={{ backgroundColor: "white" }}>
      <Text style={iOSUIKit.largeTitleEmphasized}>Hello iOS UI Kit!</Text>
      <Text style={material.title}>Title</Text>
      <Text style={systemWeights.light}>Title</Text>
    </View>
  );
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-typography Releases](https://github.com/react-native-oh-library/react-native-typography/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                                                                                                                                                                                                                                                                                                                  | Type   | Required | Platform | HarmonyOS Support |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| material            | Includes all the styles defined in the [Material Design Guidelines](https://material.io/guidelines/style/typography.html#typography-styles).Defines size, weight and color.                                                                                                                                                                                                  | object | no       | All      | yes               |
| materialDense       | material`s Dense scripts                                                                                                                                                                                                                                                                                                                                                     | object | no       | All      | yes               |
| materialTall        | material`s Tall scripts                                                                                                                                                                                                                                                                                                                                                      | object | no       | All      | yes               |
| human               | Defined in the [Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/visual-design/typography/).Defines size, weight and color.                                                                                                                                                                                                            | object | no       | All      | yes               |
| humanDense          | human`s Dense scripts                                                                                                                                                                                                                                                                                                                                                        | object | no       | All      | yes               |
| humanTall           | human`s Tall scripts                                                                                                                                                                                                                                                                                                                                                         | object | no       | All      | yes               |
| iOSUIKit            | Extracted from [the official Apple sketch file](https://developer.apple.com/design/resources/) These are the text styles that fall under the category of iOS UIKit, and are used to build the UI components of iOS Apps. They build on top of the Human Interface styles, customizing some properties such as weight or letter spacing.                                      | object | no       | iOS      | yes               |
| iOSUIKitDense       | iOSUIKit`s Dense scripts                                                                                                                                                                                                                                                                                                                                                     | object | no       | iOS      | yes               |
| iOSUIKitTall        | iOSUIKit`s Tall scripts                                                                                                                                                                                                                                                                                                                                                      | object | no       | iOS      | yes               |
| systemWeights       | A font weight in React Native is sometimes formed by a pair of a fontFamily and a fontWeight, but not always! It depends on the typeface, sometimes it's just. defined by the fontFamily. With these helpers, you don't have to worry about those inconsistencies. To combine them with a collection style (or your own styles) just spread them, as they are plain objects. | object | no       | All      | yes               |
| systemDenseWeights  | systemWeights`s Dense scripts                                                                                                                                                                                                                                                                                                                                                | object | no       | All      | yes               |
| systemTallWeights   | systemWeights`s Tall scripts                                                                                                                                                                                                                                                                                                                                                 | object | no       | All      | yes               |
| sanFranciscoWeights | San Francisco typeface                                                                                                                                                                                                                                                                                                                                                       | object | no       | iOS      | yes               |
| robotoWeights       | These weights are **only intended for Android**, as they directly reference the native Roboto typeface.                                                                                                                                                                                                                                                                      | object | no       | Android      | yes               |
| webWeights          | These weights are **only intended for the web**, and render [react-native-web](https://github.com/necolas/react-native-web)'s system font stack.                                                                                                                                                                                                                             | object | no       | Web      | yes               |
| iOSColors           | Colors iOS                                                                                                                                                                                                                                                                                                                                                                   | object | no       | iOS      | yes               |
| materialColors      | Colors Material                                                                                                                                                                                                                                                                                                                                                              | object | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hectahertz/react-native-typography/blob/master/LICENSE) ，请自由地享受和参与开源。
