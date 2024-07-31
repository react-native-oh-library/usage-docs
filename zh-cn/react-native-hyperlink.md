模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-hyperlink</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/obipawan/react-native-hyperlink">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/obipawan/react-native-hyperlink/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/obipawan/react-native-hyperlink)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-hyperlink@0.0.22
```

#### **yarn**

```bash
yarn add react-native-hyperlink@0.0.22
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text } from "react-native";
import Hyperlink from "react-native-hyperlink";

export default function App() {
  return (
    <Hyperlink
      linkDefault
      injectViewProps={(url) => ({
        testID: url === "http://link.com" ? "id1" : "id2",
        style:
          url === "https://link.com" ? { color: "red" } : { color: "blue" },
        //any other props you wish to pass to the component
      })}
    >
      <Text>
        You can pass props to clickable components matched by url.
        <Text>This url looks red https://link.com</Text> and this url looks blue
        https://link2.com{" "}
      </Text>
    </Hyperlink>
  );
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                                                                       | Type                     | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------- | ------------------------ | -------- | -------- | ----------------- |
| linkify         | linkify-it object, for custom schema                                              | object                   | no       | all      | yes               |
| linkStyle       | highlight clickable text with styles                                              | object                   | no       | all      | yes               |
| linkText        | A string or a func to replace parsed text                                         | string   &#124; function | no       | all      | yes               |
| onPress         | Func to handle click over a clickable text with parsed text as arg                | function                 | no       | all      | yes               |
| onLongPress     | Func to handle long click over a clickable text with parsed text as arg           | function                 | no       | all      | yes               |
| linkDefault     | A platform specific fallback to handle onPress. Uses Linking. Disabled by default | boolean                  | no       | all      | yes               |
| injectViewProps | Func with url as a param to inject props to the clickable component               | function                 | no       | all      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/obipawan/react-native-hyperlink/blob/master/LICENSE) ，请自由地享受和参与开源。