> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-marquee</code> </h1>
</p>

本项目基于 [react-native-marquee@0.5.0](https://github.com/kyo504/react-native-marquee) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-marquee`，具体版本所属关系如下：

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 0.5.0-0.0.1@deprecated | @react-native-oh-tpl/react-native-marquee | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-marquee) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-marquee/releases) |
| > 0.5.1                  | @react-native-ohos/react-native-marquee   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-marquee) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-marquee/releases) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-marquee
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-marquee
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

## 2. 约束与限制

### 2.1 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-marquee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-marquee/releases)


## 3. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ----------------- | -------- | -------- | ------- | ------------------------------------------------------------ | -------- 
| marqueeOnStart    | 是否在渲染后立即启动字幕动画的标志                           | boolean  | no | All      | yes               |
| speed             | 以像素/秒计算的速度                                          | number   | no | All      | yes               |
| loop              | 是否循环字幕动画的标志                                       | boolean  | no | All      | yes               |
| delay             | 渲染后延迟动画的持续时间，以毫秒为单位                       | number   | no | All      | yes               |
| onMarqueeComplete | 字幕完成动画并停止时的回调                                   | function | no | All      | yes               |
| consecutive       | 一个标志，用于启用模仿HTML字幕元素默认行为的连续模式。如果循环为false，则不生效 | boolean  | no | All      | yes               |

## 4. 遗留问题

## 5. 其他

## 6. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-marquee/blob/master/LICENSE) ，请自由地享受和参与开源。

