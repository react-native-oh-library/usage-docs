> 模板版本：v0.2.2
<p align="center">
  <h1 align="center"> <code>@react-navigation/native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-navigation/react-navigation/tree/6.x/packages/native)


## 安装与使用

进入到工程目录并输入以下命令：
<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/native@6.1.17
```
#### **yarn**

```bash
yarn add @react-navigation/native@6.1.17
```


<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
```js
import * as React from 'react';
import { Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

const Tab = createBottomTabNavigator();

function HomeScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home screen</Text>
        </View>
    );
}

function DetailsScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Details!</Text>
        </View>
    );
}

export default function App() {
    return (
        <NavigationContainer>
            <Tab.Navigator>
                <Tab.Screen name="Home" component={HomeScreen} />
                <Tab.Screen name="Details" component={DetailsScreen} />
            </Tab.Navigator>
        </NavigationContainer>
    );
}

export {App}
```

## 约束与限制
### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.11; SDK: OpenHarmony(api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
4. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**NavigationContainer**：

| Name                      | Description                                                                                                          | Type     | Required | Platform | HarmonyOS Support |
| ------------------------- | -------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useNavigationContainerRef | A ref link to navigation                                                                                             | function | no       | all      | yes               |
| onStateChange             | Function that gets called every time navigation state changes. It receives the new navigation state as the argument. | function | no       | all      | yes               |
| onReady                   | Function which is called after the navigation container and all its children finish mounting for the first time.     | function | no       | all      | yes               |

**Hooks**
| Name           | Description                                                                                                                                                                                    | Type     | Required | Platform | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useScrollToTop | The expected native behavior of scrollable components is to respond to events from navigation that will scroll to top when tapping on the active tab as you would expect from native tab bars. | function | no       | all      | yes               |

## 遗留问题

## 其他

示例代码依赖以下三方库，请查看对应文档：
+ [@react-navigation/bottom-tabs](/zh-cn/react-navigation-bottom-tabs.md)
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/native/LICENSE) ，请自由地享受和参与开源。
