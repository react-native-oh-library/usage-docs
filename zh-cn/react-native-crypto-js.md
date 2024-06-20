<!-- {% raw %} -->
> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-crypto-js</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/imchintan/react-native-crypto-js/blob/master/README.md">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/imchintan/react-native-crypto-js/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/imchintan/react-native-crypto-js)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-crypto-js@1.0.0
```

#### **yarn**

```bash
yarn add react-native-crypto-js@1.0.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from 'react';
import {
  ScrollView,
  Text,
  View,
  TextInput,
  Button,
  Alert
} from 'react-native';

import CryptoJS from "react-native-crypto-js";
//import CryptoJS from "rn-crypto-js";

//使用AES加密字符串
function encrypt_str(text: string) {
  let ciphertext = CryptoJS.AES.encrypt(text, 'secret key 123').toString();
  Alert.alert('加密后：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;
}

//使用AES解密字符串
function decrypt_str(text: string) {
  let bytes = CryptoJS.AES.decrypt(text, 'secret key 123');
  let originalText = bytes.toString(CryptoJS.enc.Utf8);
  Alert.alert('解密后：', originalText, [{ text: 'OK' }]);
}

//使用AES加密对象
function encrypt_obj(text: string) {
  let ciphertext = CryptoJS.AES.encrypt(JSON.stringify(text), 'secret key 123').toString();
  Alert.alert('加密后：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;
}

//使用AES解密对象
function decrypt_obj(text: string) {
  let bytes = CryptoJS.AES.decrypt(text, 'secret key 123');
  let originalText = JSON.parse(bytes.toString(CryptoJS.enc.Utf8));
  Alert.alert('解密后：', originalText, [{ text: 'OK' }]);
  return originalText;
}

//使用MD5加密字符串
function MD5_encrypt_str(text: string) {
  let ciphertext = CryptoJS.MD5(text).toString();
  Alert.alert('加密后：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;

}

//使用HmacMD5加密字符串
function HMD5_encrypt_str(text: string) {
  let ciphertext = CryptoJS.HmacMD5(text, 'secret key 123').toString();
  Alert.alert('加密后：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;

}

export const ReactNativeCryptoJsExample = () => {
  const [cryptText, setCryptText] = useState('test 123');
  const [cryptText1, setCryptText1] = useState('test123');
  const [cryptText2, setCryptText2] = useState('test123');
  const [decryptText, setDecryptText] = useState('');
  const [cryptObj, setCryptObj] = useState('[{id: 1}, {id: 2}]');
  const [decryptObj, setDecryptObj] = useState('');
  return (
    <ScrollView style={{ backgroundColor: 'yellow' }} bounces>
      <Text> 测试使用AES算法加解密字符串</Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="请输入内容!" onChangeText={(cryptText: React.SetStateAction<string>) => setCryptText(cryptText)} defaultValue={cryptText} />
      </View>
      <Button onPress={() => { setDecryptText(encrypt_str(cryptText)) }} title="加密字符串" />

      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="请输入内容!" onChangeText={(decryptText: React.SetStateAction<string>) => setDecryptText(decryptText)} defaultValue={decryptText} />
      </View>
      <Button onPress={() => { decrypt_str(decryptText) }} title="解密字符串" />
      <Text> 测试使用AES算法加解密对象</Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="请输入内容!" onChangeText={(cryptObj: React.SetStateAction<string>) => setCryptObj(cryptObj)} defaultValue={cryptObj} />
      </View>
      <Button onPress={() => { setDecryptObj(encrypt_obj(cryptObj)) }} title="加密对象" />

      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="请输入内容!" onChangeText={(decryptObj: React.SetStateAction<string>) => setDecryptObj(decryptObj)} defaultValue={decryptObj} />
      </View>
      <Button onPress={() => { decrypt_obj(decryptObj) }} title="解密对象" />
      <Text> 测试使用MD5算法加密字符串</Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="请输入内容!" onChangeText={(cryptText1: React.SetStateAction<string>) => setCryptText1(cryptText1)} defaultValue={cryptText1} />
      </View>
      <Button onPress={() => { MD5_encrypt_str(cryptText1) }} title="加密" />
      <Text> 测试使用HmacMD5算法加密字符串</Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="请输入内容!" onChangeText={(cryptText2: React.SetStateAction<string>) => setCryptText2(cryptText2)} defaultValue={cryptText2} />
      </View>
      <Button onPress={() => { HMD5_encrypt_str(cryptText2) }} title="加密" />
    </ScrollView>
  );
};
```

## 约束与限制

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [react-native-crypto-js 源库地址](https://github.com/imchintan/react-native-crypto-js/blob/master/README.md)

| 名称                 | 描述            | 参数类型 | 是否必填 | Platform | HarmonyOS Support |
| -------------------- | --------------- | -------- | -------- | -------- | ----------------- |
| CryptoJS.AES.encrypt | AES算法加密     | string   | yes      | All      | yes               |
| CryptoJS.AES.decrypt | AES算法解密     | string   | yes      | All      | yes               |
| CryptoJS.MD5         | MD5算法加密     | string   | yes      | All      | yes               |
| CryptoJS.HmacMD5     | HmacMD5算法加密 | string   | yes      | no       | no                |

## 遗留问题

原库使用CryptoJS.HmacMD5会报错"cannot readproperty ‘init’ of underfined"，如果需要使用HmacMD5算法可以安装使用rn-crypto-js库，用法与react-native-crypto-js相同。源库此问题 issues:[issue#4](https://github.com/imchintan/react-native-crypto-js/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/imchintan/react-native-crypto-js/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->