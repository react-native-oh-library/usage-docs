> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/material-bottom-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/material-bottom-tabs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/material-bottom-tabs/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-navigation/react-navigation/tree/6.x/packages/material-bottom-tabs)

## 安装与使用


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/material-bottom-tabs@6.2.28
```

#### **yarn**

```bash
yarn add @react-navigation/material-bottom-tabs@6.2.28
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { createMaterialBottomTabNavigator } from '@react-navigation/material-bottom-tabs';
import { View, Text } from 'react-native'
import { NavigationContainer } from '@react-navigation/native';
import * as React from 'react';

const Tab = createMaterialBottomTabNavigator();


function HomeScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home Screen</Text>
        </View>
    );
}


function SettingsScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Settings Screen</Text>
        </View>
    );
}


export function NavigationMaterialBottomTabs() {
    return (
        <NavigationContainer>
            <Tab.Navigator >
                <Tab.Screen name="Home" component={HomeScreen} />
                <Tab.Screen name="Settings" component={SettingsScreen} />
            </Tab.Navigator>
        </NavigationContainer>
    );
}   

```

## Link
本库依赖以下三方库，请查看对应文档：
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/elements](/zh-cn/react-navigation-elements.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-library/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-library/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md#link)进行引入


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
2. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [@react-navigation/material-bottom-tabs 的文档介绍](https://reactnavigation.org/docs/material-bottom-tab-navigator)

**Props**

| Name             | Description                                                                                                                                    | Type                                                                     | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| id               | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator.              | string                                                                   | no       | all      | yes               |
| initialRouteName | The name of the route to render on first load of the navigator.                                                                                | string                                                                   | no       | all      | yes               |
| screenOptions    | Default options to use for the screens in the navigator.                                                                                       | object                                                                   | no       | all      | yes               |
| backBehavior     | This controls what happens when goBack is called in the navigator. This includes pressing the device's back button or back gesture on Android. | 'firstRoute'&#124;'initialRoute'&#124;'order'&#124;'history'&#124;'none' | no       | Android  | yes               |
| shifting         | Whether the shifting style is used, the active tab icon shifts up to show the label and the inactive tabs won't have a label.                  | boolean                                                                  | no       | all      | yes               |
| labeled          | Whether to show labels in tabs. When false, only icons will be displayed.                                                                      | boolean                                                                  | no       | all      | yes               |
| activeColor      | Custom color for icon and label in the active tab.                                                                                             | string                                                                   | no       | all      | yes               |
| inactiveColor    | Custom color for icon and label in the inactive tab.                                                                                           | string                                                                   | no       | all      | yes               |
| barStyle         | Style for the bottom navigation bar.                                                                                                           | object                                                                   | no       | all      | yes               |

**Options & screenOptions**

| Name                     | Description                                                                                                                                                               | Type                         | Required | Platform | HarmonyOS Support |
|--------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|----------|----------|-------------------|
| title                    | Generic title that can be used as a fallback for headerTitle and tabBarLabel.                                                                                             | string                       | no       | all      | yes               |
| tabBarIcon               | Function that given { focused: boolean, color: string } returns a React.Node, to display in the tab bar.                                                                  | function                     | no       | all      | yes               |
| tabBarColor              | Color for the tab bar when the tab corresponding to the screen is active. Used for the ripple effect. This is only supported when shifting is true.                       | string                       | no       | no      | no                |
| tabBarLabel              | Title string of a tab displayed in the tab bar. When undefined, scene title is used. To hide, see labeled option in the previous section.                                 | string                       | no       | all      | yes               |
| tabBarBadge              | Badge to show on the tab icon, can be true to show a dot, string or number to show text.                                                                                  | true&#124;number&#124;string | no       | all      | yes               |
| tabBarAccessibilityLabel | Accessibility label for the tab button. This is read by the screen reader when the user taps the tab. It's recommended to set this if you don't have a label for the tab. | string                       | no       | all      | yes               |

**Events**
| Name     | Description                                                                                      | Type     | Required | Platform | HarmonyOS Support |
|----------|--------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| tabPress | This event is fired when the user presses the tab button for the current screen in the tab bar.  | function | no       | all      | yes               |
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/material-bottom-tabs/LICENSE) ，请自由地享受和参与开源。