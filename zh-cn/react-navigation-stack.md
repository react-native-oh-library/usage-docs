> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/stack</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/stack/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/stack)


## 安装与使用

进入到工程目录并输入以下命令：


请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/stack
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/stack
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
```js
import * as React from 'react';
import { Button, Text, View } from 'react-native';
import { NavigationContainer } from '@react-navigation/native';
import { createStackNavigator } from '@react-navigation/stack';



const HomeStack = createStackNavigator();

function HomeScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home screen</Text>
            <Button
                title="Go to Details"
                onPress={() => navigation.navigate('Details')}
            />
        </View>
    );
}

function DetailsScreen({ navigation }) {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Details!</Text>
            <Button
                title="Go back"
                onPress={() => navigation.goBack()}
            />
        </View>
    );
}



export default function App() {
    return (
        <NavigationContainer>
            <HomeStack.Navigator>
                <HomeStack.Screen name="Home" component={HomeScreen} />
                <HomeStack.Screen name="Details" component={DetailsScreen} />
            </HomeStack.Navigator>
        </NavigationContainer>
    );
}
```

## Link
本库依赖以下三方库，请查看对应文档：
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)
+ [react-native-screens](/zh-cn/react-native-screens.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-library/react-native-safe-area-context 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-library/react-native-safe-area-context 文档](/zh-cn/react-native-safe-area-context.md)进行引入



## 约束与限制
### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多属性详情请查看 [react-navigation/stack 的文档介绍](https://reactnavigation.org/docs/stack-navigator)


**Props**

| Name                  | Description                                                                                                                                                                        | Type    | Required | Platform    | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| id                    | Optional unique ID for the navigator. This can be used with navigation.getParent to refer to this navigator in a child navigator.                                                  | string  | no       | all         | yes               |
| initialRouteName      | The name of the route to render on first load of the navigator.                                                                                                                    | string  | no       | all         | yes               |
| screenOptions         | Default options to use for the screens in the navigator.                                                                                                                           | object  | no       | all         | yes               |
| detachInactiveScreens | Boolean used to indicate whether inactive screens should be detached from the view hierarchy to save memory. This enables integration with react-native-screens. Defaults to true. | boolean | no       | Android,iOS | no                |


**Options & screenOptions**

