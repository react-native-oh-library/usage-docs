> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-gesture-handler</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/software-mansion/react-native-gesture-handler">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/software-mansion/react-native-gesture-handler/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-gesture-handler Releases](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-gesture-handler@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-gesture-handler@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component } from "react";
import { Animated, Dimensions } from "react-native";
import {
  GestureHandlerRootView,
  PanGestureHandler,
} from "react-native-gesture-handler";

const { width } = Dimensions.get("screen");
const circleRadius = 30;

class Circle extends Component {
  _touchX = new Animated.Value(width / 2 - circleRadius);

  _onPanGestureEvent = Animated.event([{ nativeEvent: { x: this._touchX } }], {
    useNativeDriver: true,
  });

  render() {
    return (
      <GestureHandlerRootView>
        <PanGestureHandler onGestureEvent={this._onPanGestureEvent}>
          <Animated.View
            style={{
              height: 150,
              justifyContent: "center",
            }}
          >
            <Animated.View
              style={[
                {
                  backgroundColor: "#42a5f5",
                  borderRadius: circleRadius,
                  height: circleRadius * 2,
                  width: circleRadius * 2,
                },
                {
                  transform: [
                    {
                      translateX: Animated.add(
                        this._touchX,
                        new Animated.Value(-circleRadius)
                      ),
                    },
                  ],
                },
              ]}
            />
          </Animated.View>
        </PanGestureHandler>
      </GestureHandlerRootView>
    );
  }
}

