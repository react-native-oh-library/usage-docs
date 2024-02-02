> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-reanimated</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-reanimated">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-reanimated)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-tpl/react-native-reanimated Releases](https://github.com/react-native-oh-library/react-native-reanimated/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-reanimated@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-reanimated@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, Text } from "react-native";
import { interpolate } from "react-native-reanimated";

export default function App() {
  return (
    <View
      style={{
        flex: 1,
        backgroundColor: "violet",
      }}
    >
      <Text>{interpolate(0, [-200, 200], [1, 0])}</Text>
    </View>
  );
}
```

## 约束与限制

### 兼容性

> [!WARNING] 本库的动画功能尚未实现，请关注之后发布的版本。

本文档内容基于以下版本验证通过：

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见 [react-native-reanimated 源库地址](https://github.com/software-mansion/react-native-reanimated)

### Components

This Animated object wraps React Native built-ins such as View,Text,ScrollView,Image or FlatList.

| Name                | Description                                                          | Type      | Required | Platform        | HarmonyOS Support |
| ------------------- | -------------------------------------------------------------------- | --------- | -------- | --------------- | ----------------- |
| Animated.View       | This Animated object wraps React Native built-ins such as View       | component | No       | iOS Android Web | No                |
| Animated.Text       | This Animated object wraps React Native built-ins such as Text       | component | No       | iOS Android Web | No                |
| Animated.ScrollView | This Animated object wraps React Native built-ins such as ScrollView | component | No       | iOS Android Web | No                |
| Animated.Image      | This Animated object wraps React Native built-ins such as Image      | component | No       | iOS Android Web | No                |
| Animated.FlatList   | This Animated object wraps React Native built-ins such as FlatList   | component | No       | iOS Android Web | No                |

### Animations

| Name         | Description                                                                                                                                                                                                 | Type     | Required | Platform        | HarmonyOS Support |
| ------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | --------------- | ----------------- |
| withTiming   | lets you create an animation based on duration and easing.                                                                                                                                                  | Function | No       | iOS Android Web | No                |
| withSpring   | lets you create spring-based animations.                                                                                                                                                                    | Function | No       | iOS Android Web | No                |
| withDecay    | lets you create animations that mimic objects in motion with friction. The animation will start with the provided velocity and slow down over time according to the given deceleration rate until it stops. | Function | No       | iOS Android Web | No                |
| withSequence | withSequence is an animation modifier that lets you run animations in a sequence.                                                                                                                           | Function | No       | iOS Android Web | No                |
| withRepeat   | withRepeat is an animation modifier that lets you repeat an animation given number of times or run it indefinitely.                                                                                         | Function | No       | iOS Android Web | No                |
| withDelay    | withDelay is an animation modifier that lets you start an animation with a delay.                                                                                                                           | Function | No       | iOS Android Web | No                |
| withClamp    | withClamp is an animation modifier that lets you limit the scope of movement of your animation to make it stay within some predefined range. Use it with withSpring animation.                              | Function | No       | iOS Android Web | No                |

### Core

| Name                    | Description                                                                                                                                                                                                                 | Type     | Required | Platform        | HarmonyOS Support |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | --------------- | ----------------- |
| useSharedValue          | useSharedValue lets you define shared values in your components.                                                                                                                                                            | Function | No       | iOS Android Web | No                |
| useAnimatedStyle        | useAnimatedStyle lets you create a styles object, similar to StyleSheet styles, which can be animated using shared values.                                                                                                  | Function | No       | iOS Android Web | No                |
| useAnimatedProps        | useAnimatedProps lets you create an animated props object which can be animated using shared values. This object is used to animate properties of third-party components.                                                   | Function | No       | iOS Android Web | No                |
| useAnimatedRef          | useAnimatedRef lets you get a reference of a view. Used alongside measure, scrollTo, and useScrollViewOffset functions.                                                                                                     | Function | No       | iOS Android Web | No                |
| useDerivedValue         | useDerivedValue lets you create new shared values based on existing ones while keeping them reactive.                                                                                                                       | Function | No       | iOS Android Web | No                |
| createAnimatedComponent | createAnimatedComponent lets you create an Animated version of any React Native component. Wrapping a component with createAnimatedComponent allows Reanimated to animate any prop or style associated with that component. | Function | No       | iOS Android Web | No                |
| cancelAnimation         | cancelAnimation lets you cancel a running animation paired to a shared value.                                                                                                                                               | Function | No       | iOS Android Web | No                |

### Scroll

| Name                     | Description                                                                                                                                                        | Type     | Required | Platform        | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | --------------- | ----------------- |
| scrollTo                 | scrollTo lets you synchronously scroll to a given X or Y offset.                                                                                                   | Function | No       | iOS Android Web | No                |
| useScrollViewOffset      | useScrollViewOffset lets you to create animations based on the offset of a ScrollView. The hook automatically detects if the ScrollView is horizontal or vertical. | Function | No       | iOS Android Web | No                |
| useAnimatedScrollHandler | This is a convenience hook that returns an event handler reference which can be used with React Native's scrollable components.                                    | Function | No       | iOS Android Web | No                |

### Device

| Name                | Description                                                                                      | Type     | Required | Platform        | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------------------ | -------- | -------- | --------------- | ----------------- |
| useAnimatedKeyboard | With the useAnimatedKeyboard hook, you can create animations based on current keyboard position. | Function | No       | iOS Android Web | No                |
| useAnimatedSensor   | lets you create animations based on data from the device's sensors.                              | Function | No       | iOS Android Web | No                |
| useReducedMotion    | lets you query the reduced motion system setting. You can use it to disable animations.          | Function | No       | iOS Android Web | No                |

### Layout Animations

| Name                  | Description                                                                                                        | Type                                                  | Required | Platform        | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------------------ | ----------------------------------------------------- | -------- | --------------- | ----------------- |
| FadeIn                | FadeIn lets you create a fading animation.                                                                         | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeInRight           | FadeInRight lets you create a fading animation.                                                                    | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeInLeft            | FadeInLeft lets you create a fading animation.                                                                     | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeInUp              | FadeInUp lets you create a fading animation.                                                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeInDown            | FadeInDown lets you create a fading animation.                                                                     | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeOut               | FadeOut lets you create a fading animation.                                                                        | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeOutRight          | FadeOutRight lets you create a fading animation.                                                                   | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeOutLeft           | FadeOutLeft lets you create a fading animation.                                                                    | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeOutUp             | FadeOutUp lets you create a fading animation.                                                                      | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FadeOutDown           | FadeOutDown lets you create a fading animation.                                                                    | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceIn              | BounceIn lets you create a bouncing animation.                                                                     | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceInRight         | BounceInRight lets you create a bouncing animation.                                                                | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceInLeft          | BounceInLeft lets you create a bouncing animation.                                                                 | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceInUp            | BounceInUp lets you create a bouncing animation.                                                                   | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceInDown          | BounceInDown lets you create a bouncing animation.                                                                 | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceOut             | BounceOut lets you create a bouncing animation.                                                                    | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceOutRight        | BounceOutRight lets you create a bouncing animation.                                                               | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceOutLeft         | BounceOutLeft lets you create a bouncing animation.                                                                | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceOutUp           | BounceOutUp lets you create a bouncing animation.                                                                  | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| BounceOutDown         | BounceOutDown lets you create a bouncing animation.                                                                | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipInEasyX           | FlipInEasyX lets you create animation based on rotation over specific axis.                                        | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipInEasyY           | FlipInEasyY lets you create animation based on rotation over specific axis.                                        | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipInXDown           | FlipInXDown lets you create animation based on rotation over specific axis.                                        | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipInXUp             | FlipInXUp lets you create animation based on rotation over specific axis.                                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipInYLeft           | FlipInYLeft lets you create animation based on rotation over specific axis.                                        | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipInYRight          | FlipInYRight lets you create animation based on rotation over specific axis.                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipOutEasyX          | FlipOutEasyX lets you create animation based on rotation over specific axis.                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipOutEasyY          | FlipOutEasyY lets you create animation based on rotation over specific axis.                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipOutXDown          | FlipOutXDown lets you create animation based on rotation over specific axis.                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipOutXUp            | FlipOutXUp lets you create animation based on rotation over specific axis.                                         | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipOutYLeft          | FlipOutYLeft lets you create animation based on rotation over specific axis.                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| FlipOutYRight         | FlipOutYRight lets you create animation based on rotation over specific axis.                                      | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| LightSpeedInRight     | LightSpeedInRight lets you create an animation of a horizontally moving object with a change of opacity and skew.  | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| LightSpeedInLeft      | LightSpeedInLeft lets you create an animation of a horizontally moving object with a change of opacity and skew.   | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| LightSpeedOutRight    | LightSpeedOutRight lets you create an animation of a horizontally moving object with a change of opacity and skew. | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| LightSpeedOutLeft     | LightSpeedOutLeft lets you create an animation of a horizontally moving object with a change of opacity and skew.  | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| PinwheelIn            | PinwheelIn lets you create an animation based on rotation, scale, and opacity.                                     | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| PinwheelOut           | PinwheelOut lets you create an animation based on rotation, scale, and opacity.                                    | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RollInRight           | RollInRight lets you create an animation of a horizontally moving object with a rotation.                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RollInLeft            | RollInLeft lets you create an animation of a horizontally moving object with a rotation.                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RollOutRight          | RollOutRight lets you create an animation of a horizontally moving object with a rotation.                         | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RollOutLeft           | RollOutLeft lets you create an animation of a horizontally moving object with a rotation.                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateInDownLeft      | RotateInDownLeft lets you create a rotation animation.                                                             | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateInDownRight     | RotateInDownRight lets you create a rotation animation.                                                            | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateInUpLeft        | RotateInUpLeft lets you create a rotation animation.                                                               | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateInUpRight       | RotateInUpRight lets you create a rotation animation.                                                              | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateOutDownLeft     | RotateOutDownLeft lets you create a rotation animation.                                                            | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateOutDownRight    | RotateOutDownRight lets you create a rotation animation.                                                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateOutUpLeft       | RotateOutUpLeft lets you create a rotation animation.                                                              | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| RotateOutUpRight      | RotateOutUpRight lets you create a rotation animation.                                                             | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideInRight          | SlideInRight lets you create an animation of horizontal or vertical moving object.                                 | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideInLeft           | SlideInLeft lets you create an animation of horizontal or vertical moving object.                                  | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideInUp             | SlideInUp lets you create an animation of horizontal or vertical moving object.                                    | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideInDown           | SlideInDown lets you create an animation of horizontal or vertical moving object.                                  | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideOutRight         | SlideOutRight lets you create an animation of horizontal or vertical moving object.                                | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideOutLeft          | SlideOutLeft lets you create an animation of horizontal or vertical moving object.                                 | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideOutUp            | SlideOutUp lets you create an animation of horizontal or vertical moving object.                                   | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| SlideOutDown          | SlideOutDown lets you create an animation of horizontal or vertical moving object.                                 | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| StretchInX            | StretchInX lets you create an animation based on scaling in X or Y axis.                                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| StretchInY            | StretchInY lets you create an animation based on scaling in X or Y axis.                                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| StretchOutX           | StretchOutX lets you create an animation based on scaling in X or Y axis.                                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| StretchOutY           | StretchOutY lets you create an animation based on scaling in X or Y axis.                                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomIn                | ZoomIn lets you create an animation based on scale.                                                                | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInDown            | ZoomInDown lets you create an animation based on scale.                                                            | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInEasyDown        | ZoomInEasyDown lets you create an animation based on scale.                                                        | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInEasyUp          | ZoomInEasyUp lets you create an animation based on scale.                                                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInLeft            | ZoomInLeft lets you create an animation based on scale.                                                            | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInRight           | ZoomInRight lets you create an animation based on scale.                                                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInRotate          | ZoomInRotate lets you create an animation based on scale.                                                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomInUp              | ZoomInUp lets you create an animation based on scale.                                                              | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOut               | ZoomOut lets you create an animation based on scale.                                                               | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutDown           | ZoomOutDown lets you create an animation based on scale.                                                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutEasyDown       | ZoomOutEasyDown lets you create an animation based on scale.                                                       | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutEasyUp         | ZoomOutEasyUp lets you create an animation based on scale.                                                         | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutLeft           | ZoomOutLeft lets you create an animation based on scale.                                                           | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutRight          | ZoomOutRight lets you create an animation based on scale.                                                          | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutRotate         | ZoomOutRotate lets you create an animation based on scale.                                                         | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| ZoomOutUp             | ZoomOutUp lets you create an animation based on scale.                                                             | BaseAnimationBuilder                                  | No       | iOS Android Web | No                |
| Keyframe              | define complex animation using simple and popular animation definitions schema                                     | InnerKeyframe as unknown as typeof ReanimatedKeyframe | No       | iOS Android Web | No                |
| LayoutAnimationConfig | LayoutAnimationConfig is a component that lets you skip entering and exiting animations.                           | Component                                             | No       | iOS Android Web | No                |

### Threading

| Name                 | Description                                                                                                                                 | Type     | Required | Platform        | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | --------------- | ----------------- |
| runOnJS              | runOnJS lets you asynchronously run non-workletized functions that couldn't otherwise run on the UI thread.                                 | Function | No       | iOS Android Web | No                |
| runOnUI              | runOnUI lets you asynchronously run workletized functions on the UI thread.                                                                 | Function | No       | iOS Android Web | No                |
| createWorkletRuntime | createWorkletRuntime lets you create a new JS runtime which can be used to run worklets possibly on different threads than JS or UI thread. | Function | No       | iOS Android     | No                |

### Utilities

| Name              | Description                                                                                                                                                                               | Type     | Required | Platform        | HarmonyOS Support |
| ----------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | --------------- | ----------------- |
| interpolate       | interpolate lets you map a value from one range to another using linear interpolation.                                                                                                    | Function | No       | iOS Android Web | Yes               |
| clamp             | clamp lets you limit a value within a specified range.                                                                                                                                    | Function | No       | iOS Android Web | Yes               |
| interpolateColor  | Maps input range to output colors using linear interpolation.                                                                                                                             | Function | No       | iOS Android Web | No                |
| getRelativeCoords | Determines the location on the screen, relative to the given view. It might be useful when there are only absolute coordinates available and you need coordinates relative to the parent. | Function | No       | iOS Android Web | No                |

### Advanced APIs

| Name                | Description                                                                                                                                                                                                                           | Type     | Required | Platform        | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | --------------- | ----------------- |
| measure             | measure lets you synchronously get the dimensions and position of a view on the screen, all on the UI thread.                                                                                                                         | Function | No       | iOS Android Web | No                |
| useAnimatedReaction | useAnimatedReaction allows you to respond to changes in a shared value. It's especially useful when comparing values previously stored in the shared value with the current one.                                                      | Function | No       | iOS Android Web | No                |
| useFrameCallback    | useFrameCallback lets you run a function on every frame update.                                                                                                                                                                       | Function | No       | iOS Android Web | No                |
| useEvent            | This is low-level hook returning event handler that will be invoked with native events, which should be used in order to create custom event handler hook like useAnimatedGestureHandler or useAnimatedScrollHandler.                 | Function | No       | iOS Android Web | No                |
| useHandler          | This is low-level hook returning context object and value indicating whether worklet should be rebuilt, which should be used in order to create custom event handler hook like useAnimatedGestureHandler or useAnimatedScrollHandler. | Function | No       | iOS Android Web | No                |
| dispatchCommand     | Allows to dispatch command on a native component synchronously from the UI thread.                                                                                                                                                    | Function | No       | iOS Android Web | No                |
| setNativeProps      | setNativeProps lets you imperatively update component properties.                                                                                                                                                                     | Function | No       | iOS Android Web | No                |

## 遗留问题

- 目前仅验证了部分纯 js 方法，HarmonyOS Native 层暂未适配。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/software-mansion/react-native-reanimated/blob/main/LICENSE) ，请自由地享受和参与开源。