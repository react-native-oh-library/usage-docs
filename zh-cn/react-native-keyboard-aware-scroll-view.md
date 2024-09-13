<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-keyboard-aware-scroll-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/APSL/react-native-keyboard-aware-scroll-view">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/APSL/react-native-keyboard-aware-scroll-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-keyboard-aware-scroll-view Releases](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

<!-- tabs:start -->

> [!TIP] # 处替换为 tgz 包的路径

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
import React, { useState, useRef } from "react";
import ReactNative, { TextInput, StyleSheet, Button, View, Text } from "react-native";
import { KeyboardAwareScrollView } from "react-native-keyboard-aware-scroll-view";

const Labels = ['Username', 'Password', 'Firstname', 'Lastname', 'Address', 'Phone', 'Email', 'QQ', 'WeChat', 'Webo'];

export const ReactNativeKeyboardAwareScrollView: React.FC = (): JSX.Element => {

    const [resetScrollToCoords, setResetScrollToCoords] = useState({ x: 20, y: 20 });
    const [enableAutomaticScroll, setEnableAutomaticScroll] = useState(true);
    const [extraHeight, setExtraHeight] = useState(50);
    const [extraScrollHeight, setExtraScrollHeight] = useState(60);
    const [enableResetScrollToCoords, setEnableResetScrollToCoords] = useState(true);

    return <KeyboardAwareScrollView
        style={styles.scroll}
       resetScrollToCoords={resetScrollToCoords}
        enableAutomaticScroll={enableAutomaticScroll}
        extraHeight={extraHeight}
        extraScrollHeight={extraScrollHeight}
        enableResetScrollToCoords={enableResetScrollToCoords}
    >
        {
            Labels.map(item => {
                return <View key={item}>
                    <Text>{item}:</Text>
                    <TextInput style={styles.input} placeholder="请输入" />
                </View>;
            })
        }
    </KeyboardAwareScrollView>;
};

const styles = StyleSheet.create({
    scroll: {
        backgroundColor: '#f0f0f0'
    },
    input: {
        width: 300,
        marginLeft: 20,
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
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-keyboard-aware-scroll-view Releases](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-keyboard-aware-scroll-view 源库地址](https://github.com/APSL/react-native-keyboard-aware-scroll-view)

| Name                      | Description                                                                                    | Type                                                                                                                                                             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| viewIsInsideTabBar        | Adds an extra offset that represents the `TabBarIOS` height.                                   | boolean                                                                                                                                                          | NO       | iOS      | YES                |
| resetScrollToCoords       | Coordinates that will be used to reset the scroll when the keyboard hides.                     | Object: {x: number, y: number}                                                                                                                                   | NO       | All      | YES               |
| enableAutomaticScroll     | When focus in `TextInput` will scroll the position, default is enabled.                        | boolean                                                                                                                                                          | NO       | All      | YES               |
| extraHeight               | Adds an extra offset when focusing the `TextInput`s.                                           | number                                                                                                                                                           | NO       | All      | YES               |
| extraScrollHeight         | Adds an extra offset to the keyboard. Useful if you want to stick elements above the keyboard. | number                                                                                                                                                           | NO       | All      | YES               |
| enableResetScrollToCoords | Lets the user enable or disable automatic resetScrollToCoords.                                 | boolean                                                                                                                                                          | NO       | All      | YES               |
| keyboardOpeningTime       | Sets the delay time before scrolling to new position, default is 250                           | number                                                                                                                                                           | NO       | iOS      | YES                |
| onKeyboardWillShow          | What to do when the keyboard is about to appear                                                | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| onKeyboardDidShow           | What to do when the keyboard appears                                                           | (event?) => void                                                                                                                                                 | NO       | All      | YES               |
| onKeyboardWillHide          | What to do when the keyboard is about to be hidden                                             | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| onKeyboardDidHide           | What to do when hiding the keyboard                                                            | (event?) => void                                                                                                                                                 | NO       | All      | YES               |
| onKeyboardWillChangeFrame   | When the keyboard status is about to change                                                    | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| onKeyboardDidChangeFrame    | When the keyboard status changes                                                               | (event?) => void                                                                                                                                                 | NO       | iOS      | NO                |
| scrollToPosition          | Scroll to specific position with or without animation.                                         | (x: number, y: number, animated: bool = true) => void                                                                                                            | NO       | All      | YES               |
| scrollToEnd               | Scroll to end with or without animation.                                                       | (animated?: bool = true) => void                                                                                                                                 | NO       | All      | YES               |
| scrollIntoView            | Scrolls an element inside a KeyboardAwareScrollView into view.                                 | (element: React.Element<\*>, options: { getScrollPosition: ?(parentLayout, childLayout, contentOffset) => { x: number, y: number, animated: boolean } }) => void | NO       | All      | YES                |

## 遗留问题

- [ ] RN0.72.28版本新架构暂未支持UIManager.viewIsDescendantOf() API，该API功能为：判断组件节点嵌套关系，并在callback中返回boolean类型参数: [issue#12](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/12)
- [ ] 方法onKeyboardDidChangeFrame未实现 HarmonyOS化 问题:[issue#16](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/16)
- [ ] 方法onKeyboardWillChangeFrame未实现 HarmonyOS化 问题:[issue#15](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/15)
- [ ] 方法onKeyboardWillHide未实现 HarmonyOS化 问题:[issue#14](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/14)
- [ ] 方法onKeyboardWillShow未实现 HarmonyOS化 问题:[issue#13](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/13)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/APSL/react-native-keyboard-aware-scroll-view/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->