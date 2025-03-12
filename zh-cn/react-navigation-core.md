> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/core</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/core">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/core/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-navigation/react-navigation/tree/6.x/packages/core)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/core@6.4.16
```

#### **yarn**

```bash
yarn add @react-navigation/core@6.4.16
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Button, View, Text } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';
import { useNavigation } from '@react-navigation/core';

function MyBackButton() {
    const navigation = useNavigation();

    return (
        <Button
            title="Back"
            onPress={() => {
                navigation.goBack();
            }}
        />
    );
}

function HomeScreen({ navigation: { navigate } }) {
    return (
        <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
            <Text>This is the home screen of the app</Text>
            <Button title="Go to Profile" onPress={() => navigate('Profile')} />
        </View>
    );
}

function ProfileScreen() {
    return (
        <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
            <Text>Profile Screen</Text>
            <MyBackButton />
        </View>
    );
}

const Stack = createStackNavigator();

function App() {
    return (
        <NavigationContainer>
            <Stack.Navigator initialRouteName="Home">
                <Stack.Screen name="Home" component={HomeScreen} />
                <Stack.Screen name="Profile" component={ProfileScreen} />
            </Stack.Navigator>
        </NavigationContainer>
    );
}

export default App;

```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过: 

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下方法已验证，更多使用详情请查看 [react-navigation 的文档介绍](https://reactnavigation.org/docs/getting-started/)

| Name                 | Description                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| useNavigationBuilder | hook to build custom navigators                                                                                     | function | no       | all      | yes               |
| useNavigation        | useNavigation is a hook which gives access to navigation object                                                     | function | no       | all      | yes               |
| useNavigationState   | useNavigationState is a hook which gives access to the navigation state of the navigator which contains the screen. | function | no       | all      | yes               |
| useRoute             | useRoute is a hook which gives access to route object.                                                              | function | no       | all      | yes               |
| useFocusEffect       | hook to run side-effects when a screen is focused                                                                   | function | no       | all      | yes               |
| useIsFocused         | the current focus state of the screen                                                                               | function | no       | all      | yes               |


## 遗留问题

## 其他

示例代码依赖以下三方库，请查看对应文档：
+ [@react-navigation/stack](/zh-cn/react-navigation-stack.md)
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/core/LICENSE) ，请自由地享受和参与开源。