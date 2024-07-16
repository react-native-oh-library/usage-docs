<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-communications</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/davebeehively/react-native-communications">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/davebeehively/react-native-communications/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/davebeehively/react-native-communications)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-communications@2.2.1
```

#### **yarn**

```bash
yarn add react-native-communications@2.2.1
```

<!-- tabs:end -->

>[!WARNING] 使用时 import 的库名不变。

```js
var React = require('react-native');
var {
  StyleSheet,
  View,
  TouchableOpacity,
  Text
} = React;

import { phonecall, text, textWithoutEncoding, email, web } from 'react-native-communications';

const RNCommunications = () => {
  const handleButton1Press = () => {
    phonecall('0123456789', false)
  }
  const handleButton2Press = () => {
    email(['email@xxx.com'], null, null, 'My Subject', 'My body text')
  }
  const handleButton3Press = () => {
    text('0123456789')
  }
  const handleButton4Press = () => {
    web('https://www.baidu.com')
  }
  const handleButton5Press = () => {
    textWithoutEncoding('0123456789', "9999999")
  }

  return (
    <View style={styles.container}>
      <TouchableOpacity style={styles.button} onPress={handleButton1Press}>
        <Text>Make phonecall</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton2Press}>
        <Text>Send an email</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton3Press}>
        <Text>Send a text only phonenumber</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton4Press}>
        <Text>web to baidu</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton5Press}>
        <Text>Send a text with body</Text>
      </TouchableOpacity>
    </View>
  );
};

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: 'white',
    borderRadius: 5,
  }
});

export default RNCommunications;
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1.RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| phonecall  | 拨打电话         | function  | yes | All      | yes |
| email  | 发送电子邮件      | function  | yes | All      | no |
| text  | 发送文本消息          | function  | yes | All      | yes |
| textWithoutEncoding  | 发送文本消息，但是不进行编码处理       | function  | yes | All      | yes |
| web  | 打开指定的网页 URL         | function  | yes | All      | yes |

## 遗留问题

- [ ] HarmonyOS 侧没有邮箱应用，导致email方法无法打开发送邮件界面。
- [ ] text添加body之后，没法在短信界面拆分进短信输入栏，框架侧接口Linking.canOpenURL不支持。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/davebeehively/react-native-communications/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->