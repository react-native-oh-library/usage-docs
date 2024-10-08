> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-keyboard-accessory</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ardaogulcan/react-native-keyboard-accessory/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ardaogulcan/react-native-keyboard-accessory/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-keyboard-accessory)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-keyboard-accessory Releases](https://github.com/react-native-oh-library/react-native-keyboard-accessory/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径。

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keyboard-accessory@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keyboard-accessory@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from "react";
import { StyleSheet, View, TextInput, Button, ScrollView } from "react-native";
import { KeyboardAccessoryView } from "react-native-keyboard-accessory";

class ViewExample extends Component {
  state = {
    text: '',
  };
  render() {
	const { text } = this.state;
    return (
      <View style={styles.container}>
        <ScrollView>
        	<TextInput
                placeholder="Write your message"
                underlineColorAndroid="transparent"
                style={styles.input}/>
        </ScrollView>
        <KeyboardAccessoryView alwaysVisible={true} androidAdjustResize>
          {({ isKeyboardVisible }) => (
            <View style={styles.textInputView}>
              <TextInput
                placeholder="Write your message"
                underlineColorAndroid="transparent"
                style={styles.textInput}
				value={text}
				onChangeText={text => this.setState({ text })}
                multiline={true}
              />
              {isKeyboardVisible && (
                <Button
                  style={styles.textInputButton}
                  title="Send"
                  onPress={() => {}}
                />
              )}
            </View>
          )}
        </KeyboardAccessoryView>
      </View>
    );
  }
}

ViewExample.navigationOptions = {
  title: "View Example",
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  textInputView: {
    padding: 8,
    flexDirection: "row",
    justifyContent: "space-between",
    alignItems: "center",
  },
  textInput: {
    flexGrow: 1,
    borderWidth: 1,
    borderRadius: 10,
    borderColor: "#CCC",
    padding: 10,
    fontSize: 16,
    marginRight: 10,
    textAlignVertical: "top",
  },
  input: {
    margin: 20,
    paddingVertical: 10,
    paddingHorizontal: 20,
    borderColor: 'gray',
    borderWidth: 1,
    backgroundColor: '#FFF',
  },
  textInputButton: {
    flexShrink: 1,
  },
});

