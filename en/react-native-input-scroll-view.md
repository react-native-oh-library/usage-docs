> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-input-scroll-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-input-scroll-view Releases](https://github.com/react-native-oh-library/react-native-input-scroll-view/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-input-scroll-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-input-scroll-view@file:#
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-input-scroll-view Releases](https://github.com/react-native-oh-library/react-native-input-scroll-view/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | **Description**                                              | Type   | Required | **Default** | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------- | ----------------- |
| topOffset                 | `InputScrollView` 相对于窗口顶部的偏移量。当屏幕包含 `TopBar` 时，通常设置为 `TopBar` 的高度。如果未明确设置，程序会自动判断，但是可能会引起问题。 [issues#43](https://github.com/baijunjie/react-native-input-scroll-view/issues/43)。 | number | false    | undefined   | iOS/Android | yes               |
| keyboardOffset            | 当自动调整时，光标相对于键盘顶部的偏移量                     | number | false    | 40          | iOS/Android | yes               |
| multilineInputStyle       | 如果你的多行输入框有特定的样式，那么为了光标能够精准调整到键盘上方，应该将多行文本的样式也设置在这里，主要包含 `fontSize`、`fontFamily`、`lineHeight` 等会影响到光标位置的样式属性。**注意，不要包含 `width` 和 `height`**。 | Style  | false    | null        | iOS/Android | yes               |
| useAnimatedScrollView     | 用 `Animated.ScrollView` 组件替换 `ScrollView` 组件。        | bool   | false    | false       | iOS/Android | yes               |
| supportHardwareKeyboard   | `beta` 如果你的设备不使用软键盘，可以尝试使用此参数解决问题。 [issues#69](https://github.com/baijunjie/react-native-input-scroll-view/issues/69) | bool   | false    | false       | iOS/Android | yes               |
| keyboardAvoidingViewProps | `KeyboardAvoidingView` 组件的 Props。详细请查阅: https://facebook.github.io/react-native/docs/keyboardavoidingview | props  | false    | null        | iOS/Android | yes               |
| ...ScrollView.props       | 继承 `ScrollView` 组件的所有属性。详细请查阅: https://facebook.github.io/react-native/docs/scrollview.html | props  | false    |             | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/baijunjie/react-native-input-scroll-view/blob/master/LICENSE).
