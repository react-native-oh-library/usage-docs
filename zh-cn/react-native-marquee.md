> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-marquee</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-marquee">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-marquee/blob/sig/LICENSE/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-marquee)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/react-native-marquee> Releases](https://github.com/react-native-oh-library/react-native-marquee/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-marquee@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-marquee@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { Component } from "react";
import { StyleSheet, View } from "react-native";
import MarqueeText from "react-native-marquee";

export default class MarqueeTextSample extends Component {
  render() {
    return (
      <View style={styles.container}>
        <MarqueeText
          style={{ fontSize: 24 }}
          speed={1}
          marqueeOnStart={true}
          loop={true}
          delay={1000}
        >
          Lorem Ipsum is simply dummy text of the printing and typesetting
          industry and typesetting industry.
        </MarqueeText>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
  },
});
```

## Link

## 属性

MarqueText组件基本上继承了TextProps，以下是附加组件：

| Prop              | Type     | Optional | Default | Description                                                                     | HarmonyOS Support |
| ----------------- | -------- | -------- | ------- | ------------------------------------------------------------------------------- | ----------------- |
| marqueeOnStart    | boolean  | true     | true    | 是否在渲染后立即启动字幕动画的标志                                              | yes               |
| speed             | number   | true     | 1       | 以像素/秒计算的速度                                                             | yes               |
| loop              | boolean  | true     | true    | 是否循环字幕动画的标志                                                          | yes               |
| delay             | number   | true     | 0       | 渲染后延迟动画的持续时间，以毫秒为单位                                          | yes               |
| onMarqueeComplete | function | true     | void    | 字幕完成动画并停止时的回调                                                      | yes               |
| consecutive       | boolean  | true     | false   | 一个标志，用于启用模仿HTML字幕元素默认行为的连续模式。如果循环为false，则不生效 | yes               |

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 遗留问题

## 其他

## 开源协议

MIT Lisence
