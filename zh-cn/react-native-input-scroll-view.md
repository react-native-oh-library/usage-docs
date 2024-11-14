> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-input-scroll-view</code> </h1>
</p>
<p align="center">
    <a href=https://github.com/baijunjie/react-native-input-scroll-view>
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/baijunjie/react-native-input-scroll-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-input-scroll-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-input-scroll-view Releases](https://github.com/react-native-oh-library/react-native-input-scroll-view/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-input-scroll-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-input-scroll-view
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { StyleSheet, TextInput, View, TouchableOpacity, Text } from 'react-native';
import InputScrollView from 'react-native-input-scroll-view';


const keyboardOffsetInput = () => {
    const [text, setText] = useState('');
    return (
        <View style={styles.container}>
            <InputScrollView  keyboardOffset={100}>
                <View style={styles.placeholder} />
                <TextInput style={styles.input}
                    value={text}
                    multiline
                    onChangeText={setText}
                />
            </InputScrollView>
        </View>
    );
}


const styles = StyleSheet.create({
    container: {
        backgroundColor: '#EEE',
    },
    placeholder: {
        height: 400,
        justifyContent: 'center',
        alignItems: 'center',
      },
    input: {
        margin: 20,
        paddingVertical: 10,
        paddingHorizontal: 20,
        borderColor: 'gray',
        borderWidth: 1,
        backgroundColor: '#FFF',
    },
});

export default keyboardOffsetInput;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-input-scroll-view Releases](https://github.com/react-native-oh-library/react-native-input-scroll-view/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                      | **Description**                                              | Type   | Required | **Default** | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------- | ----------------- |
| topOffset                 | `InputScrollView` 相对于窗口顶部的偏移量。当屏幕包含 `TopBar` 时，通常设置为 `TopBar` 的高度。如果未明确设置，程序会自动判断，但是可能会引起问题。 [issues#43](https://github.com/baijunjie/react-native-input-scroll-view/issues/43)。 | number | false    | undefined   | iOS/Android | yes               |
| keyboardOffset            | 当自动调整时，光标相对于键盘顶部的偏移量                     | number | false    | 40          | iOS/Android | yes               |
| multilineInputStyle       | 如果你的多行输入框有特定的样式，那么为了光标能够精准调整到键盘上方，应该将多行文本的样式也设置在这里，主要包含 `fontSize`、`fontFamily`、`lineHeight` 等会影响到光标位置的样式属性。**注意，不要包含 `width` 和 `height`**。 | Style  | false    | null        | iOS/Android | yes               |
| useAnimatedScrollView     | 用 `Animated.ScrollView` 组件替换 `ScrollView` 组件。        | bool   | false    | false       | iOS/Android | yes               |
| supportHardwareKeyboard   | `beta` 如果你的设备不使用软键盘，可以尝试使用此参数解决问题。 [issues#69](https://github.com/baijunjie/react-native-input-scroll-view/issues/69) | bool   | false    | false       | iOS/Android | yes               |
| keyboardAvoidingViewProps | `KeyboardAvoidingView` 组件的 Props。详细请查阅: https://facebook.github.io/react-native/docs/keyboardavoidingview | props  | false    | null        | iOS/Android | yes               |
| ...ScrollView.props       | 继承 `ScrollView` 组件的所有属性。详细请查阅: https://facebook.github.io/react-native/docs/scrollview.html | props  | false    |             | iOS/Android | yes               |

#### 

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/baijunjie/react-native-input-scroll-view/blob/master/LICENSE) ，请自由地享受和参与开源。