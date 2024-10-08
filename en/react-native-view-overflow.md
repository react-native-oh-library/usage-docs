<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-overflow</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/entria/react-native-view-overflow">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/entria/react-native-view-overflow/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-view-overflow)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-view-overflow Releases](https://github.com/react-native-oh-library/react-native-view-overflow/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-view-overflow@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-view-overflow@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {View} from 'react-native';

import ViewOverflow from 'react-native-view-overflow';

export function ViewOverflowDemo() {
  return (
  <View style={{height: '100%', backgroundColor: 'white', padding: 10}}>

    <View style={{width: 200, height: 100, backgroundColor: 'red'}}>
      <ViewOverflow style={{width: 100, height: 50, backgroundColor: 'blue'}}>
          <ViewOverflow style={{width: 50, height: 25, backgroundColor: 'skyblue', left: 60, top: 30}}>
            <View style={{backgroundColor: 'yellow', height: '100%', left: 20, top: 10}} />
          </ViewOverflow>
      </ViewOverflow>
    </View>

  </View>
  );
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[react-native-view-overflow Releases](https://github.com/react-native-oh-library/react-native-view-overflow/releases)

## 属性
[!tip] 该库作为容器组件使用同View组件，可以让子控件溢出到父布局之外展示的效果；使用公共属性即可，不涉及私有属性及api方法。

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/entria/react-native-view-overflow/blob/master/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->
