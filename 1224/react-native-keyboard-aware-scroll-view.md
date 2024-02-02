> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-keyboard-aware-scroll-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/APSL/react-native-keyboard-aware-scroll-view">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/APSL/react-native-keyboard-aware-scroll-view/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/APSL/react-native-keyboard-aware-scroll-view)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-keyboard-aware-scroll-view@0.9.5
```

#### **yarn**

```bash
yarn add react-native-keyboard-aware-scroll-view@0.9.5
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

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

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，详情见 [react-native-keyboard-aware-scroll-view 源库地址](https://github.com/APSL/react-native-keyboard-aware-scroll-view)

**组件 KeyboardAwareScrollView**

| Name                      | Description                                                                                    | Type                                                                                                                                                             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| viewIsInsideTabBar        | Adds an extra offset that represents the `TabBarIOS` height.                                   | boolean                                                                                                                                                          | NO       | All      | NO                |
| resetScrollToCoords       | Coordinates that will be used to reset the scroll when the keyboard hides.                     | Object: {x: number, y: number}                                                                                                                                   | NO       | All      | NO                |
| enableAutomaticScroll     | When focus in `TextInput` will scroll the position, default is enabled.                        | boolean                                                                                                                                                          | NO       | All      | NO                |
| extraHeight               | Adds an extra offset when focusing the `TextInput`s.                                           | number                                                                                                                                                           | NO       | All      | NO                |
| extraScrollHeight         | Adds an extra offset to the keyboard. Useful if you want to stick elements above the keyboard. | number                                                                                                                                                           | NO       | All      | NO                |
| enableResetScrollToCoords | Lets the user enable or disable automatic resetScrollToCoords.                                 | boolean                                                                                                                                                          | NO       | All      | NO                |
| keyboardOpeningTime       | Sets the delay time before scrolling to new position, default is 250                           | number                                                                                                                                                           | NO       | IOS      | NO                |
| keyboardWillShow          | What to do when the keyboard is about to appear                                                | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| keyboardDidShow           | What to do when the keyboard appears                                                           | (event?) => void                                                                                                                                                 | NO       | All      | Yes               |
| keyboardWillHide          | What to do when the keyboard is about to be hidden                                             | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| keyboardDidHide           | What to do when hiding the keyboard                                                            | (event?) => void                                                                                                                                                 | NO       | All      | Yes               |
| keyboardWillChangeFrame   | When the keyboard status is about to change                                                    | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| keyboardDidChangeFrame    | When the keyboard status changes                                                               | (event?) => void                                                                                                                                                 | NO       | IOS      | NO                |
| scrollToPosition          | Scroll to specific position with or without animation.                                         | (x: number, y: number, animated: bool = true) => void                                                                                                            | NO       | All      | Yes               |
| scrollToEnd               | Scroll to end with or without animation.                                                       | (animated?: bool = true) => void                                                                                                                                 | NO       | All      | Yes               |
| scrollIntoView            | Scrolls an element inside a KeyboardAwareScrollView into view.                                 | (element: React.Element<\*>, options: { getScrollPosition: ?(parentLayout, childLayout, contentOffset) => { x: number, y: number, animated: boolean } }) => void | NO       | All      | NO                |

## 遗留问题

- [ ] 受 RNOH 侧 UIManager.viewIsDescendantOf() API 的影响，键盘事件判断后的回调函数无法执行，导致主动视图 Scroll 滚动 API 均无法生效。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE) ，请自由地享受和参与开源。
