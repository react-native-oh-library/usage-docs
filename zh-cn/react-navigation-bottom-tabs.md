> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/bottom-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/bottom-tabs/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-navigation/react-navigation/tree/6.x/packages/bottom-tabs)

## 安装与使用

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/bottom-tabs@6.5.20
```

#### **yarn**

```bash
yarn add @react-navigation/bottom-tabs@6.5.20
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';

function HomeScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home!</Text>
        </View>
    );
}

function SettingsScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Settings!</Text>
        </View>
    );
}

const Tab = createBottomTabNavigator();

export function NavigationBottomTabs() {
    return (
        <NavigationContainer>
            <Tab.Navigator>
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

1. RNOH: 0.72.11; SDK: OpenHarmony(api11) 4.1.0.53; IDE: DevEco Studio 4.1.3.412; ROM: 2.0.0.52;
2. RNOH: 0.72.13; SDK: HarmonyOS NEXT Developer Preview1; IDE: DevEco Studio 4.1.3.500; ROM: 2.0.0.58;
3. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
4. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/bottom-tabs 的文档介绍](https://reactnavigation.org/docs/bottom-tab-navigator)

**Props**
| Name                  | Description                                                                                                                                                                        | Type                                                                     | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------ | -------- | ----------- | ----------------- |
| id                    | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator.                                                  | string                                                                   | no       | all         | yes               |
| initialRouteName      | The name of the route to render on first load of the navigator.                                                                                                                    | string                                                                   | no       | all         | yes               |
| screenOptions         | Default options to use for the screens in the navigator.                                                                                                                           | object                                                                   | no       | all         | yes               |
| backBehavior          | This controls what happens when goBack is called in the navigator. This includes pressing the device's back button or back gesture on Android.                                     | 'firstRoute'&#124;'initialRoute'&#124;'order'&#124;'history'&#124;'none' | no       | Android     | yes               |
| detachInactiveScreens | Boolean used to indicate whether inactive screens should be detached from the view hierarchy to save memory. This enables integration with react-native-screens. Defaults to true. | boolean                                                                  | no       | Android,iOS | no                |
| sceneContainerStyle   | Style object for the component wrapping the screen content.                                                                                                                        | object                                                                   | no       | all         | yes               |
| tabBar                | tabBar                                                                                                                                                                             | function                                                                 | no       | all         | yes               |

**Options & screenOptions**

| Name                          | Description                                                                                                                                                                                               | Type                            | Required | Platform    | HarmonyOS Support |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------- | -------- | ----------- | ----------------- |
| title                         | Generic title that can be used as a fallback for headerTitle and tabBarLabel.                                                                                                                             | string                          | no       | all         | yes               |
| tabBarLabel                   | Title string of a tab displayed in the tab bar or a function that given { focused: boolean, color: string } returns a React.Node,                                                                         | function                        | no       | all         | yes               |
| tabBarShowLabel               | Whether the tab label should be visible. Defaults to true.                                                                                                                                                | boolean                         | no       | all         | yes               |
| tabBarLabelPosition           | Whether the label is shown below the icon or beside the icon.                                                                                                                                             | 'below-icon'&#124;'beside-icon' | no       | all         | yes               |
| tabBarLabelStyle              | Style object for the tab label.                                                                                                                                                                           | object                          | no       | all         | yes               |
| tabBarIcon                    | Function that given { focused: boolean, color: string, size: number } returns a React.Node, to display in the tab bar.                                                                                    | function                        | no       | all         | yes               |
| tabBarIconStyle               | Style object for the tab icon.                                                                                                                                                                            | object                          | no       | all         | yes               |
| tabBarBadge                   | Text to show in a badge on the tab icon. Accepts a string or a number.                                                                                                                                    | string&#124;number              | no       | all         | yes               |
| tabBarBadgeStyle              | Style for the badge on the tab icon. You can specify a background color or text color here.                                                                                                               | object                          | no       | all         | yes               |
| tabBarAccessibilityLabel      | Accessibility label for the tab button.                                                                                                                                                                   | string                          | no       | all         | yes               |
| tabBarButton                  | Function which returns a React element to render as the tab bar button.                                                                                                                                   | function                        | no       | all         | yes               |
| tabBarActiveTintColor         | Color for the icon and label in the active tab.                                                                                                                                                           | string                          | no       | all         | yes               |
| tabBarInactiveTintColor       | Color for the icon and label in the inactive tabs.                                                                                                                                                        | string                          | no       | all         | yes               |
| tabBarActiveBackgroundColor   | Background color for the active tab.                                                                                                                                                                      | string                          | no       | all         | yes               |
| tabBarInactiveBackgroundColor | Background color for the inactive tabs.                                                                                                                                                                   | string                          | no       | all         | yes               |
| tabBarHideOnKeyboard          | Whether the tab bar is hidden when the keyboard opens. Defaults to false.                                                                                                                                 | boolean                         | no       | all         | yes               |
| tabBarItemStyle               | Style object for the tab item container.                                                                                                                                                                  | object                          | no       | all         | yes               |
| tabBarStyle                   | Style object for the tab bar. You can configure styles such as background color here.                                                                                                                     | object                          | no       | all         | yes               |
| tabBarBackground              | Function which returns a React Element to use as background for the tab bar.                                                                                                                              | function                        | no       | all         | yes               |
| lazy                          | Whether this screens should render the first time it's accessed.                                                                                                                                          | boolean                         | no       | all         | yes               |
| unmountOnBlur                 | Whether this screen should be unmounted when navigating away from it.                                                                                                                                     | boolean                         | no       | all         | yes               |
| freezeOnBlur                  | Boolean indicating whether to prevent inactive screens from re-rendering. Defaults to false. Defaults to true when enableFreeze() from react-native-screens package is run at the top of the application. | boolean                         | no       | Android,iOS | no                |  |

**Header related options**
| Name        | Description                                                                                                                | Type     | Required | Platform | HarmonyOS Support |
| ----------- | -------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| header      | Custom header to use instead of the default header.                                                                        | function | no       | all      | yes               |
| headerShown | Whether to show or hide the header for the screen. The header is shown by default. Setting this to false hides the header. | boolean  | no       | all      | yes               |

**Events**
| Name         | Description                                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| ------------ | ---------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| tabPress     | This event is fired when the user presses the tab button for the current screen in the tab bar.                        | function | no       | all      | yes               |
| tabLongPress | This event is fired when the user presses the tab button for the current screen in the tab bar for an extended period. | function | no       | all      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/bottom-tabs/LICENSE) ，请自由地享受和参与开源。