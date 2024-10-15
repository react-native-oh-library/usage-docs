<!-- {% raw %} -->
> Template version: v0.2.2

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


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-marquee)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-marquee Releases](https://github.com/react-native-oh-library/react-native-marquee/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).


#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-marquee@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-marquee@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-marquee Releases](https://github.com/react-native-oh-library/react-native-marquee/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

MarqueText组件基本上继承了[TextProps](https://reactnative.dev/docs/text)，以下是附加组件：

| Name              | Type     | Optional | Default | Description                                                  | Platform | HarmonyOS Support |
| ----------------- | -------- | -------- | ------- | ------------------------------------------------------------ | -------- | ----------------- |
| marqueeOnStart    | boolean  | true     | true    | 是否在渲染后立即启动字幕动画的标志                           | All      | yes               |
| speed             | number   | true     | 1       | 以像素/秒计算的速度                                          | All      | yes               |
| loop              | boolean  | true     | true    | 是否循环字幕动画的标志                                       | All      | yes               |
| delay             | number   | true     | 0       | 渲染后延迟动画的持续时间，以毫秒为单位                       | All      | yes               |
| onMarqueeComplete | function | true     | void    | 字幕完成动画并停止时的回调                                   | All      | yes               |
| consecutive       | boolean  | true     | false   | 一个标志，用于启用模仿HTML字幕元素默认行为的连续模式。如果循环为false，则不生效 | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/kyo504/react-native-marquee/blob/master/LICENSE).

<!-- {% endraw %} -->