| Name                         | Description                                                                                                                                                                                                                                                                                                               | Type                                        | Required | Platform    | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- | -------- | ----------- | ----------------- |
| title                        | String that can be used as a fallback for headerTitle.                                                                                                                                                                                                                                                                    | string                                      | no       | all         | yes               |
| cardShadowEnabled            | Use this prop to have visible shadows during transitions. Defaults to true.                                                                                                                                                                                                                                               | boolean                                     | no       | all         | yes               |
| cardOverlayEnabled           | Use this prop to have a semi-transparent dark overlay visible under the card during transitions. Defaults to true on Android and false on iOS.                                                                                                                                                                            | boolean                                     | no       | all         | yes               |
| cardOverlay                  | Function which returns a React Element to display as the overlay for the card. Make sure to set cardOverlayEnabled to true when using this.                                                                                                                                                                               | fucntion                                    | no       | all         | yes               |
| cardStyle                    | Style object for the card in stack. You can provide a custom background color to use instead of the default background here.                                                                                                                                                                                              | object                                      | no       | all         | yes               |
| presentation                 | This is shortcut option which configures several options to configure the style for rendering and transitions.                                                                                                                                                                                                            | 'card'&#124;'modal'&#124;'transparentModal' | no       | all         | yes               |
| animationEnabled             | Whether transition animation should be enabled on the screen. If you set it to false, the screen won't animate when pushing or popping. Defaults to true on iOS and Android, false on Web.                                                                                                                                | boolean                                     | no       | all         | yes               |
| animationTypeForReplace      | The type of animation to use when this screen replaces another screen.                                                                                                                                                                                                                                                    | 'push'&#124;'pop'                           | no       | all         | yes               |
| gestureEnabled               | Whether you can use gestures to dismiss this screen.                                                                                                                                                                                                                                                                      | boolean                                     | no       | Android,iOS | yes               |
| gestureResponseDistance      | Number to override the distance of touch start from the edge of the screen to recognize gestures.                                                                                                                                                                                                                         | number                                      | no       | Android,iOS | yes               |
| gestureVelocityImpact        | Number which determines the relevance of velocity for the gesture. Defaults to 0.3.                                                                                                                                                                                                                                       | number                                      | no       | Android,iOS | yes               |
| gestureDirection             | Direction of the gestures.                                                                                                                                                                                                                                                                                                | string                                      | no       | Android,iOS | yes               |
| transitionSpec               | Configuration object for the screen transition.                                                                                                                                                                                                                                                                           | object                                      | no       | all         | yes               |
| cardStyleInterpolator        | Interpolated styles for various parts of the card.                                                                                                                                                                                                                                                                        | object                                      | no       | all         | yes               |
| headerStyleInterpolator      | Interpolated styles for various parts of the header.                                                                                                                                                                                                                                                                      | object                                      | no       | all         | yes               |
| keyboardHandlingEnabled      | If false, the keyboard will NOT automatically dismiss when navigating to a new screen from this screen. Defaults to true.                                                                                                                                                                                                 | boolean                                     | no       | all         | yes               |
| detachPreviousScreen         | Boolean used to indicate whether to detach the previous screen from the view hierarchy to save memory. Set it to false if you need the previous screen to be seen through the active screen. Only applicable if detachInactiveScreens isn't set to false.                                                                 | boolean                                     | no       | all         | no                |
| freezeOnBlur                 | Boolean indicating whether to prevent inactive screens from re-rendering. Defaults to false. Defaults to true when enableFreeze() from react-native-screens package is run at the top of the application.                                                                                                                 | boolean                                     | no       | all         | no                |
| header                       | Custom header to use instead of the default header.                                                                                                                                                                                                                                                                       | function                                    | no       | all         | yes               |
| headerMode                   | Specifies how the header should be rendered.                                                                                                                                                                                                                                                                              | 'float'&#124;'screen'                       | no       | all         | yes               |
| headerShown                  | Whether to show or hide the header for the screen. The header is shown by default. Setting this to false hides the header.                                                                                                                                                                                                | boolean                                     | no       | all         | yes               |
| headerBackAllowFontScaling   | Whether back button title font should scale to respect Text Size accessibility settings. Defaults to false.                                                                                                                                                                                                               | boolean                                     | no       | all         | yes               |
| headerBackAccessibilityLabel | Accessibility label for the header back button.                                                                                                                                                                                                                                                                           | string                                      | no       | all         | yes               |
| headerBackImage              | Function which returns a React Element to display custom image in header's back button. When a function is used, it receives the tintColor in it's argument object. Defaults to Image component with back image source, which is the default back icon image for the platform (a chevron on iOS and an arrow on Android). | function                                    | no       | all         | yes               |
| headerBackTitle              | Title string used by the back button on iOS. Defaults to the previous scene's headerTitle.                                                                                                                                                                                                                                | string                                      | no       | all         | yes               |
| headerBackTitleVisible       | A reasonable default is supplied for whether the back button title should be visible or not, but if you want to override that you can use true or false in this option.                                                                                                                                                   | boolean                                     | no       | all         | yes               |
| headerTruncatedBackTitle     | Title string used by the back button when headerBackTitle doesn't fit on the screen. "Back" by default.                                                                                                                                                                                                                   | string                                      | no       | all         | yes               |
| headerBackTitleStyle         | Style object for the back title.                                                                                                                                                                                                                                                                                          | object                                      | no       | all         | yes               |

**Events**
| Name            | Description                                                                                                                    | Type     | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| transitionStart | This event is fired when the transition animation starts for the current screen.                                               | function | no       | all      | yes               |
| transitionEnd   | This event is fired when the transition animation ends for the current screen.                                                 | function | no       | all      | yes               |
| gestureStart    | This event is fired when the swipe gesture starts for the current screen.                                                      | function | no       | all      | yes               |
| gestureEnd      | This event is fired when the swipe gesture ends for the current screen. e.g. a screen was successfully dismissed.              | function | no       | all      | yes               |
| gestureCancel   | This event is fired when the swipe gesture is cancelled for the current screen. e.g. a screen wasn't dismissed by the gesture. | function | no       | all      | yes               |
## 遗留问题

- [ ] TextInput组件可以穿透下个页面点击。[issues#37](https://github.com/react-native-oh-library/react-navigation/issues/37)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/stack/LICENSE) ，请自由地享受和参与开源。
