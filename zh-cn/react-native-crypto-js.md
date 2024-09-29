> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-crypto-js</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/imchintan/react-native-crypto-js">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/imchintan/react-native-crypto-js/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/imchintan/react-native-crypto-js)

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

> [!WARNING] 使用时 import 的库名不变。

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

function encrypt_str(text: string) {
  let ciphertext = CryptoJS.AES.encrypt(text, 'secret key 123').toString();
  Alert.alert('encrypt：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;
}

function decrypt_str(text: string) {
  let bytes = CryptoJS.AES.decrypt(text, 'secret key 123');
  let originalText = bytes.toString(CryptoJS.enc.Utf8);
  Alert.alert('decrypt：', originalText, [{ text: 'OK' }]);
}

function encrypt_obj(text: string) {
  let ciphertext = CryptoJS.AES.encrypt(JSON.stringify(text), 'secret key 123').toString();
  Alert.alert('encrypt：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;
}

function decrypt_obj(text: string) {
  let bytes = CryptoJS.AES.decrypt(text, 'secret key 123');
  let originalText = JSON.parse(bytes.toString(CryptoJS.enc.Utf8));
  Alert.alert('decrypt：', originalText, [{ text: 'OK' }]);
  return originalText;
}

function MD5_encrypt_str(text: string) {
  let ciphertext = CryptoJS.MD5(text).toString();
  Alert.alert('encrypt：', ciphertext, [{ text: 'OK' }]);
  return ciphertext;
}

function HMD5_encrypt_str(text: string) {
  let ciphertext = CryptoJS.HmacMD5(text, 'secret key 123').toString();
  Alert.alert('encrypt：', ciphertext, [{ text: 'OK' }]);
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
      <Text> Encrypt and decrypt character strings using the AES algorithm. </Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="Please enter the content." onChangeText={(cryptText: React.SetStateAction<string>) => setCryptText(cryptText)} defaultValue={cryptText} />
      </View>
      <Button onPress={() => { setDecryptText(encrypt_str(cryptText)) }} title="encrypt strings" />
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="Please enter the content." onChangeText={(decryptText: React.SetStateAction<string>) => setDecryptText(decryptText)} defaultValue={decryptText} />
      </View>
      <Button onPress={() => { decrypt_str(decryptText) }} title="decrypt strings" />
      <Text>  Encrypt and decrypt object using the AES algorithm. </Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="Please enter the content." onChangeText={(cryptObj: React.SetStateAction<string>) => setCryptObj(cryptObj)} defaultValue={cryptObj} />
      </View>
      <Button onPress={() => { setDecryptObj(encrypt_obj(cryptObj)) }} title="encrypt object" />
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="Please enter the content." onChangeText={(decryptObj: React.SetStateAction<string>) => setDecryptObj(decryptObj)} defaultValue={decryptObj} />
      </View>
      <Button onPress={() => { decrypt_obj(decryptObj) }} title="decrypt object" />
      <Text> Encrypt and decrypt character strings using the MD5 algorithm. </Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="Please enter the content." onChangeText={(cryptText1: React.SetStateAction<string>) => setCryptText1(cryptText1)} defaultValue={cryptText1} />
      </View>
      <Button onPress={() => { MD5_encrypt_str(cryptText1) }} title="encrypt" />
      <Text>  Encrypt and decrypt character strings using the HmacMD5 algorithm. </Text>
      <View style={{ padding: 10 }}>
        <TextInput style={{ height: 40 }} placeholder="Please enter the content." onChangeText={(cryptText2: React.SetStateAction<string>) => setCryptText2(cryptText2)} defaultValue={cryptText2} />
      </View>
      <Button onPress={() => { HMD5_encrypt_str(cryptText2) }} title="encrypt" />
    </ScrollView>
  );
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK：HarmonyOS-Next-DB1 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：5.0.0.61;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description | Type | Required | Platform | HarmonyOS Support |
| -------------------- | --------------- | -------- | -------- | -------- | ----------------- |
| CryptoJS.AES.encrypt | AES encryption | string   | yes      | Android、iOS      | yes               |
| CryptoJS.AES.decrypt | AES decryption | string   | yes      | Android、iOS      | yes               |
| CryptoJS.MD5         | MD5 encryption | string   | yes      | Android、iOS      | yes               |
| CryptoJS.HmacMD5     | HmacMD5 encryption | string   | yes      | no       | no                |

## 遗留问题

- [ ] 原库使用CryptoJS.HmacMD5会报错"cannot readproperty ‘init’ of underfined"，如果需要使用HmacMD5算法可以安装使用rn-crypto-js库，用法与react-native-crypto-js相同: [issue#4](https://github.com/imchintan/react-native-crypto-js/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/imchintan/react-native-crypto-js/blob/master/LICENSE) ，请自由地享受和参与开源。