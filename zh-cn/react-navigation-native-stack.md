> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/native-stack</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/native-stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/native-stack/LICENSE">
         <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/native-stack)

## 安装与使用


请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

### **npm**

```bash
npm install @react-native-oh-tpl/native-stack
```

### **yarn**

```bash
yarn install @react-native-oh-tpl/native-stack
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

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

## Link

本库依赖以下三方库，请查看对应文档：
+ [react-native-screens](/zh-cn/react-native-screens.md)
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-library/elements](/zh-cn/react-native-elements.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-library/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-library/react-native-safe-area-context 文档的 Link 章节](/zh-cn/react-native-safe-area-context.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/native-stack 的文档介绍](https://reactnavigation.org/docs/native-stack-navigator)

**Props**
| Name             | Description                                                                                                                       | Type   | Required | Platform | HarmonyOS Support |
|------------------|-----------------------------------------------------------------------------------------------------------------------------------|--------|----------|----------|-------------------|
| id               | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator. | string | no       | all      | yes               |
| initialRouteName | The name of the route to render on first load of the navigator.                                                                   | string | no       | all      | yes               |
| screenOptions    | Default options to use for the screens in the navigator.                                                                          | object | no       | all      | yes               |


**Options & screenOptions**
| Name                          | Description                                                                                                                                                                                                                                                                                                                                  | Type                                                                                                                                     | Required | Platform    | HarmonyOS Support |
|-------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------|----------|-------------|-------------------|
| title                         | String that can be used as a fallback for headerTitle.                                                                                                                                                                                                                                                                                       | string                                                                                                                                   | no       | all         | yes               |
| headerBackButtonMenuEnabled   | Boolean indicating whether to show the menu on longPress of iOS >= 14 back button. Defaults to true.                                                                                                                                                                                                                                         | boolean                                                                                                                                  | no       | iOS         | no                |
| headerBackVisible             | Whether the back button is visible in the header. You can use it to show a back button alongside headerLeft if you have specified it.                                                                                                                                                                                                        | boolean                                                                                                                                  | no       | Android,iOS | no                |
| headerBackTitle               | Title string used by the back button on iOS. Defaults to the previous scene's title, or "Back" if there's not enough space. Use headerBackTitleVisible: false to hide it.                                                                                                                                                                    | string                                                                                                                                   | no       | iOS         | no                |
| headerBackTitleStyle          | Style object for header back title.                                                                                                                                                                                                                                                                                                          | object                                                                                                                                   | no       | iOS         | no                |
| headerBackImageSource         | Image to display in the header as the icon in the back button.                                                                                                                                                                                                                                                                               | string                                                                                                                                   | no       | all         | yes               |
| headerLargeStyle              | Style of the header when a large title is shown.                                                                                                                                                                                                                                                                                             | object                                                                                                                                   | no       | iOS         | no                |
| headerLargeTitle              | Whether to enable header with large title which collapses to regular header on scroll.                                                                                                                                                                                                                                                       | string                                                                                                                                   | no       | iOS         | no                |
| headerLargeTitleShadowVisible | Whether drop shadow of header is visible when a large title is shown.                                                                                                                                                                                                                                                                        | boolean                                                                                                                                  | no       | iOS         | no                |
| headerLargeTitleStyle         | Style object for large title in header.                                                                                                                                                                                                                                                                                                      | object                                                                                                                                   | no       | iOS         | no                |
| headerShown                   | Whether to show the header. The header is shown by default. Setting this to false hides the header.                                                                                                                                                                                                                                          | boolean                                                                                                                                  | no       | all         | yes               |
| headerStyle                   | Style object for header.                                                                                                                                                                                                                                                                                             | object                                                                                                                                   | no       | all         | yes               |
| headerShadowVisible           | Whether to hide the elevation shadow (Android) or the bottom border (iOS) on the header.                                                                                                                                                                                                                                                     | object                                                                                                                                   | no       | Android，iOS | yes               |
| headerTransparent             | Boolean indicating whether the navigation bar is translucent.                                                                                                                                                                                                                                                                                | boolean                                                                                                                                  | no       | all         | yes               |
| headerBlurEffect              | Blur effect for the translucent header. The headerTransparent option needs to be set to true for this to work.                                                                                                                                                                                                                               | string                                                                                                                                   | no       | iOS         | no                |
| headerBackground              | Function which returns a React Element to render as the background of the header. This is useful for using backgrounds such as an image or a gradient.                                                                                                                                                                                       | function                                                                                                                                 | no       | all         | yes               |
| headerTintColor               | Tint color for the header. Changes the color of back button and title.                                                                                                                                                                                                                                                                       | string                                                                                                                                   | no       | all         | yes               |
| headerLeft                    | Function which returns a React Element to display on the left side of the header. This replaces the back button. See headerBackVisible to show the back button along side left element.                                                                                                                                                      | function                                                                                                                                 | no       | all         | yes               |
| headerRight                   | Function which returns a React Element to display on the right side of the header.                                                                                                                                                                                                                                                           | function                                                                                                                                 | no       | all         | yes               |
| headerTitle                   | String or a function that returns a React Element to be used by the header. Defaults to title or name of the screen.                                                                                                                                                                                                                         | string&#124;function                                                                                                                          | no       | all         | yes               |
| headerTitleAlign              | How to align the header title.Defaults to left on platforms other than iOS.Not supported on iOS. It's always center on iOS and cannot be changed.                                                                                                                                                                                            | 'left'&#124;'right'                                                                                                                            | no       | Android     | yes               |
| headerTitleStyle              | Style object for header title.                                                                                                                                                                                                                                                                                                               | object                                                                                                                                   | no       | all         | yes               |
| headerSearchBarOptions        | Options to render a native search bar on iOS.                                                                                                                                                                                                                                                                                                | object                                                                                                                                   | no       | Android，iOS | no                |
| header                        | Custom header to use instead of the default header.                                                                                                                                                                                                                                                                                          | function                                                                                                                                 | no       | all         | no                |
| statusBarAnimation            | Sets the status bar animation (similar to the StatusBar component). Defaults to fade on iOS and none on Android.                                                                                                                                                                                                                             | 'fade'&#124;'none'&#124;'slide'                                                                                                           | no       | Android，iOS | no                |
| statusBarHidden               | Whether the status bar should be hidden on this screen.                                                                                                                                                                                                                                                                                      | boolean                                                                                                                                  | no       | Android，iOS | no                |
| statusBarStyle                | Sets the status bar color (similar to the StatusBar component). Defaults to auto.                                                                                                                                                                                                                                                            | string                                                                                                                                   | no       | Android，iOS | no                |
| statusBarColor                | Sets the status bar color (similar to the StatusBar component). Defaults to initial status bar color.                                                                                                                                                                                                                                        | string                                                                                                                                   | no       | Android     | no                |
| statusBarTranslucent          | Sets the translucency of the status bar (similar to the StatusBar component). Defaults to false.                                                                                                                                                                                                                                             | boolean                                                                                                                                  | no       | Android     | no                |
| contentStyle                  | Style object for the scene content.                                                                                                                                                                                                                                                                                                          | object                                                                                                                                   | no       | all         | yes               |
| customAnimationOnGesture      | Whether the gesture to dismiss should use animation provided to animation prop. Defaults to false.                                                                                                                                                                                                                                           | boolean                                                                                                                                  | no       | iOS         | no                |
| fullScreenGestureEnabled      | Whether the gesture to dismiss should work on the whole screen. Using gesture to dismiss with this option results in the same transition animation as simple_push. This behavior can be changed by setting customAnimationOnGesture prop. Achieving the default iOS animation isn't possible due to platform limitations. Defaults to false. | boolean                                                                                                                                  | no       | iOS         | no                |
| gestureEnabled                | Whether you can use gestures to dismiss this screen. Defaults to true.                                                                                                                                                                                                                                                                       | boolean                                                                                                                                  | no       | iOS         | no                |
| animationTypeForReplace       | The type of animation to use when this screen replaces another screen. Defaults to pop.                                                                                                                                                                                                                                                      | 'push'&#124;'pop'                                                                                                                         | no       | Android，iOS | no                |
| animation                     | How the screen should animate when pushed or popped.                                                                                                                                                                                                                                                                                         | 'default'&#124;'fade'&#124;'fade_from_bottom'&#124;'fade_from_bottom'&#124;'simple_push'&#124;'slide_from_bottom'&#124;'slide_from_right'&#124;'slide_from_left'&#124;'none'      | no       | Android,iOS | no                |
| presentation                  | How should the screen be presented.                                                                                                                                                                                                                                                                                                          | 'card'&#124;'modal'&#124;'transparentModal'&#124;'containedModal'&#124;'containedModal'&#124;'fullScreenModal'&#124;'formSheet'           | no       | Android，iOS | partially         |
| orientation                   | The display orientation to use for the screen.                                                                                                                                                                                                                                                                                               | 'default'&#124;'all'&#124;'portrait'&#124;'portrait_up'&#124;'portrait_down'&#124;'landscape'&#124;'landscape_left'&#124;'landscape_left' | no       | Android，iOS | no                |
| autoHideHomeIndicator         | Boolean indicating whether the home indicator should prefer to stay hidden. Defaults to false.                                                                                                                                                                                                                                               | boolean                                                                                                                                  | no       | iOS         | no                |
| gestureDirection              | Sets the direction in which you should swipe to dismiss the screen.                                                                                                                                                                                                                                                                          | 'vertical '&#124;'horizontal '                                                                                                            | no       | iOS         | no                |
| animationDuration             | Changes the duration (in milliseconds) of slide_from_bottom, fade_from_bottom, fade and simple_push transitions on iOS. Defaults to 350.                                                                                                                                                                                                     | number                                                                                                                                  | no       | iOS         | no                |
| navigationBarColor            | Sets the navigation bar color. Defaults to initial status bar color.                                                                                                                                                                                                                                                                         | string                                                                                                                                   | no       | Android     | no                |
| navigationBarHidden           | Boolean indicating whether the navigation bar should be hidden. Defaults to false.                                                                                                                                                                                                                                                           | boolean                                                                                                                                  | no       | Android     | no                |
| freezeOnBlur                  | Boolean indicating whether to prevent inactive screens from re-rendering. Defaults to false. Defaults to true when enableFreeze() from react-native-screens package is run at the top of the application.                                                                                                                                    | boolean                                                                                                                                  | no       | Android,iOS | no                |

**Events**
| Name            | Description                                                                      | Type     | Required | Platform | HarmonyOS Support |
|-----------------|----------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| transitionStart | This event is fired when the transition animation starts for the current screen. | function | no       | all      | no                |
| transitionEnd   | This event is fired when the transition animation ends for the current screen.   | function | no       | all      | no                |

## 遗留问题

- [ ] react-native-screens功能缺失，导致headerSearchBarOptions等属性功能无法实现：[issue#25](https://github.com/react-native-oh-library/react-navigation/issues/25)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/main/packages/native-stack/LICENSE) ，请自由地享受和参与开源。