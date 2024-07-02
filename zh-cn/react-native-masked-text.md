<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-masked-text</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bhrott/react-native-masked-text">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bhrott/react-native-masked-text/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/bhrott/react-native-masked-text)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-masked-text@1.13.0
```

#### **yarn**

```bash
yarn add react-native-masked-text@1.13.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from "react";
import { View, StyleSheet } from "react-native";
import { TextInputMask } from "react-native-masked-text";

export const MaskedTextCPF = () => {
  const [mask, setMask] = useState({
    cpf: "",
  });
  return (
    <View style={styles.container}>
      <TextInputMask
        type={"cpf"}
        value={mask.cpf}
        onChangeText={(text) => {
          setMask({
            cpf: text,
          });
        }}
        style={styles.textInputStype}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    width: "100%",
  },
  textInputStype: {
    height: 50,
    width: "100%",
    borderColor: "gray",
    borderWidth: 1,
    backgroundColor: "white",
  },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> 详情见 [react-native-masked-text](https://github.com/bhrott/react-native-masked-text)

| Name                        | Description                                               | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------- | --------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| type                        | the type of the mask                                      | string   | YES      | Android IOS | YES               |
| options                     | set mask type                                             | object   | NO       | Android IOS | YES               |
| onChangeText                | set mask                                                  | function | NO       | Android IOS | YES               |
| checkText                   | Blocking user to add character                            | function | NO       | Android IOS | YES               |
| refInput                    | add the ref to a local var                                | function | NO       | Android IOS | YES               |
| customTextInput             | the custom text input component                           | any      | NO       | Android IOS | YES               |
| customTextInputProps        | the props to be passed to the custom text input           | object   | NO       | Android IOS | YES               |
| includeRawValueInChangeText | provide the masked and the raw text in every text change. | boolean  | NO       | Android IOS | YES               |

#### 目前 type 支持

| Name         | Description                                                                                                                          | required | Type   | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------------------------------------------------------------------------------ | -------- | ------ | ----------- | ----------------- |
| cel-phone    | 1.(99) 9999-9999 or (99) 99999-9999 2. +999 999 999 999                                                                              | YES      | string | Android IOS | YES               |
| cpf          | Mask: 999.999.999-99                                                                                                                 | YES      | string | Android IOS | YES               |
| cnpj         | Mask: 99.999.999/9999-99                                                                                                             | YES      | string | Android IOS | YES               |
| credit-card  | 1.9999 9999 9999 9999 or 9999 \***\* \*\*** 9999 2.9999 999999 99999 or 9999 **\*\*** 99999 3.9999 999999 9999 or 9999 **\*\*** 9999 | YES      | string | Android IOS | YES               |
| custom       | Mask: defined by pattern                                                                                                             | YES      | string | Android IOS | YES               |
| datetime     | 1. DD/MM/YYYY HH:mm:ss 2. DD/MM/YYYY 3.MM/DD/YYYY 4.YYYY/MM/DD 5.HH:mm:ss 6.HH:mm 7.HH                                               | YES      | string | Android IOS | YES               |
| money        | Mask: R$999,99 (fully customizable)                                                                                                  | YES      | string | Android IOS | YES               |
| only-numbers | accept only numbers                                                                                                                  | YES      | string | Android IOS | YES               |
| zip-code     | Mask: 99999-999                                                                                                                      | YES      | string | Android IOS | YES               |

##### 不同 type 支持的 options

- Money type:

| name       | type   | required | default | description                 | Platform    | HarmonyOS Support |
| ---------- | ------ | -------- | ------- | --------------------------- | ----------- | ----------------- |
| precision  | number | no       | `2`     | The number of cents to show | Android IOS | YES               |
| separator  | string | no       | `,`     | The cents separator         | Android IOS | YES               |
| delimiter  | string | no       | `.`     | The thousand separator      | Android IOS | YES               |
| unit       | string | no       | `R$`    | The prefix text             | Android IOS | YES               |
| suffixUnit | string | no       | `''`    | The sufix text              | Android IOS | YES               |

- Phone type：

| name     | type    | required | default    | description                                                      | Platform    | HarmonyOS Support |
| -------- | ------- | -------- | ---------- | ---------------------------------------------------------------- | ----------- | ----------------- |
| maskType | string  | no       | `maskType` | the type of the mask to use. Available: `BRL` or `INTERNATIONAL` | Android IOS | YES               |
| withDDD  | boolean | no       | `true`     | if the mask type is `BRL`, include the DDD                       | Android IOS | YES               |
| dddMask  | string  | no       | `(99) `    | if the mask type is `BRL`, the DDD mask                          | Android IOS | YES               |

- Datetime type：

| name   | type   | required | default | description                     | Platform    | HarmonyOS Support |
| ------ | ------ | -------- | ------- | ------------------------------- | ----------- | ----------------- |
| format | string | **YES**  |         | The date format to be validated | Android IOS | YES               |

- redit card type：

| name       | type    | required | default              | description                                                                          | Platform    | HarmonyOS Support |
| ---------- | ------- | -------- | -------------------- | ------------------------------------------------------------------------------------ | ----------- | ----------------- |
| obfuscated | boolean | no       | `false`              | if the mask should be obfuscated or not                                              | Android IOS | YES               |
| issuer     | string  | no       | `visa-or-mastercard` | the type of the card mask. The options are: `visa-or-mastercard`, `amex` or `diners` | Android IOS | YES               |

- Custom type：

| name        | type                          | required | default                                                               | description                                           | Platform    | HarmonyOS Support |
| ----------- | ----------------------------- | -------- | --------------------------------------------------------------------- | ----------------------------------------------------- | ----------- | ----------------- |
| mask        | string                        | **YES**  |                                                                       | The mask pattern                                      | Android IOS | YES               |
| validator   | function                      | no       | function that returns `true`                                          | the function that's validate the value in the mask    | Android IOS | YES               |
| getRawValue | function                      | no       | return current value                                                  | function to parsed value (like unmasked or converted) | Android IOS | YES               |
| translation | object (map{string,function}) | no       | `9 - digit`, `A - alpha`, `S - alphanumeric`, `* - all, except space` | The translator to use in the pattern                  | Android IOS | YES               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> 详情见 [react-native-masked-text](https://github.com/bhrott/react-native-masked-text)

##### MaskService

| Name       | Description                               | Type     | Required | Platform    | HarmonyOS Support |
| ---------- | ----------------------------------------- | -------- | -------- | ----------- | ----------------- |
| toMask     | mask a value                              | function | NO       | Android IOS | YES               |
| toRawValue | get the raw value of a masked value       | function | NO       | Android IOS | YES               |
| isValid    | validate if the mask and the valueg match | function | NO       | Android IOS | YES               |
| getMask    | get the mask used to mask the value       | function | NO       | Android IOS | YES               |

- static toMask(type, value, settings): mask a value
  - `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
  - `value` (String, required): the value to be masked
  - `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter
- static toRawValue(type, maskedValue, settings): get the raw value of a masked value.
  - `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
  - `maskedValue` (String, required): the masked value to be converted in raw value
  - `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter
- static isValid(type, value, settings): validate if the mask and the value match.
  - `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
  - `value` (String, required): the value to be masked
  - `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter
- static getMask(type, value, settings): get the mask used to mask the value
  - `type` (String, required): the type of the mask (`cpf`, `datetime`, etc...)
  - `value` (String, required): the value to be masked
  - `settings` (Object, optional): if the mask type accepts options, pass it in the settings parameter

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License](https://github.com/bhrott/react-native-masked-text/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
