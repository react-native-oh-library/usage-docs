> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-easy-grid</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/GeekyAnts/react-native-easy-grid">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/GeekyAnts/react-native-easy-grid/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache License 2.0-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/GeekyAnts/react-native-easy-grid)


## 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install react-native-easy-grid@0.2.2
```

#### **yarn**

```bash
yarn add react-native-easy-grid@0.2.2 
```

<!-- tabs:end -->


下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。


```js

import React from "react";
import { Text } from 'react-native';
import { Col, Row, Grid } from "react-native-easy-grid";

const App = () => {
 
  return (
    <Grid>
      <Col style={{ backgroundColor: '#9400D3' }}>
        <Row size={1} style={{ backgroundColor: '#FFB6C1' }}></Row>
        <Row size={2} style={{ backgroundColor: '#9400D3' }}></Row>
      </Col>
      <Col size={2} style={{ backgroundColor: '#FF4500' }}></Col>
      <Col size={3}>
        <Row size={1} style={{ backgroundColor: '#FFB6C1' }}></Row>
        <Row size={2} style={{ backgroundColor: '#9400D3' }}></Row>
        <Row size={1} style={{ backgroundColor: '#008000' }}></Row>
      </Col>
    </Grid>
  )
      
};

export default App;
  
```
## 约束与限制

##### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;


## 属性

Grid、Row、Col组件接收所有 [React Native View](https://reactnative.dev/docs/view#props)组件的Props

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**RowProps和ColProps的公共属性：**

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|   size  | 布局占比   | number   | no | iOS,Android      | yes |
|   onPress：() => void  |  点击事件       | function     | no | iOS,Android      | yes |


## 遗留问题

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/GeekyAnts/react-native-easy-grid/blob/master/LICENSE) ，请自由地享受和参与开源。

