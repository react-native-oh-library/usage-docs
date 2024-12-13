> Template version: v0.2.2

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-gesture-handler Releases](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-gesture-handler
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-gesture-handler
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

this repository  release package that end with rc.x has been adapted to `Codegen` , generate the bridge code of the third-party library by using the `Codegen`. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

> [!TIP] 引入原生代码之前请确认IDE版本，5.0.3.810及其之后的版本需要在harmony工程中的hvigor-config.json5文件中新增如下配置以解决路径过长导致的编译报错问题
> "properties":{
>      "ohos.nativeResolver":false
> }

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP]  The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-gesture-handler": "file:../../node_modules/@react-native-oh-tpl/react-native-gesture-handler/harmony/gesture_handler.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md)

### 3. Configuring CMakeLists and Introducing GestureHandlerPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
+ #include "generated/RNOHGeneratedPackage.h"
+ #include "GestureHandlerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
+     std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<GestureHandlerPackage>(ctx)
    };
}
```

### 4. Introducing Gesture Handler Package to ArkTS

Open the`entry/src/main/ets/RNPackagesFactory.ts ` file and add the following code:

```diff
+ import { GestureHandlerPackage } from '@react-native-oh-tpl/react-native-gesture-handler/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GestureHandlerPackage(ctx),
  ];
}
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-gesture-handler Releases](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/releases)

> [!TIP] [Official Documentation](https://docs.swmansion.com/react-native-gesture-handler/docs/)

## Gestures

### Gesture detector

GestureDetector is a major component of the Gesture Handler library version 2.x.

#### Gesture detector Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                                                                                  | Type                             | Required | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- | -------- |
| gesture    | A gesture object containing the configuration and callbacks.                                     | base gestures or any ComposedGesture | yes      | All      | yes      |

#### Gesture Method
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

BaseButton Properties
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| onActiveStateChange | that gets triggered when button changes from inactive to active and vice versa. | function | All   | yes   |
| onPress | that gets triggered when the button gets pressed | function | All   | yes   |
| onLongPress | that gets triggered when the button gets pressed for at least `delayLongPress` milliseconds. | function | All   | yes   |
| exclusive | defines if more than one button could be pressed simultaneously. By default set `true`. | boolean | All   | yes   |
| delayLongPress | defines the delay, in milliseconds, after which the `onLongPress` callback gets called. By default set to 600. | number | All   | yes   |

ReactButton Properties
| Name | Description                                                                                  | Type                             | Platform | HarmonyOS Support |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- |
| underlayColor | this is the background color that will be dimmed when button is in active state. | Color | All   | yes   |

### Drawer Layout

Properties
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

Properties
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

### Gesture handlers General Properties
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME                | Description                                                                                                                                   | TYPE                     | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | -------- | -------- | -------- |
| enabled                 | Indicates whether the given handler should be analyzing stream of touch events or not.                                                            | boolean                      | no       | All      | yes      |
| hitSlop                 | This parameter enables control over what part of the connected view area can be used to begin recognizing the gesture.                            | object                       | no       | All      | yes      |
| onGestureEvent          | Takes a callback that is going to be triggered for each subsequent touch event while the handler is in an ACTIVE state.                           | callback                     | no       | All      | yes      |
| onHandlerStateChange    | Takes a callback that is going to be triggered when state of the given handler changes.                                                           | callback                     | no       | All      | yes      |

### Gesture handlers common event data

The following is the common event data for the `onGestureEvent` and `onHandlerStateChange` callbacks.
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME         | Description                                                             | TYPE | Platform | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------- | ------ | -------- | -------- |
| state            | Current state of the handler.                                               | State  | All      | yes      |
| numberOfPointers | Represents the number of pointers (fingers) currently placed on the screen. | number | All      | yes      |

### PanGestureHandler

#### PanGestureHandler Properties
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME                       | Description                                                                                                                                                                             | TYPE | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | -------- | -------- |
| minDist                        | Minimum distance the finger (or multiple finger) need to travel before the handler activates.                                                                                               | number  | no       | All      | yes      |
| minPointers                    | A number of fingers that is required to be placed before handler can activate.                                                                                                              | number  | no       | All      | yes      |
| maxPointers                    | When the given number of fingers is placed on the screen and handler hasn't yet activated it will fail recognizing the gesture.                                                             | number  | no       | All      | yes      |
| activeOffsetX                  | Range along X axis (in points) where fingers travels without activation of handler.                                                                                                         | number  | no       | All      | yes      |
| activeOffsetY                  | Range along Y axis (in points) where fingers travels without activation of handler.                                                                                                         | number  | no       | All      | yes      |

#### PanGestureHandler event data

Please refer to the [common event data for the basic handler class](#gesture-handlers-通用事件数据). The following is the event data specific to the  PanGestureHandler.

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

#### TapGestureHandler Properties
> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| NAME      | Description                                                                                                                    | TYPE | Required | Platform | HarmonyOS Support |
| ------------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | -------- |
| minPointers   | Minimum number of pointers (fingers) required to be placed before the handler activates.                                           | number | no       | All      | yes      |
| maxDurationMs | Maximum time, expressed in milliseconds, that defines how fast a finger must be released after a touch.                            | number | no       | All      | yes      |
| maxDelayMs    | Maximum time, expressed in milliseconds, that can pass before the next tap — if many taps are required.                            | number | no       | All      | yes      |
| maxDeltaX     | Maximum distance, expressed in points, that defines how far the finger is allowed to travel along the X axis during a tap gesture. | number | no       | All      | yes      |
| maxDeltaY     | Maximum distance, expressed in points, that defines how far the finger is allowed to travel along the Y axis during a tap gesture. | number | no       | All      | yes      |
| maxDist       | Maximum distance, expressed in points, that defines how far the finger is allowed to travel during a tap gesture.                  | number | no       | All      | yes      |

#### TapGestureHandler event data

Please refer to the [common event data for the basic handler class](#gesture-handlers-通用事件数据). The following is the event data specific to the TapGestureHandler.

`x`

X coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the view attached to the handler.

`y`

Y coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the view attached to the handler.

`absoluteX`

X coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the window. It is recommended to use absoluteX instead of x in cases when the view attached to the handler can be transformed as an effect of the gesture.

`absoluteY`

Y coordinate, expressed in points, of the current position of the pointer (finger or a leading pointer when there are multiple fingers placed) relative to the window. It is recommended to use absoluteY instead of y in cases when the view attached to the handler can be transformed as an effect of the gesture.

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE).
