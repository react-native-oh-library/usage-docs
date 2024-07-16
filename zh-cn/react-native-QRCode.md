> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qrcode</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cssivision/react-native-qrcode">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cssivision/react-native-qrcode/blob/master/LICENSE">
       <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-qrcode)

## 安装与使用

1、请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-qrcode](https://github.com/react-native-oh-library/react-native-qrcode/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-qrcode@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-qrcode@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import QRCode from "react-native-qrcode";
import { StyleSheet, View, TextInput, Button } from "react-native";
export const QrCodeExamle = () => {
  const [text, setText] = useState("");
  const [QRCodeValue, setQRCodeValue] = useState < any > null;
  const showQRCode = () => {
    setQRCodeValue(text);
  };
  const reset = () => {
    setQRCodeValue(null);
    setText("");
  };
  return (
    <View style={styles.container}>
      <TextInput
        placeholder="请输入要生成二维码的文本"
        style={styles.input}
        onChangeText={(text) => setText(text)}
        value={text}
      />
      <View style={{ flexDirection: "row" }}>
        <Button title="点击生成二维码" onPress={showQRCode} />
        <Button title="重置" onPress={reset} />
      </View>

      {QRCodeValue && (
        <QRCode
          value={QRCodeValue}
          size={200}
          bgColor="black"
          fgColor="white"
        />
      )}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: "white",
    alignItems: "center",
  },

  input: {
    width: 300,
    height: 40,
    borderColor: "gray",
    borderWidth: 1,
    margin: 10,
    borderRadius: 5,
    padding: 5,
  },
});
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档](/zh-cn/react-native-webview.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-qrcode](https://github.com/react-native-oh-library/react-native-qrcode/releases)

## 属性

### QRCode

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
 
> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

该库为 UI 组件库，通过配置属性标签，实现对应的功能。

| Name    | Type   | Description                 | Required | Platform    | HarmonyOS Support |
| ------- | ------ | --------------------------- | -------- | ----------- | ----------------- |
| value   | string | What the qrcode stands for. | no       | iOS/Android | yes               |
| size    | number | qrcode size                 | no       | iOS/Android | yes               |
| bgColor | string | backgroundColor             | no       | iOS/Android | yes               |
| fgColor | string | fgColor                     | no       | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-qrcode/blob/master/LICENSE) ，请自由地享受和参与开源。
