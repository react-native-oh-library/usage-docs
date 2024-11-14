> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-navigation/elements</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/elements">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/elements/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/elements)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/elements Releases](https://github.com/react-native-oh-library/react-navigation/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/elements
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/elements
```

<!-- tabs:end -->


下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { Header, getHeaderTitle } from "@react-navigation/elements";
import { createStackNavigator } from "@react-navigation/stack"
import { NavigationContainer } from "@react-navigation/native";
import { Text, View } from 'react-native';


const Stack = createStackNavigator();

function HomeScreen() {
    return (
        <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
            <Text>Home Screen</Text>
        </View>
    );
}

export function NavigationElements() {
    return (
        <NavigationContainer>
            <Stack.Navigator
                screenOptions={{
                    header: ({ options, route }) => (
                        <Header {...options} title={getHeaderTitle(options, route.name)} headerStyle={{ backgroundColor: 'red' }} />
                    ),
                }}
            >
                <Stack.Screen name="Home" component={HomeScreen} />
            </Stack.Navigator>
        </NavigationContainer>
    );
}

export default NavigationElements;
```

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases?q=elements&expanded=true)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

以下属性已验证，更多使用详情请查看 [react-navigation/elements 的文档介绍](https://reactnavigation.org/docs/elements)

**Header Props**
| Name                           | Description                                                                                                                | Type                | Required | Platform | HarmonyOS Support |
|--------------------------------|----------------------------------------------------------------------------------------------------------------------------|---------------------|----------|----------|-------------------|
| headerTitle                    | String or a function that returns a React Element to be used by the header.                                                |              string       | no       | all      | yes               |
| headerTitleAlign               | How to align the header title                                                                                              | 'left'&#124;'center' | no       | all      | yes               |
| headerTitleAllowFontScaling    | Whether header title font should scale to respect Text Size accessibility settings.                                        | boolean             | no       | all      | yes               |
| headerLeft                     | Function which returns a React Element to display on the left side of the header.                                          | function            | no       | all      | yes               |
| headerRight                    | Function which returns a React Element to display on the right side of the header.                                         | function            | no       | all      | yes               |
| headerShadowVisible            | Whether to hide the elevation shadow (Android) or the bottom border (iOS) on the header.                                   | boolean             | no       | all      | yes               |
| headerStyle                    | Style object for the header. You can specify a custom background color here                                                | object              | no       | all      | yes               |
| headerTitleStyle               | Style object for the title component                                                                                       | object              | no       | all      | yes               |
| headerLeftContainerStyle       | Customize the style for the container of the headerLeft component, for example to add padding.                             | object              | no       | all      | yes               |
| headerRightContainerStyle      | Customize the style for the container of the headerRight component, for example to add padding.                            | object              | no       | all      | yes               |
| headerTitleContainerStyle      | Customize the style for the container of the headerTitle component, for example to add padding.                            | object              | no       | all      | yes               |
| headerBackgroundContainerStyle | Style object for the container of the headerBackground element.                                                            | object              | no       | all      | yes               |
| headerTintColor                | Tint color for the header                                                                                                  | string              | no       | all      | yes               |
| headerPressColor               | Color for material ripple (Android >= 5.0 only)                                                                            | string              | no       | Android  | no                |
| headerPressOpacity             | Press opacity for the buttons in header (Android < 5.0, and iOS)                                                           | number              | no       | all      | yes               |
| headerTransparent              | Defaults to false. If true, the header will not have a background unless you explicitly provide it with headerBackground.  | boolean             | no       | all      | yes               |
| headerBackground               | Function which returns a React Element to render as the background of the header.                                          | function            | no       | all      | yes               |
| headerStatusBarHeight          | Extra padding to add at the top of header to account for translucent status bar.                                           | number              | no       | all      | yes               |


**Header Components Props**

| Name               | Description                                                                                                                  | Type     | Required | Platform | HarmonyOS Support |
|--------------------|------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| HeaderBackground   | A component containing the styles used in the background of the header, such as the background color and shadow.             | function | no       | all      | yes               |
| HeaderTitle        | A component used to show the title text in header. It's the default for headerTitle. It accepts the same props as a Text.    | function | no       | all      | yes               |
| HeaderBackButton   | A component used to show the back button header. It's the default for headerLeft in the stack navigator.                     | function | no       | all      | yes               |
| MissingIcon        | A component that renders a missing icon symbol. It can be used as a fallback for icons to show that there's a missing icon.  | function | no       | all      | yes               |
| PlatformPressable  | A component which provides an abstraction on top of Pressable to handle platform differences.                                | function | no       | all      | yes               |
| ResourceSavingView | A component which aids in improving performance for inactive screens by utilizing removeClippedSubviews.                     | function | no       | all      | yes               |

**Utilities**
| Name                   | Description                                                                                                       | Type     | Required | Platform | HarmonyOS Support |
|------------------------|-------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| SafeAreaProviderCompat | A wrapper over the SafeAreaProvider component from `react-native-safe-area-context which includes initial values. | function | no       | all      | yes               |
| HeaderBackContext      | React context that can be used to get the back title of the parent screen.                                        | function | no       | all      | yes               |
| HeaderShownContext     | React context that can be used to check if a header is visible in a parent screen.                                | function | no       | all      | yes               |
| HeaderHeightContext    | React context that can be used to get the height of the nearest visible header in a parent screen.                | function | no       | all      | yes               |
| useHeaderHeight        | Hook that returns the height of the nearest visible header in the parent screen.                                  | function | no       | all      | yes               |
| getDefaultHeaderHeight | Helper that returns the default header height.                                                                    | function | no       | all      | yes               |
| getHeaderTitle         | Helper that returns the title text to use in header.                                                              | function | no       | all      | yes               |    


## 遗留问题

## 其他

示例代码依赖以下三方库，请查看对应文档：
+ [@react-navigation/stack](/zh-cn/react-navigation-stack.md)
+ [@react-navigation/native](/zh-cn/react-navigation-native.md)
+ [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
+ [@react-native-oh-library/react-native-safe-area-context](/zh-cn/react-native-safe-area-context.md)
  
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/elements/LICENSE) ，请自由地享受和参与开源。