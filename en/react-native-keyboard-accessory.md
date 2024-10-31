> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-keyboard-accessory)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-keyboard-accessory Releases](https://github.com/react-native-oh-library/react-native-keyboard-accessory/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).。

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keyboard-accessory@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keyboard-accessory@file:#
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { StyleSheet, View, TextInput, Button, ScrollView } from "react-native";
import { KeyboardAccessoryView } from "react-native-keyboard-accessory";

class ViewExample extends Component {
  state = {
    text: "",
  };
  render() {
    const { text } = this.state;
    return (
      <View style={styles.container}>
        <ScrollView>
          <TextInput
            placeholder="Write your message"
            underlineColorAndroid="transparent"
            style={styles.input}
          />
        </ScrollView>
        <KeyboardAccessoryView alwaysVisible={true} androidAdjustResize>
          {({ isKeyboardVisible }) => (
            <View style={styles.textInputView}>
              <TextInput
                placeholder="Write your message"
                underlineColorAndroid="transparent"
                style={styles.textInput}
                value={text}
                onChangeText={(text) => this.setState({ text })}
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
    borderColor: "gray",
    borderWidth: 1,
    backgroundColor: "#FFF",
  },
  textInputButton: {
    flexShrink: 1,
  },
});

export default ViewExample;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-keyboard-accessory Releases](https://github.com/react-native-oh-library/react-native-keyboard-accessory/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### KeyboardAccessoryViewProperties

用于在键盘上方显示一个自定义的工具栏或附加内容，允许用户在输入内容时操作工具栏中的按钮或 Others 控件

| Name                  | **Description**                                                                                                                                                                                                                                                                         | **Type**               | Required | **Default** | Platform    | HarmonyOS Support |
| --------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------- | -------- | ----------- | ----------- | ----------------- |
| `style`               | Style `object` or `StyleSheet` reference which will be applied to Accessory `View`                                                                                                                                                                                                      | `object`               | no       | `null`      | iOS/Android | yes               |
| `animateOn`           | Enables show/hide animation on given platform. Values: `['ios', 'android', 'all', 'none','harmony']`.                                                                                                                                                                                   | `enum:string`          | no       | `ios`       | iOS/Android | yes               |
| `animationConfig`     | For passing custom animations to show/hide. If given prop is function, `duration` and `easing` parameters from `Keyboard` event will be passed to the function, function should return `LayoutAnimation` compatible animation config. Or you can directly pass animation config object. | `function` or `object` | no       | `null`      | iOS/Android | yes               |
| `alwaysVisible`       | When set to `true` Accessory View will be always visible at the bottom of the screen. Good for sticky `TextInput`'s                                                                                                                                                                     | `boolean`              | no       | `false`     | iOS/Android | yes               |
| `bumperHeight`        | Bumper height to prevent visual glitches if animation couldn't keep up with the keyboard animation.                                                                                                                                                                                     | `number`               | no       | 15          | iOS/Android | yes               |
| `visibleOpacity`      | Opacity of the Accessory when it is visible. _Note:_ Opacity is used for hiding the accessory to prevent render delays.                                                                                                                                                                 | `number`               | no       | 1           | iOS/Android | yes               |
| `heightProperty`      | Control how the component manages its height. The component listens for children changes and automatically adjusts its height, so `height` is usually sufficient. For use with a multiline, autogrowing `TextInput`, `minHeight` is recommended. Values: `['height', 'minHeight']`      | `enum:string`          | no       | `height`    | iOS/Android | no                |
| `hiddenOpacity`       | Opacity of the Accessory when it is hidden.                                                                                                                                                                                                                                             | `number`               | no       | 0           | iOS/Android | no                |
| `hideBorder`          | Set true if you want to hide top border of the Accessory                                                                                                                                                                                                                                | `boolean`              | no       | false       | iOS/Android | yes               |
| `inSafeAreaView`      | Set true if you want to adapt SafeAreaView on iPhone X                                                                                                                                                                                                                                  | `boolean`              | no       | false       | iOS         | no                |
| `androidAdjustResize` | Set true in ejected apps to adjust resize                                                                                                                                                                                                                                               | `boolean`              | no       | false       | Android     | no                |
| `avoidKeyboard`       | Set true if you want accessory to maintain KeyboardAvoidingView behavior. You shouldn't use any other Keyboard Avoiding library when you set this to `true`                                                                                                                             | `boolean`              | no       | false       | iOS/Android | yes               |

### KeyboardAccessoryNavigationProperties

用于处理键盘导航的组件

| Name                      | **Description**                                                                            | **Type**      | Required | **Default**                              | Platform    | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------------------ | ------------- | -------- | ---------------------------------------- | ----------- | ----------------- |
| `doneButtonTitle`         | Title text to show on the right Button of Navigation View                                  | `string`      | no       | `'Done'`                                 | iOS/Android | yes               |
| `tintColor`               | Tint color for the arrows and done button                                                  | `string`      | no       | `'#007AFF'`                              | iOS/Android | yes               |
| `doneButton`              | Replace default Done Button. Non-Touchable node should be provided.                        | `node`        | no       | `null`                                   | iOS/Android | yes               |
| `nextButton`              | Replace default Next Button. Non-Touchable node should be provided.                        | `node`        | no       | `null`                                   | iOS/Android | yes               |
| `previousButton`          | Replace default Previous Button. Non-Touchable node should be provided.                    | `node`        | no       | `null`                                   | iOS/Android | yes               |
| `doneDisabled`            | Disables Done Button                                                                       | `boolean`     | no       | false                                    | no          | no                |
| `nextDisabled`            | Disables Next Button                                                                       | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `previousDisabled`        | Disables Previous Button                                                                   | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `doneHidden`              | Hides Done Button                                                                          | `boolean`     | no       | false                                    | no          | no                |
| `nextHidden`              | Hides Next Button                                                                          | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `previousHidden`          | Hides Previous Button                                                                      | `boolean`     | no       | false                                    | iOS/Android | yes               |
| `accessoryStyle`          | Style object or StyleSheet reference which will be applied to Navigation Accessory `View`. | `object`      | no       | null                                     | iOS/Android | yes               |
| `doneButtonStyle`         | Style object or StyleSheet reference which will be applied to Done Button `View`           | `object`      | no       | null                                     | iOS/Android | yes               |
| `doneButtonTitleStyle`    | Style object or StyleSheet reference which will be applied to Done Button `Text`           | `object`      | no       | null                                     | iOS/Android | yes               |
| `doneButtonHitslop`       | This defines how far your touch can start away from the doneButton                         | `Insets`      | no       | { left: 0, top: 0, right: 0, bottom: 0 } | iOS/Android | yes               |
| `previousButtonStyle`     | Style object or StyleSheet reference which will be applied to Previous Button `View`       | `object`      | no       | 0                                        | iOS/Android | yes               |
| `nextButtonStyle`         | Style object or StyleSheet reference which will be applied to Next Button `View`           | `object`      | no       | 0                                        | iOS/Android | yes               |
| `nextButtonDirection`     | Arrow direction for the Next Button. Values: `['down', 'up', 'right', 'left']`.            | `enum:string` | no       | `'down'`                                 | iOS/Android | yes               |
| `nextButtonHitslop`       | This defines how far your touch can start away from the nextButton                         | `Insets`      | no       | { left: 0, top: 0, right: 0, bottom: 0 } | iOS/Android | yes               |
| `previousButtonDirection` | Arrow direction for the Previous Button. Values: `['down', 'up', 'right', 'left']`.        | `enum:string` | no       | `'up'`                                   | iOS/Android | yes               |
| `previousButtonHitslop`   | This defines how far your touch can start away from the previousButton                     | `Insets`      | no       | { left: 0, top: 0, right: 0, bottom: 0 } | iOS/Android | yes               |
| `onDone`                  | Triggered on Done Button `press`                                                           | `function`    | no       | null                                     | iOS/Android | yes               |
| `onNext`                  | Triggered on Next Button `press`                                                           | `function`    | no       | null                                     | iOS/Android | yes               |
| `onPrevious`              | Triggered on Previous Button `press`                                                       | `function`    | no       | null                                     | iOS/Android | yes               |

### KeyboardAwareTabBarComponentProperties

| Name              | **Description**                                                    | **Type**           | Required | **Default** | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------ | ------------------ | -------- | ----------- | ----------- | ----------------- |
| `TabBarComponent` | Provide TabBarComponent to render. Usually from `react-navigation` | `node`, `function` | no       |             | iOS/Android | yes               |

## Known Issues

## Others

- inSafeAreaView 是专为适配 ios 的刘海和底部横条布局设计的，HarmonyOS 没有此类问题，只支持默认设置 false。

- androidAdjustResize 是为适配安卓键盘弹出时窗口的布局，HarmonyOS 键盘弹出没有该问题，无需设置该 Properties。

- doneDisabled 和 doneHiddenProperties 在 iOS,Android 不生效，HarmonyOS 与其表现一致: [issue#99](https://github.com/ardaogulcan/react-native-keyboard-accessory/issues/99)

- heightProperty属性在iOS,Android不生效，HarmonyOS与其表现一致: [issue#100](https://github.com/ardaogulcan/react-native-keyboard-accessory/issues/100)

- hiddenOpacity属性在iOS,Android不生效，HarmonyOS与其表现一致: [issue#101](https://github.com/ardaogulcan/react-native-keyboard-accessory/issues/101)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ardaogulcan/react-native-keyboard-accessory/blob/master/LICENSE).
