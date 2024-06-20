> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-md5</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/kmend/react-native-md5">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kmend/react-native-md5/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/kmend/react-native-md5)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-md5@1.0.0 --save
```

#### **yarn**

```bash
yarn add react-native-md5@1.0.0 
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import {ScrollView, StyleSheet,View,Text,TextInput,TouchableHighlight} from 'react-native';
import React,{ useState } from 'react';
import md5 from "react-native-md5";

const styles = StyleSheet.create({
    container: { flex: 1, backgroundColor: '#F5FCFF' },
    content: { paddingTop: 40, alignItems: 'center' },
    fieldContainer: { flexDirection: 'row', alignItems: 'center', marginBottom: 10 },
    button: { borderRadius: 3, paddingVertical: 5, paddingHorizontal: 10, backgroundColor: 'green', marginBottom: 10 },
    buttonText: { color: '#fff', textAlign: 'center' },
});
export function md5TestExample() {
	let data = '';
    const [hMd5Text, setHMd5Text] = useState("");
    const [bMd5Text, setBMd5Text] = useState("");
    const [sMd5Text, setSMd5Text] = useState("");
    const [hmatch, setHmatch] = useState("");
    const [bmatch, setBmatch] = useState("");
    const [smatch, setSmatch] = useState("");

    return(
        <ScrollView style={styles.container} contentContainerStyle={styles.content}>
            <Text>{}</Text>
            <View style={styles.fieldContainer}>
                <TextInput placeholder = "输入加密字符串" 
                        onChangeText={ value => { data = value; setHMd5Text(md5.hex_md5(value)); setBMd5Text(md5.b64_md5(value)); setSMd5Text(md5.str_md5(value)); }}>
                </TextInput>
            </View>
            <View style={styles.fieldContainer}>
                <Text>.........................</Text>
            </View>
            <View style={styles.fieldContainer}>
                <TextInput placeholder = "输入HMAC密匙"
                onChangeText={
                    value => { 
                        setHmatch(md5.hex_hmac_md5(data,value)); setBmatch(md5.b64_hmac_md5(data,value)); setSmatch(md5.str_hmac_md5(data,value)); 
                    }
                } 
                ></TextInput>
            </View>
            
            <View style={styles.fieldContainer}><Text>16位:{hMd5Text} </Text></View>
            <View style={styles.fieldContainer}><Text>base-64:{bMd5Text} </Text></View>
            <View style={styles.fieldContainer}> <Text>字符串:{sMd5Text} </Text></View>
            
            <View style={styles.fieldContainer}><Text>HMAC-MD5 16位:{hmatch} </Text></View>
            <View style={styles.fieldContainer}><Text>HMAC-MD5 base-64:{bmatch} </Text></View>
            <View style={styles.fieldContainer}> <Text>HMAC-MD5 字符串:{smatch} </Text></View>
        </ScrollView>
    );
}
```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## API

> [!tip] "Platform"列表示该接口在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| hex_md5    |  返回格式为16进制字符串的md5值   | function | no       | All      | yes               |
| b64_md5           |   返回格式为base64的md5值  | function | no       | All      | yes               |
| str_md5 |   返回格式为字符串的md5值    | function | no       | All      | yes               |
| hex_hmac_md5        |   返回格式为16进制字符串的HMAC-md5值   | function | no       | All      | yes               |
| b64_hmac_md5        |   返回格式为base64的HMAC-md5值   | function | no       | All      | yes               |
| str_hmac_md5        |    返回格式为字符串的HMAC-md5值  | function | no       | All      | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/kmend/react-native-md5/blob/master/README.md) ，请自由地享受和参与开源。
