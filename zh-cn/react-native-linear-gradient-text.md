> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient-text </code> </h1>
</p>
<p align="center">
    <a href="https://github.com/HMDarkFir3/react-native-linear-gradient-text">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/HMDarkFir3/react-native-linear-gradient-text/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/HMDarkFir3/react-native-linear-gradient-text)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### npm

```bash
npm install react-native-linear-gradient-text@1.2.8
```

#### yarn

```bash
yarn add react-native-linear-gradient-text@1.2.8
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React from "react";
import { View, StyleSheet } from "react-native";
import { LinearGradientText } from "react-native-linear-gradient-text";

export const App = () => {
  return (
    <View style={styles.container}>
      <LinearGradientText
        colors={["#E76F00", "#EA374E"]}
        text="Hello World"
        start={{ x: 0.5, y: 0 }} // Optional
        end={{ x: 1, y: 1 }} // Optional
        textStyle={{ fontSize: 40 }} // Optional
        textProps={{ allowFontScaling: true }} // Optional
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
  },
});
```
## Link

本库 HarmonyOS 侧实现依赖 @react-native-oh-tpl/masked-view 和 @react-native-oh-tpl/react-native-linear-gradient 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/masked-view 文档的 Link 章节 ](/zh-cn/react-native-masked-view-masked-view.md#link) 和 [@react-native-oh-tpl/react-native-linear-gradient 文档的 Link 章节 ](/zh-cn/react-native-linear-gradient.md#link)进行引入。

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.21;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-linear-gradient-text ReadMe](https://github.com/HMDarkFir3/react-native-linear-gradient-text/tree/main)

### Props:

| Name      | Description                                                                                                   | **Type**                                                         | Platform | Required | HarmonyOS Support |
| --------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | -------- | -------- | ----------------- |
| text      | An string that display text. Example: `text="Hello World"`                                                    | string                                                           | All      | Y        | Yes               |
| colors    | An array of at least two color values that represent gradient colors. Example: `colors={["black", "white"]}`. | string[]                                                         | All      | Y        | Yes               |
| start     | An optional prop. He declare the position that the gradient starts. Example `start={{ x: 0.5, y: 0 }}`.       | { x: number, y: number }                                         | All      | N        | Yes               |
| end       | Same as start, but for the of the gradient.                                                                   | { x: number, y: number }                                         | All      | N        | Yes               |
| textStyle | A property to change all styles that a text has.                                                              | [TextStyle](https://reactnative.dev/docs/text-style-props)       | All      | N        | Yes               |
| textProps | A property to apply native props to text.                                                                     | [TextProps](https://reactnative.dev/docs/text-style-props#props) | All      | N        | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/HMDarkFir3/react-native-linear-gradient-text/blob/main/LICENSE) ，请自由地享受和参与开源。
