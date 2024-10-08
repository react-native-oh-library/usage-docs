> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/material-top-tabs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/material-top-tabs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/material-top-tabs/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-navigation/react-navigation/tree/6.x/packages/material-top-tabs)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-navigation/material-top-tabs@6.6.13
```

#### **yarn**

```bash
yarn add @react-navigation/material-top-tabs@6.6.13
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { createMaterialTopTabNavigator } from '@react-navigation/material-top-tabs';
import { View, Text,SafeAreaView } from 'react-native'
import { NavigationContainer } from '@react-navigation/native';
import * as React from 'react';

const Tab = createMaterialTopTabNavigator();


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


export function NavigationMaterialTopTabs() {
    return (
        <SafeAreaView style={{ flex: 1 }}>
            <NavigationContainer>
                <Tab.Navigator >
                    <Tab.Screen name="Home" component={HomeScreen} options={{ title: '家' }} />
                    <Tab.Screen name="Settings" component={SettingsScreen} options={{ title: '设置' }} />
                </Tab.Navigator>
            </NavigationContainer>
        </SafeAreaView>
    );
}

```


## Link
本库依赖以下三方库，请查看对应文档：
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/react-native-tab-view](/zh-cn/react-native-tab-view.md)
+ [@react-native-oh-tpl/react-native-pager-view](/zh-cn/react-native-pager-view.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-tab-view、@react-native-oh-tpl/react-native-pager-view  的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-tab-view 文档的 Link 章节](/zh-cn/react-native-tab-view.md#link)，[@react-native-oh-tpl/react-native-pager-view 文档的 Link 章节](/zh-cn/react-native-pager-view.md#link)，进行引入


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK：HarmonyOS NEXT Developer Beta1 B.0.18; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [@react-navigation/material-top-tabs 的文档介绍](https://reactnavigation.org/docs/material-top-tab-navigator)

**Props**
| Name                | Description                                                                                                                                    | Type                                                                    | Required | Platform | HarmonyOS Support |
|---------------------|------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|----------|----------|-------------------|
| id                  | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator.              | string                                                                  | no       | all      | yes               |
| initialRouteName    | The name of the route to render on first load of the navigator.                                                                                | string                                                                  | no       | all      | yes               |
| screenOptions       | Default options to use for the screens in the navigator.                                                                                       | object                                                                  | no       | all      | yes               |
| backBehavior        | This controls what happens when goBack is called in the navigator. This includes pressing the device's back button or back gesture on Android. | 'firstRoute'&#124;'initialRoute'&#124;'order'&#124;'history'&#124;'none' | no       | Android  | yes               |
| tabBarPosition      | Position of the tab bar in the tab view. Possible values are 'top' and 'bottom'. Defaults to 'top'.                                            | 'top'&#124;'bottom'                                                      | no       | all      | yes               |
| keyboardDismissMode | String indicating whether the keyboard gets dismissed in response to a drag gesture.                                                           | 'auto'&#124;'on-drag'&#124;'none'                                        | no       | all      | yes               |
| initialLayout       | Object containing the initial height and width of the screens.                                                                                 | object                                                                  | no       | all      | yes               |
| sceneContainerStyle | Style to apply to the view wrapping each screen. You can pass this to override some default styles such as overflow clipping.                  | object                                                                  | no       | all      | yes               |
| style               | Style to apply to the tab view container.                                                                                                      | object                                                                  | no       | all      | yes               |
| tabBar              | Function that returns a React element to display as the tab bar.                                                                               | function                                                                | no       | all      | yes               |

**Options & screenOptions**
| Name                          | Description                                                                                                                                                                                        | Type                 | Required | Platform    | HarmonyOS Support |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------------------|----------|-------------|-------------------|
| title                         | Generic title that can be used as a fallback for headerTitle and tabBarLabel.                                                                                                                      | string               | no       | all         | yes               |
| tabBarLabel                   | Title string of a tab displayed in the tab bar or a function                                                                                                                                       | string&#124;function | no       | all         | yes               |
| tabBarAccessibilityLabel      | Accessibility label for the tab button. This is read by the screen reader when the user taps the tab.                                                                                              | string               | no       | all         | yes               |
| tabBarAllowFontScaling        | Whether label font should scale to respect Text Size accessibility settings.                                                                                                                       | boolean              | no       | all         | yes               |
| tabBarShowLabel               | Whether the tab label should be visible. Defaults to true.                                                                                                                                         | boolean              | no       | all         | yes               |
| tabBarIcon                    | Function that given { focused: boolean, color: string } returns a React.Node,                                                                                                                      | function             | no       | all         | yes               |
| tabBarShowIcon                | Whether the tab icon should be visible. Defaults to false.                                                                                                                                         | boolean              | no       | all         | yes               |
| tabBarBadge                   | Function that returns a React element to use as a badge for the tab.                                                                                                                               | function             | no       | all         | yes               |
| tabBarIndicator               | Function that returns a React element as the tab bar indicator.                                                                                                                                    | function             | no       | all         | yes               |
| tabBarIndicatorStyle          | Style object for the tab bar indicator.                                                                                                                                                            | object               | no       | all         | yes               |
| tabBarIndicatorContainerStyle | Style object for the view containing the tab bar indicator.                                                                                                                                        | object               | no       | all         | yes               |
| tabBarActiveTintColor         | Color for the icon and label in the active tab.                                                                                                                                                    | string               | no       | all         | yes               |
| tabBarInactiveTintColor       | Color for the icon and label in the inactive tabs.                                                                                                                                                 | string               | no       | all         | yes               |
| tabBarGap                     | Spacing between the tab items in the tab bar.                                                                                                                                                      | number               | no       | all         | yes               |
| tabBarAndroidRipple           | Allows to customize the Android ripple effect.                                                                                                                                                     | object               | no       | Android     | no                |
| tabBarPressColor              | Color for material ripple.                                                                                                                                                                         | string               | no       | Android     | no                |
| tabBarPressOpacity            | Opacity for pressed tab.                                                                                                                                                                           | string               | no       | Android，iOS | yes               |
| tabBarBounces                 | Boolean indicating whether the tab bar bounces when overscrolling.                                                                                                                                 | boolean              | no       | iOS         | no                |
| tabBarScrollEnabled           | Boolean indicating whether to make the tab bar scrollable.                                                                                                                                         | boolean              | no       | all         | yes               |
| tabBarIconStyle               | Style object for the tab icon container.                                                                                                                                                           | object               | no       | all         | yes               |
| tabBarLabelStyle              | Style object for the tab label.                                                                                                                                                                    | object               | no       | all         | yes               |
| tabBarItemStyle               | Style object for the individual tab items.                                                                                                                                                         | object               | no       | all         | yes               |
| tabBarContentContainerStyle   | Style object for the view containing the tab items.                                                                                                                                                | object               | no       | all         | yes               |
| tabBarStyle                   | Style object for the tab bar.                                                                                                                                                                      | object               | no       | all         | yes               |
| swipeEnabled                  | Boolean indicating whether to enable swipe gestures. Swipe gestures are enabled by default. Passing false will disable swipe gestures, but the user can still switch tabs by pressing the tab bar. | boolean              | no       | all         | yes               |
| lazy                          | Whether this screen should be lazily rendered.                                                                                                                                                     | boolean              | no       | all         | yes               |
| lazyPreloadDistance           | When lazy is enabled, you can specify how many adjacent screens should be preloaded in advance with this prop.                                                                                     | number               | no       | all         | yes               |
| lazyPlaceholder               | Function that returns a React element to render if this screen hasn't been rendered yet.                                                                                                           | function             | no       | all         | yes               |

**Events**
| Name         | Description                                                                                                            | Type     | Required | Platform | HarmonyOS Support |
|--------------|------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| tabPress     | This event is fired when the user presses the tab button for the current screen in the tab bar.                        | function | no       | all      | yes               |
| tabLongPress | This event is fired when the user presses the tab button for the current screen in the tab bar for an extended period. | function | no       | all      | yes               |

## 遗留问题

## 其他
  
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/material-top-tabs/LICENSE) ，请自由地享受和参与开源。