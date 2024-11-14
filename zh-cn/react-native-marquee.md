> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-marquee</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kyo504/react-native-marquee/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kyo504/react-native-marquee/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-marquee)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-marquee Releases](https://github.com/react-native-oh-library/react-native-marquee/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-marquee
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-marquee
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

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-marquee Releases](https://github.com/react-native-oh-library/react-native-marquee/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

MarqueText组件基本上继承了[TextProps](https://reactnative.dev/docs/text)，以下是附加组件：

| Name              | Type     | Optional | Default | Description                                                  | Platform | HarmonyOS Support |
| ----------------- | -------- | -------- | ------- | ------------------------------------------------------------ | -------- | ----------------- |
| marqueeOnStart    | boolean  | true     | true    | 是否在渲染后立即启动字幕动画的标志                           | All      | yes               |
| speed             | number   | true     | 1       | 以像素/秒计算的速度                                          | All      | yes               |
| loop              | boolean  | true     | true    | 是否循环字幕动画的标志                                       | All      | yes               |
| delay             | number   | true     | 0       | 渲染后延迟动画的持续时间，以毫秒为单位                       | All      | yes               |
| onMarqueeComplete | function | true     | void    | 字幕完成动画并停止时的回调                                   | All      | yes               |
| consecutive       | boolean  | true     | false   | 一个标志，用于启用模仿HTML字幕元素默认行为的连续模式。如果循环为false，则不生效 | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/kyo504/react-native-marquee/blob/master/LICENSE) ，请自由地享受和参与开源。
