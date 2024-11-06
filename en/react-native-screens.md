> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-screens</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-screens">
        <img src="https://img.shields.io/badge/platforms-iOS%20|%20Android%20|%20tvOS%20|%20Windows%20|%20Web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-screens/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/software-mansion/react-native-screens)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/native
npm install @react-native-oh-tpl/stack
npm install @react-native-oh-tpl/react-native-safe-area-context
npm install react-native-screens@3.29.0
```

#### **yarn**

```bash
yarn add @react-navigation/native
yarn add @react-navigation/stack
yarn add @react-native-oh-tpl/react-native-safe-area-context
yarn add react-native-screens@3.29.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import {ScrollView, Button, View, Text} from 'react-native';
import {NavigationContainer} from '@react-navigation/native';
import {createStackNavigator} from '@react-navigation/stack';
import { enableScreens } from "react-native-screens";

enableScreens(false);
function Home({navigation}) {
    return (
        <ScrollView
            style={{backgroundColor: 'yellow'}}
            contentInsetAdjustmentBehavior="automatic">
            <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
                <Text>Home Screen</Text>
            </View>
            <Button title="To Detail" onPress={() => navigation.push('Detail')} />
        </ScrollView>
    );
}

function Detail({navigation}) {
    return (
        <View style={{flex: 1, alignItems: 'center', justifyContent: 'center'}}>
            <Text>Details Screen</Text>
            <Button title="To Home" onPress={() => navigation.goBack()} />
        </View>
    );
}

const Stack = createStackNavigator();

function NativeNavigation() {
    return (
        <NavigationContainer>
            <Stack.Navigator>
                <Stack.Screen
                    name="Home"
                    component={Home}
                    options={{title: 'Home的title'}}
                />
                <Stack.Screen
                    name="Detail"
                    component={Detail}
                    options={{title: 'Detail的title'}}
                />
            </Stack.Navigator>
        </NavigationContainer>
    );
}

export default function RNScreenTest() {
    return <NativeNavigation />;
}

```

#### 禁用 `react-native-screens`

因为 ArkUI侧未提供capi接口，容器组件需要capi化，故本库未实现harmonyOS原生化，所以 react-native-screens 禁用 HarmonyOS 原生屏幕使用 react-native views 即可，请在您的入口文件中添加以下代码。 (例如. `App.js`):

```js
import { enableScreens } from "react-native-screens";

enableScreens(false);
```

您还可以通过[detachInactiveScreens](https://reactnavigation.org/docs/stack-navigator#detachinactivescreens)在每个导航器中禁用原生屏幕。

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/stack and @react-native-oh-tpl/react-native-safe-area-context. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/stack](/en/react-navigation-stack.md) and [@react-native-oh-tpl/react-native-safe-area-context](/en/react-native-safe-area-context.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1.RNOH:0.72.29; SDK:HarmonyOS-NEXT-DB6 5.0.0.61; IDE:DevEco Studio 5.0.3.706; ROM:3.0.0.60;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                                      | Description                                                                           | Type     | Required | Platform    | HarmonyOS Support |
|-----------------------------------------------------------|---------------------------------------------------------------------------------------|----------|----------|-------------|-------------------|
| enableScreens                                             | 支持原生及其 React Native View                                                              | function | No       | iOS Android | Yes               |
| enableFreeze                                              | 对 react-freeze 的支持，使用 ReactSuspense 机制来防止 React 组件树的部分渲染                              | function | No       | iOS Android | Yes               |
| createNativeStackNavigator                                | 提供屏幕切换的能力                                                                             | function | No       | iOS Android | NO                |
| NativeStackNavigationProp                                 | 切换页面属性的封装                                                                             | object   | No       | iOS Android | Yes               |
| NativeStackNavigationOptions                              | 导航栏属性设置封装                                                                             | object   | No       | iOS Android | NO                |
| FullWindowOverlay                                         | 一个组件，可以将其子组件放在其他组件之上                                                                  | object   | No       | iOS Android | NO                |
| SearchBarProps                                            | 搜索栏的属性设置封装                                                                            | object   | No       | iOS Android | NO                |
| SearchBarCommands                                         | 搜索栏的操作封装                                                                              | object   | No       | iOS Android | NO                |
| useTransitionProgress                                     | 提供屏幕过渡的动画插值器                                                                          | function | No       | iOS Android | NO                |
| userReanimatedTransitionProgress ReanimatedScreenProvider | 屏幕切换期间调用的帧回调，用于 react-native-reanimated 2.0 及其以上的版本，并使用 ReanimatedScreenProvider 进行封装 | function | No       | iOS Android | NO                |
| userHeaderHeight                                          | 计算静态标题栏的高度，当屏幕方向发生更改，此值会发生更改                                                          | function | No       | iOS Android | NO                |
| userAnimatedHeaderHeight                                  | 动态计算标题栏的高度，此值会随着每个视图布局变化而变化                                                           | function | No       | iOS Android | NO                |

## Known Issues

- [ ] ArkUI侧未提供capi接口，容器组件需要capi化，故本库未实现harmonyOS原生化适配，harmonyOS侧仅支持部分属性。

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/software-mansion/react-native-screens/blob/main/LICENSE).
