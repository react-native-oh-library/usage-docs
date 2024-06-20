> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-navigation/elements</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/elements">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/6.x/packages/elements/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig/packages/elements)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/elements Releases](https://github.com/react-native-oh-library/react-navigation/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/elements@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/elements@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { HeaderBackContext } from "@react-navigation/elements";
```

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-navigation Releases](https://github.com/react-native-oh-library/react-navigation/releases?q=elements&expanded=true)

## 属性

详细请查看 [react-navigation/elements 的文档介绍](https://reactnavigation.org/docs/elements/#resourcesavingview)

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**Header**：用作标头的组件

| Name                           | Description                               | Type                      | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------- | ------------------------- | -------- | -------- | ----------------- |
| headerTitle                    | 场景标题，或者返回一个 React 元素用作标题 | string \| React.reactNode | No       | All      | 未验证            |
| headerTitleAlign               | 标题对齐方式                              | left \| center            | No       | All      | 未验证            |
| headerTitleAllowFontScaling    | 标题是否缩放                              | boolean                   | No       | All      | 未验证            |
| headerLeft                     | 函数，返回一个 React 元素用在页眉左侧     | React.reactNode           | No       | All      | 未验证            |
| headerRight                    | 函数，返回一个 React 元素用在页眉右侧     | React.reactNode           | No       | All      | 未验证            |
| headerShadowVisible            | 是否显示阴影                              | boolean                   | No       | All      | 未验证            |
| headerStyle                    | 页眉样式                                  | ViewStyle                 | No       | All      | 未验证            |
| headerTitleStyle               | 页眉标题颜色                              | TextStyle                 | No       | All      | 未验证            |
| headerLeftContainerStyle       | headerLeft 容器的样式                     | ViewStyle                 | No       | All      | 未验证            |
| headerRightContainerStyle      | headerRight 容器的样式                    | ViewStyle                 | No       | All      | 未验证            |
| headerTitleContainerStyle      | headerTitle 容器的样式                    | ViewStyle                 | No       | All      | 未验证            |
| headerBackgroundContainerStyle | headerBackground 容器的样式               | ViewStyle                 | No       | All      | 未验证            |
| headerTintColor                | 页眉颜色                                  | string                    | No       | All      | 未验证            |
| headerPressColor               | 页眉按下颜色                              | string                    | No       | All      | 未验证            |
| headerPressOpacity             | 页眉按下不透明度                          | number                    | No       | All      | 未验证            |
| headerTransparent              | 页眉是否透明                              | boolean                   | No       | All      | 未验证            |
| headerBackground               | 函数，返回一个 React 元素对页眉背景渲染   | function                  | No       | All      | 未验证            |
| headerStatusBarHeight          | 页眉状态栏高度                            | number                    | No       | All      | 未验证            |

**HeaderBackground**：可用于 Header 的 headerBackground 属性

**HeaderTitle**：可用于 Header 的 headerTitle 属性

**HeaderBackButton**：用于显示后退按钮标题的组件

| Name               | Description                                     | Type            | Required | Platform | HarmonyOS Support |
| ------------------ | ----------------------------------------------- | --------------- | -------- | -------- | ----------------- |
| disabled           | 是否可用                                        | boolean         | No       | All      | 未验证            |
| onPress            | 点击事件                                        | function        | No       | All      | 未验证            |
| pressColor         | 点击时的颜色                                    | string          | No       | All      | 未验证            |
| backImage          | 函数，返回一个 React 元素用于后退按钮显示的图片 | React.reactNode | No       | All      | 未验证            |
| tintColor          | 按钮颜色                                        | string          | No       | All      | 未验证            |
| label              | 按钮的文本                                      | string          | No       | All      | 未验证            |
| truncatedLabel     | 空间不足时显示的文本                            | string          | No       | All      | 未验证            |
| labelVisible       | 文本是否可见                                    | boolean         | No       | All      | 未验证            |
| labelStyle         | 文本样式                                        | TextStyle       | No       | All      | 未验证            |
| allowFontScaling   | 文本是否根据字体缩放                            | boolean         | No       | All      | 未验证            |
| onLabelLayout      | 标签大小更改时要触发的回调。                    | function        | No       | All      | 未验证            |
| screenLayout       | 屏幕布局                                        | Layout          | No       | All      | 未验证            |
| titleLayout        | 标题中 title 元素的布局                         | Layout          | No       | All      | 未验证            |
| canGoBack          | 能否导航回来                                    | boolean         | No       | All      | 未验证            |
| accessibilityLabel | 屏幕阅读器按钮的辅助功能标签                    | string          | No       | All      | 未验证            |
| testID             | ID                                              | string          | No       | All      | 未验证            |
| style              | 按钮样式                                        | ViewStyle       | No       | All      | 未验证            |

**MissingIcon**：渲染丢失的图标符号的组件。它可以用作图标的回退，以显示缺少图标

| Name  | Description | Type      | Required | Platform | HarmonyOS Support |
| ----- | ----------- | --------- | -------- | -------- | ----------------- |
| color | icon 的颜色 | string    | No       | All      | 未验证            |
| size  | icon 的大小 | number    | No       | All      | 未验证            |
| style | icon 的样式 | TextStyle | No       | All      | 未验证            |

**PlatformPressable**：在[Pressable](https://reactnative.dev/docs/Pressable)之上提供抽象以处理平台差异的组件
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| pressColor | 按压时的颜色 | string | No | All | 未验证 |
| pressOpacity | 按压时的不透明度 | number | No | All | 未验证 |

**ResourceSavingView**：通过使用 removeClippedSubviews 来帮助提高非活动屏幕的性能的组件，它接受一个可见的道具来指示是否应该剪辑屏幕

**SafeAreaProviderCompat**：来自“react native safe-area context”的 SafeAreaProvider 组件的包装器

**HeaderBackContext**：React 上下文，可用于获取父屏幕的后标题

**HeaderShownContext**：React 上下文，可用于检查页眉在父屏幕中是否可见

**HeaderHeightContext**：React 上下文，可用于获取父屏幕中最近的可见页眉的高度

## 方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                     | Description                      | Type     | Required | Platform | HarmonyOS Support |
| ------------------------ | -------------------------------- | -------- | -------- | -------- | ----------------- |
| `useHeaderHeight`        | 返回父屏幕中最近的可见页眉的高度 | function | no       | All      | 未验证            |
| `getDefaultHeaderHeight` | 返回默认页眉高度                 | function | no       | All      | yes               |
| `getHeaderTitle`         | 返回页眉标题文本                 | function | no       | All      | 未验证            |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-navigation/react-navigation/blob/6.x/packages/elements/LICENSE) ，请自由地享受和参与开源。