export default function App() {
  return <Circle />;
}
```

## 使用Codegen

本库未带rc.x的版本号是已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

> [!TIP] 引入原生代码之前请确认IDE版本，5.0.3.810及其之后的版本需要在harmony工程中的hvigor-config.json5文件中新增如下配置以解决路径过长导致的编译报错问题
> "properties":{
          "ohos.nativeResolver":false
}

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-gesture-handler": "file:../../node_modules/@react-native-oh-tpl/react-native-gesture-handler/harmony/gesture_handler.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 GestureHandlerPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-gesture-handler/src/main/cpp" ./gesture-handler)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_gesture_handler)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "GestureHandlerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<GestureHandlerPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 Gesture Handler Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import { GestureHandlerPackage } from '@react-native-oh-tpl/react-native-gesture-handler/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GestureHandlerPackage(ctx),
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-gesture-handler Releases](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/releases)

> [!tip] [官方文档](https://docs.swmansion.com/react-native-gesture-handler/docs/)

## Gestures

### Gesture detector

GestureDetector 是 Gesture Handler 库 2.x 版本的一个主要组件。

#### Gesture detector 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                                                  | Type                             | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- | -------- |
| gesture    | A gesture object containing the configuration and callbacks.                                     | base gestures or any ComposedGesture | yes      | All      | yes      |

#### Gesture 的方法
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| method | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| Gesture.Tap() | Creates a new instance of [TapGesture](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/tap-gesture) with its default config and no callbacks. | function() | All      | yes    |
| Gesture.Pan() | Creates a new instance of [PanGesture](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/pan-gesture) with its default config and no callbacks. | function() | All      | yes    |
| Gesture.Rotation() | Creates a new instance of [`RotationGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/rotation-gesture) with its default config and no callbacks. | function() | All      | yes    |
| Gesture.LongPress() | Creates a new instance of [`LongPressGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/long-press-gesture) with its default config and no callbacks. | function() | All      | yes    |
| Gesture.Manual() | Creates a new instance of [`ManualGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/manual-gesture) with its default config and no callbacks. | function() | All      | yes    |
| Gesture.Pinch() | Creates a new instance of [`PinchGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/pinch-gesture) with its default config and no callbacks. | function() | All      | yes    |
| Gesture.Fling() | Creates a new instance of [`FlingGesture`](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/fling-gesture) with its default config and no callbacks. | function() | All      | yes    |

## Components

### Touchables

Gesture Handler 库提供了一种基于原生按钮的 React Native touchable 组件的实现，它不依赖于 React Native 的 JS responder system。这些组件的实现遵循相同的 API，旨在替代 React Native 中的 touchable 组件,HarmonyOS 已全面支持。

- [Touchable Opacity](https://reactnative.dev/docs/touchableopacity)
- [Touchable Without Feedback](https://reactnative.dev/docs/touchablewithoutfeedback)
- [Touchable Highlight](https://reactnative.dev/docs/touchablehighlight)
- [Touchable Native Feedback](https://reactnative.dev/docs/touchablenativefeedback)

### Buttons

BaseButton 属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| onActiveStateChange | that gets triggered when button changes from inactive to active and vice versa. | function | All   | yes   |
| onPress | that gets triggered when the button gets pressed | function | All   | yes   |
| onLongPress | that gets triggered when the button gets pressed for at least `delayLongPress` milliseconds. | function | All   | yes   |
| exclusive | defines if more than one button could be pressed simultaneously. By default set `true`. | boolean | All   | yes   |
| delayLongPress | defines the delay, in milliseconds, after which the `onLongPress` callback gets called. By default set to 600. | number | All   | yes   |

ReactButton 属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| underlayColor | this is the background color that will be dimmed when button is in active state. | Color | All   | yes   |

### Drawer Layout

属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| drawerType | A gesture object                                     | 'front'\|'back'\|'slide' | All | yes |
| edgewidth | allows for defining how far from the edge of the content view the gesture should activate. | number | All   | yes   |
| hideStatusBar | when set to `true` Drawer component will use [StatusBar](https://reactnative.dev/docs/statusbar.html) API to hide the OS status bar whenever the drawer is pulled or when its in an "open" state. | boolean | All   | yes   |
| statusbaranimation | Can be used when `hideStatusBar` is set to `true` and will select the animation used for hiding/showing the status bar. | 'fade'\|'slide'\|'none' | All   | yes   |
| overlaycolor | of a semi-transparent overlay to be displayed on top of the content view when drawer gets open. | color | All   | yes   |
| rendernavigationview | his attribute is present in the standard implementation already and is one of the required params. | function | All   | yes   |
| ondrawerclose | This function is called when the drawer is closed. | function | All   | yes   |
| ondraweropen | This function is called when the drawer is opened. | function | All   | yes   |
| ondrawerslide | his function is called as a drawer sliding open from touch events. | function | All   | yes   |
| ondrawerstatechanged | This function is called when the status of the drawer changes. | function | All   | yes   |
| children | Children is a component which is rendered by default and is wrapped by drawer. | component\| function | All   | yes   |

### Swipeable

属性
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| friction | a number that specifies how much the visual interaction will be delayed compared to the gesture distance. | number | All | yes |
| leftThreshold | distance from the left edge at which released panel will animate to the open state | number | All | yes |
| rightThreshold | distance from the right edge at which released panel will animate to the open state | number | All | yes |
| dragOffsetFromLeftEdge | distance that the panel must be dragged from the left edge to be considered a swipe. | number                   | All | yes |
| dragOffsetFromRightEdge | distance that the panel must be dragged from the right edge to be considered a swipe. | number | All | yes |
| overshootLeft | a boolean value indicating if the swipeable panel can be pulled further than the left actions panel's width. | boolean | All | yes |
| overshootRight | a boolean value indicating if the swipeable panel can be pulled further than the right actions panel's width. I | boolean | All | yes |
| overshootFriction | a number that specifies how much the visual interaction will be delayed compared to the gesture distance at overshoot. | number                   | All | yes |
| onSwipeableOpen | method that is called when action panel gets open | function(direction: 'left' \| 'right', swipeable: Swipeable) | All | yes |
| onSwipeableClose | method that is called when action panel is closed. | function(direction: 'left' \| 'right', swipeable: Swipeable) | All | yes |
| onSwipeableWillOpen | Called when action panel starts animating on open (either right or left). | function((direction: 'left' \| 'right')) | All | yes |
| onSwipeableWillClose | Called when action panel starts animating on close. | function((direction: 'left' \| 'right')) | All | yes |
| renderLeftActions | This map describes the values to use as inputRange for extra interpolation: AnimatedValue: [startValue, endValue] | function(progressAnimatedValue: AnimatedInterpolation,<br/>    dragAnimatedValue: AnimatedInterpolation,<br/>    swipeable: Swipeable) | All | yes |
| renderRightActions | method that is expected to return an action panel that is going to be revealed from the right side when user swipes left. | function(progressAnimatedValue: AnimatedInterpolation,<br/>    dragAnimatedValue: AnimatedInterpolation,<br/>    swipeable: Swipeable) | All | yes |
| containerStyle | style object for the container (Animated.View), for example to override `overflow: 'hidden'`. | StyleProp<ViewStyle> | All | yes |
| childrenContainerStyle | style object for the children container (Animated.View), for example to apply `flex: 1`. | StyleProp<ViewStyle> | All | yes |


## Gesture handlers(legacy)

> [!WARNING] Consider using the new [gestures API](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/gesture) instead. The old API is not actively supported and is not receiving the new features. Check out [RNGH 2.0 section in Introduction](https://docs.swmansion.com/react-native-gesture-handler/docs/#rngh-20) for more information.

### Gesture handlers 通用属性
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME                | Description                                                                                                                                   | TYPE                     | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | -------- | -------- | -------- |
| enabled                 | Indicates whether the given handler should be analyzing stream of touch events or not.                                                            | boolean                      | no       | All      | yes      |
| hitSlop                 | This parameter enables control over what part of the connected view area can be used to begin recognizing the gesture.                            | object                       | no       | All      | yes      |
| onGestureEvent          | Takes a callback that is going to be triggered for each subsequent touch event while the handler is in an ACTIVE state.                           | callback                     | no       | All      | yes      |
| onHandlerStateChange    | Takes a callback that is going to be triggered when state of the given handler changes.                                                           | callback                     | no       | All      | yes      |

### Gesture handlers 通用事件数据

以下是提供给 `onGestureEvent` 和 `onHandlerStateChange` 回调的通用事件数据:
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME         | Description                                                             | TYPE | Platform | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------- | ------ | -------- | -------- |
| state            | Current state of the handler.                                               | State  | All      | yes      |
| numberOfPointers | Represents the number of pointers (fingers) currently placed on the screen. | number | All      | yes      |

### PanGestureHandler

#### PanGestureHandler 属性
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME                       | Description                                                                                                                                                                             | TYPE | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | -------- | -------- |
| minDist                        | Minimum distance the finger (or multiple finger) need to travel before the handler activates.                                                                                               | number  | no       | All      | yes      |
| minPointers                    | A number of fingers that is required to be placed before handler can activate.                                                                                                              | number  | no       | All      | yes      |
| maxPointers                    | When the given number of fingers is placed on the screen and handler hasn't yet activated it will fail recognizing the gesture.                                                             | number  | no       | All      | yes      |
| activeOffsetX                  | Range along X axis (in points) where fingers travels without activation of handler.                                                                                                         | number  | no       | All      | yes      |
| activeOffsetY                  | Range along Y axis (in points) where fingers travels without activation of handler.                                                                                                         | number  | no       | All      | yes      |

#### PanGestureHandler 事件数据

请到查看[基础 handler 类的通用事件数据](#gesture-handlers-通用事件数据)。以下是 PanGestureHandler 特有的事件数据。

`translationX`

Translation of the pan gesture along X axis accumulated over the time of the gesture. The value is expressed in the point units.

`translationY`

Translation of the pan gesture along Y axis accumulated over the time of the gesture. The value is expressed in the point units.

`velocityX`

Velocity of the pan gesture along the X axis in the current moment. The value is expressed in point units per second.

`velocityY`

Velocity of the pan gesture along the Y axis in the current moment. The value is expressed in point units per second.

`x`

X coordinate of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the view attached to the handler. Expressed in point units.

`y`

Y coordinate of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the view attached to the handler. Expressed in point units.

### TapGestureHandler

#### TapGestureHandler 属性
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME      | Description                                                                                                                    | TYPE | Required | Platform | HarmonyOS Support |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| minPointers   | Minimum number of pointers (fingers) required to be placed before the handler activates.                                           | number | no       | All      | yes      |
| maxDurationMs | Maximum time, expressed in milliseconds, that defines how fast a finger must be released after a touch.                            | number | no       | All      | yes      |
| maxDelayMs    | Maximum time, expressed in milliseconds, that can pass before the next tap — if many taps are required.                            | number | no       | All      | yes      |
| maxDeltaX     | Maximum distance, expressed in points, that defines how far the finger is allowed to travel along the X axis during a tap gesture. | number | no       | All      | yes      |
| maxDeltaY     | Maximum distance, expressed in points, that defines how far the finger is allowed to travel along the Y axis during a tap gesture. | number | no       | All      | yes      |
| maxDist       | Maximum distance, expressed in points, that defines how far the finger is allowed to travel during a tap gesture.                  | number | no       | All      | yes      |

#### TapGestureHandler 事件数据

请到查看[基础 handler 类的通用事件数据](#gesture-handlers-通用事件数据)。以下是 TapGestureHandler 特有的事件数据。

`x`

X coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the view attached to the handler.

`y`

Y coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the view attached to the handler.

`absoluteX`

X coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the window. It is recommended to use absoluteX instead of x in cases when the view attached to the handler can be transformed as an effect of the gesture.

`absoluteY`

Y coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the window. It is recommended to use absoluteY instead of y in cases when the view attached to the handler can be transformed as an effect of the gesture.

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE) ，请自由地享受和参与开源。