export default ViewExample;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-keyboard-accessory Releases](https://github.com/react-native-oh-library/react-native-keyboard-accessory/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### KeyboardAccessoryView属性

用于在键盘上方显示一个自定义的工具栏或附加内容，允许用户在输入内容时操作工具栏中的按钮或其他控件

| Name                  | **Description**                                              | **Type**               | Required | **Default** | Platform    | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------ | ---------------------- | -------- | ----------- | ----------- | ----------------- |
| `style`               | Style `object` or `StyleSheet` reference which will be applied to Accessory `View` | `object`               | no       | `null`      | iOS/Android | yes               |
| `animateOn`           | Enables show/hide animation on given platform. Values: `['ios', 'android', 'all', 'none','harmony']`. | `enum:string`          | no       | `ios`       | iOS/Android | yes               |
| `animationConfig`     | For passing custom animations to show/hide. If given prop is function, `duration` and `easing` parameters from `Keyboard` event will be passed to the function, function should return `LayoutAnimation` compatible animation config. Or you can directly pass animation config object. | `function` or `object` | no       | `null`      | iOS/Android | yes               |
| `alwaysVisible`       | When set to `true` Accessory View will be always visible at the bottom of the screen. Good for sticky `TextInput`'s | `boolean`              | no       | `false`     | iOS/Android | yes               |
| `bumperHeight`        | Bumper height to prevent visual glitches if animation couldn't keep up with the keyboard animation. | `number`               | no       | 15          | iOS/Android | yes               |
| `visibleOpacity`      | Opacity of the Accessory when it is visible. *Note:* Opacity is used for hiding the accessory to prevent render delays. | `number`               | no       | 1           | iOS/Android | yes               |
| `heightProperty`      | Control how the component manages its height. The component listens for children changes and automatically adjusts its height, so `height` is usually sufficient. For use with a multiline, autogrowing `TextInput`, `minHeight` is recommended. Values: `['height', 'minHeight']` | `enum:string`          | no       | `height`    | iOS/Android | yes               |
| `hiddenOpacity`       | Opacity of the Accessory when it is hidden.                  | `number`               | no       | 0           | iOS/Android | yes               |
| `hideBorder`          | Set true if you want to hide top border of the Accessory     | `boolean`              | no       | false       | iOS/Android | yes               |
| `inSafeAreaView`      | Set true if you want to adapt SafeAreaView on iPhone X       | `boolean`              | no       | false       | iOS         | no                |
| `androidAdjustResize` | Set true in ejected apps to adjust resize                    | `boolean`              | no       | false       | Android     | no                |
| `avoidKeyboard`       | Set true if you want accessory to maintain KeyboardAvoidingView behavior. You shouldn't use any other Keyboard Avoiding library when you set this to `true` | `boolean`              | no       | false       | iOS/Android | yes               |

### KeyboardAccessoryNavigation属性

用于处理键盘导航的组件

| Name                      | **Description**                                              | **Type**      | Required | **Default**                              | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | ------------- | -------- | ---------------------------------------- | ----------- | ----------------- |
| `doneButtonTitle`         | Title text to show on the right Button of Navigation View    | `string`      | no       | `'Done'`                                 | iOS/Android | yes               |
| `tintColor`               | Tint color for the arrows and done button                    | `string`      | no       | `'#007AFF'`                              | iOS/Android | yes               |
| `doneButton`              | Replace default Done Button. Non-Touchable node should be provided. | `node`        | no       | `null`                                   | iOS/Android | yes               |
| `nextButton`              | Replace default Next Button. Non-Touchable node should be provided. | `node`        | no       | `null`                                   | iOS/Android | yes               |
| `previousButton`          | Replace default Previous Button. Non-Touchable node should be provided. | `node`        | no       | `null`                                   | iOS/Android | yes               |
| `doneDisabled`            | Disables Done Button                                         | `boolean`     | no       | false                                    | no          | no                |
| `nextDisabled`            | Disables Next Button                                         | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `previousDisabled`        | Disables Previous Button                                     | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `doneHidden`              | Hides Done Button                                            | `boolean`     | no       | false                                    | no          | no                |
| `nextHidden`              | Hides Next Button                                            | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `previousHidden`          | Hides Previous Button                                        | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `accessoryStyle`          | Style object or StyleSheet reference which will be applied to Navigation Accessory `View`. | `object`      | no       | null                                     | iOS/Android | yes               |
| `doneButtonStyle`         | Style object or StyleSheet reference which will be applied to Done Button `View` | `object`      | no       | null                                     | iOS/Android | yes               |
| `doneButtonTitleStyle`    | Style object or StyleSheet reference which will be applied to Done Button `Text` | `object`      | no       | null                                     | iOS/Android | yes               |
| `doneButtonHitslop`       | This defines how far your touch can start away from the doneButton | `Insets`      | no       | { left: 0, top: 0, right: 0, bottom: 0 } | iOS/Android | yes               |
| `previousButtonStyle`     | Style object or StyleSheet reference which will be applied to Previous Button `View` | `object`      | no       | 0                                        | iOS/Android | yes               |
| `nextButtonStyle`         | Style object or StyleSheet reference which will be applied to Next Button `View` | `object`      | no       | 0                                        | iOS/Android | yes               |
| `nextButtonDirection`     | Arrow direction for the Next Button. Values: `['down', 'up', 'right', 'left']`. | `enum:string` | no       | `'down'`                                 | iOS/Android | yes               |
| `nextButtonHitslop`       | This defines how far your touch can start away from the nextButton | `Insets`      | no       | { left: 0, top: 0, right: 0, bottom: 0 } | iOS/Android | yes               |
| `previousButtonDirection` | Arrow direction for the Previous Button. Values: `['down', 'up', 'right', 'left']`. | `enum:string` | no       | `'up'`                                   | iOS/Android | yes               |
| `previousButtonHitslop`   | This defines how far your touch can start away from the previousButton | `Insets`      | no       | { left: 0, top: 0, right: 0, bottom: 0 } | iOS/Android | yes               |
| `onDone`                  | Triggered on Done Button `press`                             | `function`    | no       | null                                     | iOS/Android | yes               |
| `onNext`                  | Triggered on Next Button `press`                             | `function`    | no       | null                                     | iOS/Android | yes               |
| `onPrevious`              | Triggered on Previous Button `press`                         | `function`    | no       | null                                     | iOS/Android | yes               |

### KeyboardAwareTabBarComponent属性

| Name              | **Description**                                              | **Type**           | Required | **Default** | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------------------ | -------- | ----------- | ----------- | ----------------- |
| `TabBarComponent` | Provide TabBarComponent to render. Usually from `react-navigation` | `node`, `function` | no       |             | iOS/Android | yes               |

## 遗留问题

## 其他

- inSafeAreaView 是专为适配ios的刘海和底部横条布局设计的，HarmonyOS没有此类问题，只支持默认设置false。

- androidAdjustResize 是为适配安卓键盘弹出时窗口的布局，HarmonyOS键盘弹出没有该问题，无需设置该属性。

- doneDisabled和doneHidden属性在iOS,Android不生效，HarmonyOS与其表现一致: [issue#99](https://github.com/ardaogulcan/react-native-keyboard-accessory/issues/99)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ardaogulcan/react-native-keyboard-accessory/blob/master/LICENSE) ，请自由地享受和参与开源。