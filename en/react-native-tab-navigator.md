<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-tab-navigator</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ptomasroos/react-native-tab-navigator">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ptomasroos/react-native-tab-navigator/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-tab-navigator)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-tab-navigator Releases](https://github.com/react-native-oh-library/react-native-tab-navigator/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-tab-navigator@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-tab-navigator@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React, { useState } from "react";
import { View, StyleSheet, Text, Image } from "react-native";
import TabNavigator from "react-native-tab-navigator";

const HOME_IMAGE = [
  require("../assets/tab-navigator/home_unselected.svg"),
  require("../assets/tab-navigator/home_selected.svg"),
];
const PROFILE_IMAGE = [
  require("../assets/tab-navigator/profile_unselected.svg"),
  require("../assets/tab-navigator/profile_selected.svg"),
];

const App = () => {
  const [selectedTab, setSelectedTab] = useState("home");
  return (
    <View style={styles.container}>
      <TabNavigator style={styles.tabContainer}>
        <TabNavigator.Item
          selected={selectedTab === "home"}
          title="Home"
          selectedTitleStyle={{ color: "#3496f0" }}
          renderIcon={() => (
            <Image source={HOME_IMAGE[0]} style={styles.iconSize} />
          )}
          renderSelectedIcon={() => (
            <Image source={HOME_IMAGE[1]} style={styles.iconSize} />
          )}
          onPress={() => setSelectedTab("home")}
        >
          <Home />
        </TabNavigator.Item>
        <TabNavigator.Item
          selected={selectedTab === "profile"}
          title="Profile"
          selectedTitleStyle={{ color: "#3496f0" }}
          renderIcon={() => (
            <Image source={PROFILE_IMAGE[0]} style={styles.iconSize} />
          )}
          renderSelectedIcon={() => (
            <Image source={PROFILE_IMAGE[1]} style={styles.iconSize} />
          )}
          onPress={() => setSelectedTab("profile")}
        >
          <Profile />
        </TabNavigator.Item>
      </TabNavigator>
    </View>
  );
};

function Home() {
  return (
    <View style={styles.tabContainer}>
      <Text style={styles.welcome}>Home</Text>
    </View>
  );
}

function Profile() {
  return (
    <View style={styles.tabContainer}>
      <Text style={styles.welcome}>Profile</Text>
    </View>
  );
}

export default App;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-tab-navigator Releases](https://github.com/react-native-oh-library/react-native-tab-navigator/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### TabNavigator props

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| sceneStyle        | define for rendered scene       | object (style) | No       | iOS/Android | Yes               |
| tabBarStyle       | define style for TabBar         | object (style) | No       | iOS/Android | Yes               |
| tabBarShadowStyle | define shadow style for tabBar  | object (style) | No       | iOS/Android | Yes               |
| hidesTabTouch     | disable onPress opacity for Tab | boolean        | No       | iOS/Android | Yes               |

### TabNavigator.Item props

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| renderIcon         | returns Item icon                                  | function         | No       | iOS/Android | Yes               |
| renderSelectedIcon | returns selected Item icon                         | function         | No       | iOS/Android | Yes               |
| badgeText          | text for Item badge                                | string or number | No       | iOS/Android | Yes               |
| renderBadge        | returns Item badge                                 | function         | No       | iOS/Android | Yes               |
| title              | Item title                                         | string           | No       | iOS/Android | Yes               |
| titleStyle         | styling for Item title                             | style            | No       | iOS/Android | Yes               |
| selectedTitleStyle | styling for selected Item title                    | style            | No       | iOS/Android | Yes               |
| tabStyle           | styling for tab                                    | style            | No       | iOS/Android | Yes               |
| selected           | return whether the item is selected                | boolean          | No       | iOS/Android | Yes               |
| onPress            | onPress method for Item                            | function         | No       | iOS/Android | Yes               |
| allowFontScaling   | allow font scaling for title                       | boolean          | No       | iOS/Android | Yes               |
| accessible         | indicates if this item is an accessibility element | boolean          | No       | iOS/Android | Yes               |
| accessibilityLabel | override text for screen readers                   | string           | No       | iOS/Android | Yes               |
| testID             | used to locate this item in end-to-end-tests       | string           | No       | iOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ptomasroos/react-native-tab-navigator/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
