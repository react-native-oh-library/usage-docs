> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-notifier</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/seniv/react-native-notifier">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/seniv/react-native-notifier/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


>[!TIP] [Github 地址](https://github.com/seniv/react-native-notifier)
## 安装与使用

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install react-native-notifier@2.0.0
```

#### **yarn**

```bash
yarn add react-native-notifier@2.0.0
```



下面的代码展示了这个库的基本使用场景：


```js
import * as React from 'react';
import { View, Text,SafeAreaView,TouchableOpacity } from "react-native";

import {Notifier, NotifierWrapper  } from 'react-native-notifier';

import { GestureHandlerRootView } from 'react-native-gesture-handler';

export const Notifier = () => {
  return (
 <>
<SafeAreaView style={{ flex: 1 }}>
 <GestureHandlerRootView style={{ flex: 1 }}>
   <NotifierWrapper>
     <TouchableOpacity  
         style={{
         alignItems: 'center',
         borderRadius: 5,
         marginHorizontal: 10,
         backgroundColor: '#007BFF',
         padding: 15,
         marginTop: 10,
         marginBottom:10
         }}
         onPress={() =>
         Notifier.showNotification({
         title: '基本测试',
         description: '基本测试',
        })
    }>
       <Text >onPress</Text>
     </TouchableOpacity>
   </NotifierWrapper>
 </GestureHandlerRootView>
</SafeAreaView>
 </>
)
};
```
## Link

本库 HarmonyOS 侧实现依赖 @react-native-oh-tpl/react-native-gesture-handler 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入
## 约束与限制
### 兼容性

本文档内容基于以下版本验证通过:

1. RNOH: 0.72.28; SDK: HarmonyOS-NEXT-DB1 5.0.0.31; IDE: DevEco Studio 5.0.3.500; ROM: 3.0.0.25;

## 属性

详细请查看 [react-native-notifier 的文档介绍](https://github.com/seniv/react-native-notifier)

Both `NotifierWrapper` and `NotifierRoot` receive the same props.

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| omitGlobalMethodsHookup  | If set to `true`, global `Notifier` methods will not control this component. It's useful in case you have more than one `NotifierWrapper` or `NotifierRoot` rendered. If enabled, the only way to display notifications is using refs. | Boolean  | yes | All      | No |
| useRNScreensOverlay  | use `FullWindowOverlay` component from `react-native-screens` library. If `true`, Notifier will be rendered above NativeStackNavigation modals and RN Modal on iOS. This Option will work only if `react-native-screens` library is installed. iOS Only. | Boolean  | yes | iOS      | No |
| rnScreensOverlayViewStyle  | Style that will be used for RN View that is inside of FullWindowOverlay. iOS Only. | ViewStyle  | yes | iOS      | No |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| showNotification  | Show notification with params. | Function  | yes | All      | yes |
| hideNotification  |Hide notification and run callback function when notification completely hidden. | Function  | yes | All      | yes |
| clearQueue  |Clear [notifications queue](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#queue-mode) and optionally hide currently displayed notification. Might be useful to run after logout, after which queued notifications should not be displayed.| Function  | yes | All      | yes |

### `showNotification`
```
Notifier.showNotification(params: object);
```

`params`

| Name                | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| title  | Title of notification. Passed to Component. | String| Yes | All  |Yes  |
| description |Description of notification. Passed to Component. | String | Yes | All    | Yes    |
| duration |Time after notification will disappear. Set to 0 to not hide notification automatically  | Number | No |All    | Yes   
| Component |Component of the notification body. You can use one of the [bin components](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components), or your [custom component](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#custom-component).  | Component | No |All    | Yes   
| componentProps | Additional props that are passed to Component. See all available props of built-in components in the [components section](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#components).  | Object | No |All    | Yes   
| containerStyle |tyles Object or a Function that will receive translateY: Animated.Value as first parameter and should return Styles that will be used in container. Using this parameter it is possible to create[ your own animations of the notification](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#custom-animations).   | bool |No | All    | Yes   
| containerProps | 	Props of Animated Container  | Object |No | All    | Yes  
| queueMode | Determines the order in which notifications are shown. Read more in the [Queue Mode](https://github.com/seniv/react-native-notifier/tree/main?tab=readme-ov-file#queue-mode) section.  | String |No | All    | Yes  
| swipeEnabled |Can notification be hidden by swiping it out | bool |No | All    | Yes  
| animationDuration | How fast notification will appear/disappear | Number |No | All    | Yes  
| showAnimationDuration | How fast notification will appear.   | Number |No | All    | Yes  
| hideAnimationDuration	 | How fast notification will disappear.| Number |No | All    | Yes 
| easing | Animation easing. Details:[easing](https://reactnative.dev/docs/easing)  | Easing |No | All    | Yes   
| showEasing | Show Animation easing.| Easing |No | All    | Yes   
| hideEasing |Hide Animation easing. | Easing |No | All    | Yes   
| onShown | Function called when entering animation is finished | () => void |No | All    | Yes  
| onStartHiding | Function called when notification started hiding | () => void |No | All    | Yes  
| onHidden |Function called when notification completely hidden | () => void |No | All    | Yes  
| onPress | Function called when user press on notification | () => void |No | All    | Yes  
| hideOnPress | Should notification hide when user press on it| Boolean |No | All    | Yes  
| swipePixelsToClose	 | How many pixels user should swipe-up notification to dismiss it | Number |No | All    | Yes  
| swipeEasing	 | Animation easing after user finished swiping | Easing |No | All    | Yes  
| swipeAnimationDuration	 | How fast should be animation after user finished swiping | Number |No | All    | Yes  
| translucentStatusBar	 | Add additional top padding that equals to StatusBar.currentHeight. Android Only. | Number |No | Android    | No  

### `hideNotification`
```
Notifier.hideNotification(onHiddenCallback?: (result: Animated.EndResult) => void);
```

### `clearQueue`
```
Notifier.clearQueue(hideDisplayedNotification?: boolean);
```

## Queue Mode

Queue mode is used to define the order in which the notification appears in case other notifications are being displayed at the moment.

For example, if you have some important information like chat messages and you want the user to see all the notifications, then you can use `standby` mode. Or if you want to display something like an error message, then you can use `reset` mode.

By default, `reset` mode is used, which means every new notification clears the queue and gets displayed immediately.

In most cases, you will probably use only `reset` or `standby` modes.

All possible modes:
| Mode                |   Effect                                          |                
| ------------------- | ------------------------------------ | 
| reset | Clear notification queue and immediately display the new notification. Used by default.
| standby | Add notification to the end of the queue.
| next | Put notification in the first place in the queue. Will be shown right after the current notification disappears.
| immediate | Similar to next, but also it will hide currently displayed notification.

## 静态方法
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### `NotifierComponents.Notifications`
Currently, there are 2 components out of the box. If none of them fits your needs, then you can easily create your [Custom Component].

| Name | Type | Default |  Description |  Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |  -------- |  ---- |  -------- | 
| title  | String | null  | Title of notification. | All | Yes
| description  | String | null  | Description of notification. | All | Yes
| componentProps.titleStyle  | TextStyle | null  | The style to use for rendering title. | All | Yes
| componentProps.descriptionStyle  | TextStyle | null  |The style to use for rendering description. | All | Yes
| componentProps.imageSource  | Object | null  | Passed to <Image /> as source param. | All | Yes
| componentProps.imageStyle  | ImageStyle | null  | The style to use for rendering image. | All | Yes
| componentProps.containerStyle  | ViewStyle | null  | The style to use for notification container. | All | Yes
| componentProps.ContainerComponent  | Component | SafeAreaView  | A container of the component. Set it in case you use different SafeAreaView than the standard | All | Yes
| componentProps.maxTitleLines  | number | null  | The maximum number of lines to use for rendering title. | All | Yes
| componentProps.maxDescriptionLines  | number | null  | The maximum number of lines to use for rendering description. | All | Yes

### `NotifierComponents.Alert`

| Name | Type | Default |  Description | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |  -------- | ---- |  -------- |
| title  | String | null  | Title of notification. |  All | Yes
| description  | String | null  | Description of notification. |  All | Yes
| componentProps.titleStyle  | TextStyle | null  | The style to use for rendering title. |  All | Yes
| componentProps.descriptionStyle  | TextStyle | null  |The style to use for rendering description. |  All | Yes
|componentProps.alertType  | String | 'success'  |Background color will be changed depending on the type. Available values: error(red), success(green), warn(orange) and info(blue). |  All | Yes
| componentProps.backgroundColor | String | null  | While the background of the alert depends on alertType, you can also set the other color you want. |  All | Yes
| componentProps.textColor  | String | 'white'  | Color of title and description. |  All | Yes
| componentProps.ContainerComponent  | Component | SafeAreaView  | A container of the component. Set it in case you use different SafeAreaView than the standard |  All | Yes
| componentProps.maxTitleLines  | number | null  | The maximum number of lines to use for rendering title. |  All | Yes
| componentProps.maxDescriptionLines  | number | null  | The maximum number of lines to use for rendering description. | All | Yes

## 遗留问题

- [ ] translucentStatusBar状态栏透明在HarmonyOS不支持,useRNScreensOverlay,rnScreensOverlayViewStyle两个属性依赖于react-native-screens，暂未适配harmonyOS  

## 其他

- omitGlobalMethodsHookup源库属性未生效 问题：[issues#102](https://github.com/seniv/react-native-notifier/issues/102) 
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/seniv/react-native-notifier/blob/main/LICENSE) ，请自由地享受和参与开源。
<!-- {% endraw %} -->