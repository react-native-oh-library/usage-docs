> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-responsive-fontsize</code> </h1>
</p>
<p align="center">
    <a href="https://https://github.com/heyman333/react-native-responsive-fontsize">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/heyman333/react-native-responsive-fontSize/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/heyman333/react-native-responsive-fontSize)

## 安装与使用
<!-- tabs:start -->
进入到工程目录并输入以下命令：

#### **npm**

```bash
$ npm install react-native-responsive-fontsize@0.5.1 --save
```

#### **yarn**

```bash
$ yarn add react-native-responsive-fontsize@0.5.1
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import { RFPercentage, RFValue } from "react-native-responsive-fontsize";
import { View, Text, StyleSheet } from 'react-native';

const styles = StyleSheet.create({
  welcome: {
    fontSize: RFValue(24, 580),
    textAlign: "center",
    margin: 10,
  },
  instructions: {
    textAlign: "center",
    margin: 10,
    fontSize: RFPercentage(5),
  },
});
const App = () => {
  return (
    <View style={{ height: '100%', width: '100%', backgroundColor: '#ffffff',marginTop:50}}>
      <View style={{ height: 200 }}>
        <Text>fontSize used RFValue(24, 580):</Text>
        <Text style={styles.welcome}>Hello World1</Text>
      </View>
      <View style={{ height: 200 }}>
        <Text>fontSize used RFPercentage(5):</Text>
        <Text style={styles.instructions}>Hello World2</Text>
      </View>
    </View>
  )
}

export default App;
```
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.27; SDK：HarmonyOS-NEXT-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 静态方法
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name         | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------ | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| RFPercentage | The font size is calculated as a percentage of the height(`width` in landscape mode) of the device. | function | no       | Android/iOS | yes               |
| RFValue      | The font size is calculated based on standardScreenHeight and passed value | function | no       | Android/iOS | yes               |

**RFPercentage参数**

| Name    | Description | Type   | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------ | -------- | ----------- | ----------------- |
| percent | font size   | number | yes      | Android/iOS | yes               |

**RFValue参数**

| Name                 | Description            | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------- | ------ | -------- | ----------- | ----------------- |
| value                | font size              | number | yes      | Android/iOS | yes               |
| standardScreenHeight | standard screen height | number | no       | Android/iOS | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/heyman333/react-native-responsive-fontSize/blob/master/LICENSE) ，请自由地享受和参与开源。
