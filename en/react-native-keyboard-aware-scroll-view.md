> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-keyboard-aware-scroll-view Releases](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keyboard-aware-scroll-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keyboard-aware-scroll-view@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-keyboard-aware-scroll-view Releases](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-keyboard-aware-scroll-view](https://github.com/APSL/react-native-keyboard-aware-scroll-view)

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

## Known Issues

- [ ] RN0.72.28版本新架构暂未支持UIManager.viewIsDescendantOf() API，该API功能为：判断组件节点嵌套关系，并在callback中返回boolean类型参数: [issue#12](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/12)
- [ ] 键盘抬起部分生命周期未HarmonyOS化，功能不受影响 问题:[issue#17](https://github.com/react-native-oh-library/react-native-keyboard-aware-scroll-view/issues/17)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/APSL/react-native-keyboard-aware-scroll-view/blob/master/LICENSE).
