> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-phone-number-input</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/garganurag893/react-native-phone-number-input">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/garganurag893/react-native-phone-number-input/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/garganurag893/react-native-phone-number-input)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm npm i react-native-phone-number-input@2.1.0 --save
```

#### **yarn**

```bash
yarn add react-native-phone-number-input@2.1.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useRef } from "react";
import {
  SafeAreaView,
  StyleSheet,
  View,
  StatusBar,
  TouchableOpacity,
  Text,
} from "react-native";
import PhoneInput from "react-native-phone-number-input";
import { Colors } from "react-native/Libraries/NewAppScreen";

export const InputDemo = () => {
  const [value, setValue] = useState("");
  const [countryCode, setCountryCode] = useState("");
  const [formattedValue, setFormattedValue] = useState("");
  const [valid, setValid] = useState(false);
  const [disabled, setDisabled] = useState(false);
  const [showMessage, setShowMessage] = useState(false);
  const phoneInput = useRef < PhoneInput > null;

  return (
    <>
      <StatusBar barStyle="dark-content" />
      <View style={styles.container}>
        <SafeAreaView style={styles.wrapper}>
          {showMessage && (
            <View style={styles.message}>
              <Text>Country Code : {countryCode}</Text>
              <Text>Value : {value}</Text>
              <Text>Formatted Value : {formattedValue}</Text>
              <Text>Valid : {valid ? "true" : "false"}</Text>
            </View>
          )}
          <PhoneInput
            ref={phoneInput}
            defaultValue={value}
            disableArrowIcon={true}
            defaultCode="AX"
            layout="first"
            onChangeText={(text) => {
              setValue(text);
            }}
            onChangeFormattedText={(text) => {
              setFormattedValue(text);
              setCountryCode(phoneInput.current?.getCountryCode() || "");
            }}
            countryPickerProps={{ withAlphaFilter: true }}
            disabled={disabled}
            withDarkTheme={false}
            withShadow={false}
            autoFocus={true}
            renderDropdownImage={<h1>Hello, world!</h1>}
          />
          <TouchableOpacity
            style={styles.button}
            onPress={() => {
              const checkValid = phoneInput.current?.isValidNumber(value);
              setShowMessage(true);
              setValid(checkValid ? checkValid : false);
              setCountryCode(phoneInput.current?.getCountryCode() || "");
              let getNumberAfterPossiblyEliminatingZero =
                phoneInput.current?.getNumberAfterPossiblyEliminatingZero();
              console.log(getNumberAfterPossiblyEliminatingZero);
            }}
          >
            <Text style={styles.buttonText}>Check</Text>
          </TouchableOpacity>
        </SafeAreaView>
      </View>
    </>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: Colors.lighter,
  },
  wrapper: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  button: {
    marginTop: 20,
    height: 50,
    width: 300,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#7CDB8A",
    shadowColor: "rgba(0,0,0,0.4)",
    shadowOffset: {
      width: 1,
      height: 5,
    },
    shadowOpacity: 0.34,
    shadowRadius: 6.27,
    elevation: 10,
  },
  buttonText: {
    color: "white",
    fontSize: 14,
  },
  message: {
    borderWidth: 1,
    borderRadius: 5,
    padding: 20,
    marginBottom: 20,
    justifyContent: "center",
    alignItems: "flex-start",
  },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                     | Description                           | Type                                                                                                          | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| defaultCode              | default country code                  | [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L252) | no       | Android iOS | yes               |
| withDarkTheme            | Keyboard Theme Colors                 | boolean                                                                                                       | no       | iOS         | partially         |
| withShadow               | Whether there is a shadow             | boolean                                                                                                       | no       | Android iOS | yes               |
| autoFocus                | focus                                 | boolean                                                                                                       | no       | Android iOS | yes               |
| defaultValue             | default value                         | string                                                                                                        | no       | Android iOS | yes               |
| value                    | value                                 | string                                                                                                        | no       | Android iOS | yes               |
| disabled                 | disabled                              | boolean                                                                                                       | no       | Android iOS | yes               |
| disableArrowIcon         | disable arrow icon                    | boolean                                                                                                       | no       | Android iOS | yes               |
| placeholder              | placeholder                           | string                                                                                                        | no       | Android iOS | yes               |
| onChangeCountry          | Events for country                    | (country: Country) => void                                                                                    | no       | Android iOS | yes               |
| onChangeText             | Events for text                       | (text: string) => void                                                                                        | no       | Android iOS | yes               |
| onChangeFormattedText    | Events for formatted text             | (text: string) => void                                                                                        | no       | Android iOS | yes               |
| containerStyle           | Style of the component                | `StyleProp<ViewStyle>`                                                                                        | no       | Android iOS | yes               |
| textContainerStyle       | The style of the component text       | `StyleProp<ViewStyle>`                                                                                        | no       | Android iOS | yes               |
| renderDropdownImage      | render Drop down Image                | `JSX.Element`                                                                                                 | no       | Android iOS | yes               |
| textInputProps           | style of the input                    | [TextInputProps](https://reactnative.dev/docs/textinput)                                                      | no       | Android iOS | yes               |
| textInputStyle           | style of the inputText                | `StyleProp<TextStyle>`                                                                                        | no       | Android iOS | yes               |
| codeTextStyle            | style of the code text                | `StyleProp<TextStyle>`                                                                                        | no       | Android iOS | yes               |
| flagButtonStyle          | the style of the flag Button          | `StyleProp<ViewStyle>`                                                                                        | no       | Android iOS | yes               |
| countryPickerButtonStyle | the style of the countryPicker button | `StyleProp<ViewStyle>`                                                                                        | no       | Android iOS | yes               |
| layout                   | the component of layout               | "first" or "second"                                                                                           | no       | Android iOS | yes               |
| filterProps              | filter the props                      | CountryFilterProps                                                                                            | no       | Android iOS | yes               |
| countryPickerProps       | the countryPicker Props               | any                                                                                                           | no       | Android iOS | yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                  | Description                                 | Type                                                                                                                | Required | Platform    | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| getCountryCode                        | get the country code                        | () => [CountryCode](https://github.com/xcarpentier/react-native-country-picker-modal/blob/master/src/types.ts#L252) | no       | Android iOS | yes               |
| getCallingCode                        | get the call code                           | () => string                                                                                                        | no       | Android iOS | yes               |
| getNumberAfterPossiblyEliminatingZero | get the initial value and generated number. | () => {number: string , formattedNumber: string }                                                                   | no       | Android iOS | yes               |
| isValidNumber                         | Verifying whether a number is valid         | (number: string)=>boolean                                                                                           | no       | Android iOS | yes               |

## 遗留问题

## 其他

- 在 HarmonyOS NEXT 上，withDarkTheme 只能让国家选择器的主题色更改，无法更改键盘的颜色。因为 iOS 提供给开发者设置键盘深浅模式的选项，一旦开发者设置错误会导致输入法键盘和应用出现颜色错层，在 HarmonyOS NEXT 上输入法键盘做了自适应应用颜色模式的能力，故不需要再提供该属性。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/garganurag893/react-native-phone-number-input/blob/master/LICENSE.md) ，请自由地享受和参与开源。
