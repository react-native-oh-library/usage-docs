> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-dismiss-keyboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DanielMSchmidt/react-native-dismiss-keyboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/DanielMSchmidt/react-native-dismiss-keyboard/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/DanielMSchmidt/react-native-dismiss-keyboard)


## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-dismiss-keyboard@1.0.0
```

#### **yarn**

```bash
yarn add react-native-dismiss-keyboard@1.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import {
    AppRegistry,
    StyleSheet,
    TextInput,
    View,
    Text,
    Keyboard
} from 'react-native';

export default class ReactNativeDismissKeyboardExample extends Component {

    keyboardDidShowListener = null;
    keyboardDidHideListener = null;
    state = { KeyboardShown: false };

    constructor(props) {
        super(props);
        this.keyboardDidShowListener = null;
        this.keyboardDidHideListener = null;
        this.state = { KeyboardShown: false };
    }

    //键盘弹出事件响应
    keyboardDidShowHandler(event) {
        this.setState({ KeyboardShown: true });
        console.log(event.endCoordinates.height);
    }

    //键盘隐藏事件响应
    keyboardDidHideHandler(event) {
        this.setState({ KeyboardShown: false });
    }

    //强制隐藏键盘
    dissmissKeyboard() {
        Keyboard.dismiss();
        console.log("输入框当前焦点状态：" + this.refs.bottomInput.isFocused());
    }

    render() {
        return (
            <View style={[styles.container]}>
                <View style={[styles.flexDirection, styles.inputHeight]}>
                    <TextInput style={styles.textInputStyle} ref="bottomInput" />
                    <Text style={styles.buttonStyle}
                        onPress={this.dissmissKeyboard.bind(this)}>
                        收起键盘
                    </Text>
                </View>
            </View>
        )
    }
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        paddingTop: 15,
        backgroundColor: '#ffffff'
    },
    flexDirection: {
        flexDirection: 'row'
    },
    inputHeight: {
        height: 35,
        alignItems: 'center'
    },
    textInputStyle: {
        flex: 1,
        height: 35,
        fontSize: 18,
        borderWidth: 1,
        borderColor: '#4CAF50',
        borderRadius: 8,
        marginRight: 8
    },
    buttonStyle: {
        fontSize: 20,
        color: 'white',
        width: 100,
        textAlign: 'center',
        backgroundColor: '#4CA300'
    },
});
```
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 电脑ROM。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop   | Description   | Type       | Required | Platform | HarmonyOS Support |
| ----- | ----- | -------- | -------- | -------- | -------- |
| `addListener`  | Register a JavaScript function that listens to handle native keyboard notification events. | function  | no     | All  | yes      |
| `dismiss`  | Retract the pop-up keyboard and make the current text box lose focus. | function  |  no     | All   | yes      |
| `scheduleLayoutAnimation`  |Used to synchronize changes in the size or position of a TextInput (or other keyboard attachment view) with keyboard movements.| function | no     | All | yes      |
| `isVisible`  | Whether the keyboard is currently displayed.| function      |  no     | All   | yes      |
| `metrics`  | If a soft keyboard is displayed, return the size of the soft keyboard.| function      |  no     | All   | yes      |

## 遗留问题

## 其他

## 开源协议
本项目基于 [The MIT License (MIT)](https://github.com/DanielMSchmidt/react-native-dismiss-keyboard/blob/master/LICENSE) ，请自由地享受和参与开源。