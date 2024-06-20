<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-keyboard-aware-scroll-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-keyboard-aware-scroll-view Releases](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

<!-- tabs:start -->

> [!tip] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keyboard-aware-scroll-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keyboard-aware-scroll-view@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React from "react";
import { TextInput, StyleSheet, ScrollView } from "react-native";
import { KeyboardAwareScrollView } from "react-native-keyboard-aware-scroll-view";

const KasvCom: React.FC = (): JSX.Element => {
  return (
    <>
      <KeyboardAwareScrollView>
        <ScrollView>
          <TextInput style={styles.input} placeholder="键盘事件测试输入框" />
        </ScrollView>
      </KeyboardAwareScrollView>
    </>
  );
};

const styles = StyleSheet.create({
  input: {
    width: "90%",
    marginLeft: "5%",
    borderWidth: 2,
    borderColor: "black",
    height: 40,
    borderRadius: 10,
    fontSize: 26,
    paddingLeft: 6,
    marginTop: 10,
    marginBottom: 10,
  },
});

export default KasvCom;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-keyboard-aware-scroll-view Releases](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases)

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，详情见 [react-native-keyboard-aware-scroll-view 源库地址](https://github.com/APSL/react-native-keyboard-aware-scroll-view)

**组件 KeyboardAwareScrollView**

| Name                      | Description                                                                                    | Type                                                                                                                                                             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| viewIsInsideTabBar        | Adds an extra offset that represents the `TabBarIOS` height.                                   | boolean                                                                                                                                                          | NO       | IOS      | NO                |
| resetScrollToCoords       | Coordinates that will be used to reset the scroll when the keyboard hides.                     | Object: {x: number, y: number}                                                                                                                                   | NO       | All      | YES               |
| enableAutomaticScroll     | When focus in `TextInput` will scroll the position, default is enabled.                        | boolean                                                                                                                                                          | NO       | All      | YES               |
| extraHeight               | Adds an extra offset when focusing the `TextInput`s.                                           | number                                                                                                                                                           | NO       | All      | YES               |
| extraScrollHeight         | Adds an extra offset to the keyboard. Useful if you want to stick elements above the keyboard. | number                                                                                                                                                           | NO       | All      | YES               |
| enableResetScrollToCoords | Lets the user enable or disable automatic resetScrollToCoords.                                 | boolean                                                                                                                                                          | NO       | All      | YES               |
| keyboardOpeningTime       | Sets the delay time before scrolling to new position, default is 250                           | number                                                                                                                                                           | NO       | IOS      | NO                |
| keyboardWillShow          | What to do when the keyboard is about to appear                                                | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| keyboardDidShow           | What to do when the keyboard appears                                                           | (event?) => void                                                                                                                                                 | NO       | All      | YES               |
| keyboardWillHide          | What to do when the keyboard is about to be hidden                                             | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| keyboardDidHide           | What to do when hiding the keyboard                                                            | (event?) => void                                                                                                                                                 | NO       | All      | YES               |
| keyboardWillChangeFrame   | When the keyboard status is about to change                                                    | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| keyboardDidChangeFrame    | When the keyboard status changes                                                               | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| scrollToPosition          | Scroll to specific position with or without animation.                                         | (x: number, y: number, animated: bool = true) => void                                                                                                            | NO       | All      | YES               |
| scrollToEnd               | Scroll to end with or without animation.                                                       | (animated?: bool = true) => void                                                                                                                                 | NO       | All      | YES               |
| scrollIntoView            | Scrolls an element inside a KeyboardAwareScrollView into view.                                 | (element: React.Element<\*>, options: { getScrollPosition: ?(parentLayout, childLayout, contentOffset) => { x: number, y: number, animated: boolean } }) => void | NO       | All      | NO                |

## 遗留问题

- [ ] RN0.72.5版本新架构暂未支持UIManager.viewIsDescendantOf() API，该API功能为：判断组件节点嵌套关系，并在callback中返回boolean类型参数。

- 问题说明：KeyboardAwareScrollView组件逻辑为：监听软键盘出现事件，并绑定callback，在callback中利用UIManager.viewIsDescendantOf()判断组件是否为该组件的子组件，返回true则抬升TextInput的高度，并处理相关Props。由于新架构暂未支持该API，目前IOS与Harmony的新架构均不会调用该API的callback，而Android则始终在callback内返回false，导致该组件的键盘出现事件的相关逻辑功能无法生效。
- 处理现状：由于UIManager.viewIsDescendantOf() API暂无法调用内部callback，现已将其暂时删除，将callback变为外部逻辑。受此影响,KeyboardAwareScrollView组件无法判断当前聚焦的TextInput组件是否为子组件，KeyboardAwareScrollView组件以外的TextInput组件聚焦时也会触发KeyboardAwareScrollView组件的Props设置。且由于oh侧系统软键盘会自动抬起TextInput的高度，KeyboardAwareScrollView组件外的TextInput聚焦时，距离软键盘顶部会有额外的距离。

- 使用建议：KeyboardAwareScrollView组件外不设置可聚焦TextInput组件或将其写入KeyboardAwareScrollView组件slot内。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/APSL/react-native-keyboard-aware-scroll-view/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->