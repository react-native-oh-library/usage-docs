> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-confetti-cannon</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/VincentCATILLON/react-native-confetti-cannon">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20Web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/VincentCATILLON/react-native-confetti-cannon/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/VincentCATILLON/react-native-confetti-cannon)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-confetti-cannon@1.5.2
```

#### **yarn**

```bash
yarn add react-native-confetti-cannon@1.5.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

#### Using a Component

```js
import * as React from 'react';
import { StyleSheet, View, Text } from 'react-native';
import ConfettiCannon from 'react-native-confetti-cannon';

export default function ConfettiCannonExample() {

  return (
    <View style={{width: '100%', height: '100%'}}>
      <ConfettiCannon
        count={50}
        origin={{x: -10, y: -10}}
      />
    </View>
  )
}
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; OH SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio: 5.0.3.400; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| count  | items count to display        | number  |    yes    |  iOS,Android,Web  |         yes        |
| origin  | animation position origin       | {x: number, y: number}  |    yes    |  iOS,Android,Web  |         yes        |
| explosionSpeed  | explosion duration (ms) from origin to top        | number  |    no    |  iOS,Android,Web  |         yes        |
| fallSpeed  | fall duration (ms) from top to bottom        | number  |    no    |  iOS,Android,Web  |         yes        |
| fadeOut  | make the confettis disappear at the end        | boolean  |    no    |  iOS,Android,Web  |         yes        |
| colors  | give your own colors to the confettis        | string[]  |    no    |  iOS,Android,Web  |         yes        |
| autoStart  | auto start the animation        | boolean  |    no    |  iOS,Android,Web  |         yes        |
| autoStartDelay  | delay to wait before triggering animation        | number  |    no    |  iOS,Android,Web  |         yes        |


## 事件

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  onAnimationStart  |    callback triggered at animation start	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  onAnimationResume  |    callback triggered at animation resume	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  onAnimationStop  |    callback triggered at animation stop	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  onAnimationEnd  |    callback triggered at animation end	    | Function  |    no    |  iOS,Android,Web  |         yes        |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  start  |    start the animation programmatically	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  resume  |    resume the animation programmatically	    | Function  |    no    |  iOS,Android,Web  |         yes        |
|  stop  |    stop the animation programmatically	    | Function  |    no    |  iOS,Android,Web  |         yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/VincentCATILLON/react-native-confetti-cannon/blob/master/LICENSE) ，请自由地享受和参与开源。
