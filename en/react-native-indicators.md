> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-indicators</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-indicators">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-indicators/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-BSD-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/n4kz/react-native-indicators)

## 安装与使用

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-indicators@0.17.0
```

#### **yarn**

```bash
yarn add react-native-indicators@0.17.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from 'react';
import { AppRegistry, StatusBar, View, Platform, Dimensions } from 'react-native';
import {
  BallIndicator,
  BarIndicator,
  DotIndicator,
  MaterialIndicator,
  PacmanIndicator,
  PulseIndicator,
  SkypeIndicator,
  UIActivityIndicator,
  WaveIndicator,
} from 'react-native-indicators';
const { width, height } = Dimensions.get('window');


 export class IndicatorsTestExample extends Component {
    render() {
      return (
        <View style={styles.container}>
          <View style={styles.row}>
            <View style={styles.flex}>
              <BallIndicator color='white' animationDuration={800} />
            </View>

            <View style={styles.flex}>
              <PulseIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <SkypeIndicator color='white' />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <WaveIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <WaveIndicator color='white' waveMode='outline' />
            </View>

            <View style={styles.flex}>
              <WaveIndicator color='white' count={2} waveFactor={0.1} />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <UIActivityIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <MaterialIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <PacmanIndicator color='white' />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <BarIndicator color='white' count={5} />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <DotIndicator
                count={3}
                color='white'
                animationDuration={800}
              />
            </View>

            <View style={styles.flex}>
              <DotIndicator
                style={styles.reverse}
                count={3}
                color='white'
                animationDuration={800}
              />
            </View>
          </View>
        </View>
      );
    }
  }


const styles = {
  container: {
  height: height-100,
    backgroundColor: '#01579B',
    padding: 20,
  },

  row: {
    flex: 1,
    flexDirection: 'row',
  },

  reverse: {
    transform: [{
      rotate: '180deg',
    }],
  },

  flex: {
    flex: 1,
  },
};
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


### Common properties

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| animationEasing  | Animation easing function	   | Function  | NO | ALL      | YES |
| animationDuration  | 	Animation duration in ms     | Number | NO | ALL      | YES |
| animating  | 	Animation toggle    | Boolean | NO | ALL      | YES |
| interaction  | Animation is interaction  | Boolean | NO | ALL      | YES |
| hidesWhenStopped  | Hide when not animating   | Boolean | NO | ALL      | YES |

### BallIndicator

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |


### BarIndicator 

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### DotIndicator  

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### MaterialIndicator   

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| trackWidth  | Indicator track width    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### PacmanIndicator    

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### PulseIndicator     

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### SkypeIndicator    

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |
| minScale  | Minimum component scale    | Number  | NO | ALL      | YES |
| maxScale  | Maximum component scale    | Number  | NO | ALL      | YES |

### UIActivityIndicator    

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### WaveIndicator     

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |
| waveFactor  | Wave base number   | Number  | NO | ALL      | YES |
| waveMode  | Wave appearance    | String  | NO | ALL      | YES |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The BSD License (BSD)](https://github.com/n4kz/react-native-indicators/blob/master/license.txt) ，请自由地享受和参与开源。