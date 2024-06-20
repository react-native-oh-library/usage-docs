> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-screens</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-screens">
        <img src="https://img.shields.io/badge/platforms-iOS%20|%20Android%20|%20tvOS%20|%20Windows%20|%20Web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://opensource.org/license/mit/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/bottom-tabs
npm install @react-navigation/native
npm install @react-navigation/native-stack
npm install @react-navigation/stack
npm install @react-native-oh-tpl/react-native-gesture-handler
npm install react-native-reanimated
npm install @react-native-oh-tpl/react-native-safe-area-context
npm install react-native-screens
```

#### **yarn**

```bash
yarn add @react-navigation/bottom-tabs
yarn add @react-navigation/native
yarn add @react-navigation/native-stack
yarn add @react-navigation/stack
yarn add @react-native-oh-tpl/react-native-gesture-handler
yarn add react-native-reanimated
yarn add @react-native-oh-tpl/react-native-safe-area-context
yarn add react-native-screens
```

<!-- tabs:end -->

声明：[@react-native-oh-tpl/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)和[@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)需要进行额外的配置，详情请去对应的文档查看。

下面的代码展示了这个库的基本使用场景：

<!-- {% raw %} -->
```js
import React from "react";
import { NavigationContainer, ParamListBase } from "@react-navigation/native";
import { ScrollView, Button, Tesxt } from "react-native";
import { NativeStackNavigationProp } from "react-native-screens";
import { createBottomTabNavigator } from "@react-navigation/bottom-tabs";
import { createStackNavigator } from "@react-navigation/stack";
import { enableScreens } from "react-native-screens";

enableScreens(false);

const Stack = createStackNavigator();

function NativeNavigation() {
  return (
    <NavigationContainer>
      <Stack.Navigator>
        <Stack.Screen name="Home" component={Home} />
      </Stack.Navigator>
    </NavigationContainer>
  );
}

const Tab = createBottomTabNavigator();
const NestedNavigator = () => (
  <Tab.Navigator>
    <Tab.Screen name="Screen1" component={Home} />
  </Tab.Navigator>
);

function Home({
  navigation,
}: {
  navigation: NativeStackNavigationProp<ParamListBase>,
}) {
  return (
    <ScrollView
      style={{ backgroundColor: "yellow" }}
      contentInsetAdjustmentBehavior="automatic"
    >
      <Button
        title="NestedNavigator"
        onPress={() => {
          navigation.push("NestedNavigator");
        }}
      />
    </ScrollView>
  );
}

export default function RNScreenTest() {
  return <NativeNavigation />;
}
```

#### 禁用 `react-native-screens`

因为 ArkUI(Navigation、NavRouter、NavDestination)没有代理任何独特功能，且无法映射到 main_page 通过页面容器优化性能，所以 react-native-screens 禁用 HarmonyOS 原生屏幕使用 react-native views 即可，请在您的入口文件中添加以下代码。 (例如. `App.js`):

```js
import { enableScreens } from "react-native-screens";

enableScreens(false);
```
<!-- {% endraw %} -->

您还可以通过[`detachInactiveScreens`](https://reactnavigation.org/docs/stack-navigator#detachinactivescreens)在每个导航器中禁用使用原生屏幕。

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 属性

| Name                                                      | Description                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| enableScreens                                             | 支持原生及其 React Native View                                                                                      | function | No       | All      | Yes               |
| enableFreeze                                              | 对 react-freeze 的支持，使用 ReactSuspense 机制来防止 React 组件树的部分渲染                                        | function | No       | All      | Yes               |
| createNativeStackNavigator                                | 提供屏幕切换的能力                                                                                                  | function | No       | All      | NO                |
| NativeStackNavigationProp                                 | 切换页面属性的封装                                                                                                  | object   | No       | All      | Yes               |
| NativeStackNavigationOptions                              | 导航栏属性设置封装                                                                                                  | object   | No       | All      | NO                |
| FullWindowOverlay                                         | 一个组件，可以将其子组件放在其他组件之上                                                                            | object   | No       | All      | Yes               |
| SearchBarProps                                            | 搜索栏的属性设置封装                                                                                                | object   | No       | All      | NO                |
| SearchBarCommands                                         | 搜索栏的操作封装                                                                                                    | object   | No       | All      | NO                |
| useTransitionProgress                                     | 提供屏幕过渡的动画插值器                                                                                            | function | No       | All      | NO                |
| userReanimatedTransitionProgress ReanimatedScreenProvider | 屏幕切换期间调用的帧回调，用于 react-native-reanimated 2.0 及其以上的版本，并使用 ReanimatedScreenProvider 进行封装 | function | No       | All      | NO                |
| userHeaderHeight                                          | 计算静态标题栏的高度，当屏幕方向发生更改，此值会发生更改                                                            | function | No       | All      | NO                |
| userAnimatedHeaderHeight                                  | 动态计算标题栏的高度，此值会随着每个视图布局变化而变化                                                              | function | No       | All      | NO                |

[原库接口文档](https://github.com/software-mansion/react-native-screens/blob/main/guides/GUIDE_FOR_LIBRARY_AUTHORS.md) ，欢迎提交 [issue](https://gitee.com/react-native-oh-library/usage-docs/issues).

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/software-mansion/react-native-screens/blob/main/LICENSE) ，请自由地享受和参与开源。
