> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>@react-navigation/native-stack</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/native-stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/native-stack/LICENSE">
         <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/native-stack)

## 安装与使用

> [!TIP] native-stack和elements的tgz包都在react-navigation Releases。

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases)、[@react-native-oh-library/react-native-safe-area-context Releases](https://github.com/react-native-oh-library/react-native-safe-area-context/releases)，并下载native-stack、elements、react-native-safe-area-context适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为tgz包的路径

<!-- tabs:start -->

### **npm**

```bash
npm install react-native-screens@3.31.1
npm install @react-native-oh-tpl/native-stack@file:#
npm install @react-native-oh-tpl/elements@file:#
npm install @react-native-oh-tpl/react-native-safe-area-context@file:#
```

### **yarn**

```bash
yarn install react-native-screens@3.31.1
yarn install @react-native-oh-tpl/native-stack@file:#
yarn install @react-native-oh-tpl/elements@file:#
yarn install @react-native-oh-tpl/react-native-safe-area-context
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

<!-- {% raw %} -->
```tsx
import * as React from 'react';
import { Button, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createNativeStackNavigator } from '@react-navigation/native-stack';
import { enableScreens } from "react-native-screens";
enableScreens(false);

function HomeScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Profile"
        onPress={() => navigation.navigate('Profile')}
      />
    </View>
  );
}

function ProfileScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Notifications"
        onPress={() => navigation.navigate('Notifications')}
      />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

function NotificationsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button
        title="Go to Settings"
        onPress={() => navigation.navigate('Settings')}
      />
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

function SettingsScreen({ navigation }) {
  return (
    <View style={{ flex: 1, alignItems: 'center', justifyContent: 'center' }}>
      <Button title="Go back" onPress={() => navigation.goBack()} />
    </View>
  );
}

const Stack = createNativeStackNavigator();

function MyStack() {
  return (
    <Stack.Navigator
      initialRouteName="Home"
      screenOptions={{
        headerTintColor: 'white',
        headerStyle: { backgroundColor: 'tomato' },
      }}
    >
      <Stack.Screen name="Home" component={HomeScreen} />
      <Stack.Screen name="Notifications" component={NotificationsScreen} />
      <Stack.Screen name="Profile" component={ProfileScreen} />
      <Stack.Screen name="Settings" component={SettingsScreen} />
    </Stack.Navigator>
  );
}

export default function App() {
  return (
    <NavigationContainer>
      <MyStack />
    </NavigationContainer>
  );
}

```
<!-- {% endraw %} -->

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-safe-area-context的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-safe-area-context 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-safe-area-context.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases)

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description     | Type     | Required | Platform | HarmonyOS Support |
| -------------------------- | --------------- | -------- | -------- | -------- | ----------------- |
| createNativeStackNavigator | 创建 Stack 组件 | function | no       | All      | yes               |

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/native-stack 的文档介绍](https://reactnavigation.org/docs/native-stack-navigator)

**Stack.Navigator：**

| Name             | Description                        | Type   | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------- | ------ | -------- | -------- | ----------------- |
| initialRouteName | 首次加载导航器时要呈现的路由的名称 | string | no       | All      | yes               |
| screenOptions    | 用于导航器中屏幕的默认选项。       | object | no       | All      | yes               |

**ScreenOptions:**

| Name            | Description          | Type   | Required | Platform | HarmonyOS Support |
| --------------- | -------------------- | ------ | -------- | -------- | ----------------- |
| headerStyle     | 标头的样式对象       | object | no       | All      | yes               |
| headerTitle     | 标头标题             | string | no       | All      | yes               |
| headerTintColor | 后退按钮和标题的颜色 | object | no       | All      | yes               |

**Stack.Screen：**

| Name      | Description                          | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------ | -------- | -------- | -------- | ----------------- |
| name      | 屏幕组件的唯一标识                   | string   | no       | All      | yes               |
| component | 用于定义堆栈导航器中的屏幕内容和行为 | function | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/native-stack/LICENSE) ，请自由地享受和参与开源。
