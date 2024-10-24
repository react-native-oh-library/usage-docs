> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/imchintan/react-native-crypto-js)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK：HarmonyOS-Next-DB1 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：5.0.0.61;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name             | Description | Type | Required | Platform | HarmonyOS Support |
| -------------------- | --------------- | -------- | -------- | -------- | ----------------- |
| CryptoJS.AES.encrypt | AES encryption | string   | yes      | Android、iOS      | yes               |
| CryptoJS.AES.decrypt | AES decryption | string   | yes      | Android、iOS      | yes               |
| CryptoJS.MD5         | MD5 encryption | string   | yes      | Android、iOS      | yes               |
| CryptoJS.HmacMD5     | HmacMD5 encryption | string   | yes      | no       | no                |

## Known Issues

- [ ] 原库使用CryptoJS.HmacMD5会报错"cannot readproperty ‘init’ of underfined"，如果需要使用HmacMD5算法可以安装使用rn-crypto-js库，用法与react-native-crypto-js相同: [issue#4](https://github.com/imchintan/react-native-crypto-js/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/imchintan/react-native-crypto-js/blob/master/LICENSE).
