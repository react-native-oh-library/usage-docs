> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-htmlview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jsdf/react-native-htmlview">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jsdf/react-native-htmlview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/jsdf/react-native-htmlview)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-htmlview@0.17.0
```

#### **yarn**

```bash
yarn add react-native-htmlview@0.17.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {StyleSheet, View, Linking} from 'react-native';
import HTMLView from 'react-native-htmlview';

const HtmlViewExample = () => {
  const htmlContent = `
      <h1>Hello, World!</h1>
      <p>This is a <a href="https://www.vmall.com">link</a></p>
      <p>Here is an image: <img src="https://res.vmallres.com/pimages/uomcdn/CN/pms/202404/displayProduct/10086102004921/428_428_a_mobileFF345C8650FF6E88771386A6433556D0.jpg" alt="Example Image" /></p>
  `;

  return (
    <View style={{...styles.container,backgroundColor:'white'}} >
      <HTMLView 
        value={htmlContent} 
        stylesheet={styles} // Optional: Pass custom styles for HTML elements
        onLinkPress={(url) => Linking.openURL(url)} // Optional: Handle link presses
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
    // Define custom styles for HTML elements
    a: {
      fontWeight: 'bold',
      color: 'blue',
      fontSize: 20,
      borderColor:'#000000',
      borderWidth:2
    },
    img: {
      width: 200,
      height: 100,
    },
});

export default HtmlViewExample;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!tip] 该库为UI组件库，可以在该库的标签下，使原本无法在RN框架生效的Html写法，可以实现对应的功能。

| Name            | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| value           | a string of HTML content to render                           | string | yes      | All      | yes               |
| onLinkPress     | a function which will be called with a url when a link is pressed. Passing this prop will override how links are handled | string | no       | All      | yes               |
| onLinkLongPress | a function which will be called with a url when a link is long pressed. The default is | string | no       | All      | yes               |
| stylesheet      | a stylesheet object keyed by tag name, which will override the styles applied to those respective tags. | string | no       | All      | yes               |
| renderNode      | a custom function to render HTML nodes however you see fit.  | string | no       | All      | yes               |
| bullet          | text which is rendered before every inside a `li``ul`        | string | no       | All      | yes               |
| paragraphBreak  | text which appears after every element`p`                    | string | no       | All      | yes               |
| lineBreak       | text which appears after text elements which create a new line | string | no       | All      | yes               |
| addLineBreaks   | when explicitly , effectively sets                           | string | no       | All      | yes               |

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/jsdf/react-native-htmlview/blob/master/LICENSE) ，请自由地享受和参与开源。
