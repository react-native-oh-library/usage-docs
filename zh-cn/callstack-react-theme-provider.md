<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@callstack/react-theme-provider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-theme-provider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-theme-provider/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/callstack/react-theme-provider)

## 安装与使用

#### **npm**

```bash
npm install @callstack/react-theme-provider@3.0.9
```

#### **yarn**

```bash
yarn add @callstack/react-theme-provider@3.0.9
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {
  StyleSheet,
  Text,
  Button,
  View
} from 'react-native';

import { createTheming } from '@callstack/react-theme-provider';

const theme = {
  lightTheme: {
    background: '#ffffff',
    text: '#000000'
  },
  darkTheme: {
    background: '#000000',
    text: '#ffffff'
  },
};

const { ThemeProvider, useTheme } = createTheming(theme);

const RNThemeProvider = () => {
  const theme = useTheme();

  const [ptheme, setTheme] = React.useState(theme.lightTheme);

  const toggleTheme = () => {
    setTheme(ptheme => (ptheme === theme.lightTheme ? theme.darkTheme : theme.lightTheme));
  };

  const ThemedView = () => {
    return (
      <View style={[styles.container, { backgroundColor: ptheme.background }]}>
        <Text style={[styles.text, { color: ptheme.text }]}>Hello, Themed World!</Text>
      </View>
    );
  }
  return (
    <ThemeProvider theme={theme}>
      <ThemedView />
      <View style={styles.buttonContainer}>
        <Button title="Toggle Theme" onPress={toggleTheme} />
      </View>
    </ThemeProvider>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    fontSize: 20,
  },
  buttonContainer: {
    position: 'absolute',
    justifyContent: 'center',
    alignItems: 'center',
    bottom: 30,
    left: 0,
    right: 0,
  },
});

export default RNThemeProvider;
```

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.22;

## 组件

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ThemeProvider  | 接收一个主题对象作为属性，并将该主题提供给其子组件 | component | no | all      | yes |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| createTheming | 从库中导入以创建主题对象 | function  | yes | all      | yes |
| useTheme | 用于在函数组件中访问当前主题,它返回当前主题对象 | function | no | all      | yes |
| withTheme  | 用于将当前主题作为属性传递给包装组件 | function | yes | all      | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-theme-provider/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->