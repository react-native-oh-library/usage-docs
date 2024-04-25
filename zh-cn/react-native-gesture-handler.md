> 模板版本：v0.1.3

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

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-gesture-handler)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-gesture-handler Releases](https://github.com/react-native-oh-library/react-native-gesture-handler/releases)，并下载适用版本的 tgz 包。

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

快速使用：

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
                        new Animated.Value(-circleRadius),
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

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-gesture-handler": "file:../../node_modules/@react-native-oh-tpl/react-native-gesture-handler/harmony/gesture_handler.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-gesture-handler": "file:../../node_modules/@react-native-oh-tpl/react-native-gesture-handler/harmony/gesture_handler"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 GestureHandlerPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-gesture-handler/src/main/cpp" ./gesture-handler)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_gesture_handler)
# RNOH_END: link_packages
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

### 在 ArkTs 侧引入 gesture-handler 组件

react-native-gesture-handler 在 2.x 版本里，不再从原生端引入 `<GestureHandlerRootView>`，而是在 JS 端添加。详情请看官方说明：[Migrating off RNGHEnabledRootView](https://docs.swmansion.com/react-native-gesture-handler/docs/guides/migrating-off-rnghenabledroot)。

鸿蒙支持 1.x 在原生端替换 `RootView` 来添加 `<GestureHandlerRootView>` 的方式。

**如果使用 2.x 方式，则把后面带有 `1.x` 注释的代码删掉即可**

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { RNGestureHandlerRootView, RNGestureHandlerButton } from "rnoh-gesture-handler"
+ import { RNGestureHandlerModule } from 'rnoh-gesture-handler/src/main/ets/RNGestureHandlerModule'  // 1.x

  @Builder
  function buildCustomRNComponent(ctx: ComponentBuilderContext) {
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnComponentContext,
        tag: ctx.tag,
        buildCustomComponent: buildCustomComponent
      })
    }
+   else if (ctx.componentName == RNGestureHandlerRootView.NAME){
+     RNGestureHandlerRootView({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomRNComponent
+     })
+   } else if (ctx.componentName == RNGestureHandlerButton.NAME){
+     RNGestureHandlerButton({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomRNComponent
+     })
+   }
    ...
  }
  ...
  build() {
    Column() {
      if (this.rnAbility && this.shouldShow) {
        RNApp({
+         onSetUp: (rnInstance) => {  // 1.x
+           rnInstance.bindComponentNameToDescriptorType(RNGestureHandlerRootView.NAME, "RootView")  // 1.x
+           rnInstance.getTurboModule<RNGestureHandlerModule>(RNGestureHandlerModule.NAME).install()  // 1.x
+         },  // 1.x
          ...
        })
      }
    }
    .height('100%')
    .width('100%')
  }
```

### 在 ArkTs 侧引入 Gesture Handler Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { GestureHandlerPackage } from 'rnoh-gesture-handler/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GestureHandlerPackage(ctx),
  ];
}
```

### 运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-gesture-handler Releases](https://github.com/react-native-oh-library/react-native-gesture-handler/releases)

> [!tip] [官方文档](https://docs.swmansion.com/react-native-gesture-handler/docs/)

## Gestures

### Gesture detector

GestureDetector 是 Gesture Handler 库 2.x 版本的一个主要组件。

#### Gesture detector 属性

| 名称       | 说明                                                                                             | 类型                                 | 是否必填 | 原库平台 | 鸿蒙支持 |
| ---------- | ------------------------------------------------------------------------------------------------ | ------------------------------------ | -------- | -------- | -------- |
| gesture    | A gesture object containing the configuration and callbacks.                                     | base gestures or any ComposedGesture | yes      | All      | yes      |
| userSelect | This parameter allows to specify which userSelect property should be applied to underlying view. | ("none" \| "auto" \| "text")         | no       | Web      | no       |

目前 GestureDetector 支持:

`Gesture.Tap() `

Creates a new instance of [TapGesture](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/tap-gesture) with its default config and no callbacks.

`Gesture.Pan()`

Creates a new instance of [PanGesture](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/pan-gesture) with its default config and no callbacks.

## Components

### Touchables

Gesture Handler 库提供了一种基于原生按钮的 React Native touchable 组件的实现，它不依赖于 React Native 的 JS responder system。这些组件的实现遵循相同的API，旨在替代 React Native 中的 touchable 组件

目前支持：

- [Touchable Opacity](https://reactnative.dev/docs/touchableopacity)

- [Touchable Without Feedback](https://reactnative.dev/docs/touchablewithoutfeedback)

## Gesture handlers(legacy)

> [!WARNING] Consider using the new [gestures API](https://docs.swmansion.com/react-native-gesture-handler/docs/gestures/gesture) instead. The old API is not actively supported and is not receiving the new features. Check out [RNGH 2.0 section in Introduction](https://docs.swmansion.com/react-native-gesture-handler/docs/#rngh-20) for more information.

### Gesture handlers 通用属性

| 名称                    | 说明                                                                                                                                              | 类型                         | 是否必填 | 原库平台 | 鸿蒙支持 |
| ----------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------- | -------- | -------- | -------- |
| enabled                 | Indicates whether the given handler should be analyzing stream of touch events or not.                                                            | boolean                      | no       | All      | yes      |
| shouldCancelWhenOutside | When true the handler will cancel or fail recognition (depending on its current state) whenever the finger leaves the area of the connected view. | boolean                      | no       | All      | no       |
| cancelsTouchesInView    | When true, the handler will cancel touches for native UI components (UIButton, UISwitch, etc) it's attached to when it becomes ACTIVE.            | boolean                      | no       | iOS      | no       |
| simultaneousHandlers    | When set, the handler will be allowed to activate even if one or more of the handlers provided by their refs are in an ACTIVE state.              | refs                         | no       | All      | no       |
| waitFor                 | When set the handler will not activate as long as the handlers provided by their refs are in the BEGAN state.                                     | refs                         | no       | All      | no       |
| hitSlop                 | This parameter enables control over what part of the connected view area can be used to begin recognizing the gesture.                            | object                       | no       | All      | yes      |
| userSelect              | This parameter allows to specify which userSelect property should be applied to underlying view.                                                  | ("none" \| "auto" \| "text") | no       | Web      | no       |
| activeCursor            | This parameter allows to specify which cursor should be used when gesture activates.                                                              | CSS cursor values            | no       | Web      | no       |
| onGestureEvent          | Takes a callback that is going to be triggered for each subsequent touch event while the handler is in an ACTIVE state.                           | callback                     | no       | All      | yes      |
| onHandlerStateChange    | Takes a callback that is going to be triggered when state of the given handler changes.                                                           | callback                     | no       | All      | yes      |

### Gesture handlers 通用事件数据

以下是提供给 `onGestureEvent` 和 `onHandlerStateChange` 回调的通用事件数据:

| 名称             | 说明                                                                        | 类型   | 原库平台 | 鸿蒙支持 |
| ---------------- | --------------------------------------------------------------------------- | ------ | -------- | -------- |
| state            | Current state of the handler.                                               | State  | All      | yes      |
| numberOfPointers | Represents the number of pointers (fingers) currently placed on the screen. | number | All      | yes      |

### PanGestureHandler

#### PanGestureHandler 属性

| 名称                           | 说明                                                                                                                                                                                        | 类型    | 是否必填 | 原库平台 | 鸿蒙支持 |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | -------- | -------- |
| minDist                        | Minimum distance the finger (or multiple finger) need to travel before the handler activates.                                                                                               | number  | no       | All      | yes      |
| minPointers                    | A number of fingers that is required to be placed before handler can activate.                                                                                                              | number  | no       | All      | yes      |
| maxPointers                    | When the given number of fingers is placed on the screen and handler hasn't yet activated it will fail recognizing the gesture.                                                             | number  | no       | All      | yes      |
| activeOffsetX                  | Range along X axis (in points) where fingers travels without activation of handler.                                                                                                         | number  | no       | All      | yes      |
| activeOffsetY                  | Range along Y axis (in points) where fingers travels without activation of handler.                                                                                                         | number  | no       | All      | yes      |
| failOffsetY                    | When the finger moves outside this range (in points) along Y axis and handler hasn't yet activated it will fail recognizing the gesture.                                                    | number  | no       | All      | yes      |
| failOffsetX                    | When the finger moves outside this range (in points) along X axis and handler hasn't yet activated it will fail recognizing the gesture. Range can be given as an array or a single number. | number  | no       | All      | yes      |
| maxDeltaX                      | This method is deprecated but supported for backward compatibility. Instead of using maxDeltaX={N} you can do failOffsetX={[-N, N]}.                                                        | number  | no       | All      | yes      |
| maxDeltaY                      | This method is deprecated but supported for backward compatibility. Instead of using maxDeltaY={N} you can do failOffsetY={[-N, N]}.                                                        | number  | no       | All      | yes      |
| minOffsetX                     | This method is deprecated but supported for backward compatibility. Instead of using minOffsetX={N} you can do activeOffsetX={N}.                                                           | number  | no       | All      | yes      |
| minOffsetY                     | This method is deprecated but supported for backward compatibility. Instead of using minOffsetY={N} you can do activeOffsetY={N}.                                                           | number  | no       | All      | yes      |
| minDeltaX                      | This method is deprecated but supported for backward compatibility. Instead of using minDeltaX={N} you can do activeOffsetX={[-N, N]}.                                                      | number  | no       | All      | yes      |
| minDeltaY                      | This method is deprecated but supported for backward compatibility. Instead of using minDeltaY={N} you can do activeOffsetY={[-N, N]}.                                                      | number  | no       | All      | yes      |
| avgTouches                     | Android, by default, will calculate translation values based on the position of the leading pointer (the first one that was placed on the screen).                                          | number  | no       | Android  | no       |
| enableTrackpadTwoFingerGesture | Enables two-finger gestures on supported devices, for example iPads with trackpads.                                                                                                         | boolean | no       | iOS      | no       |

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

| 名称          | 说明                                                                                                                               | 类型   | 是否必填 | 原库平台 | 鸿蒙支持 |
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

- 手势只支持 Pan 和 Tap 手势；
- 组件只支持 Touchables

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-linear-gradient/blob/harmony/LICENSE) ，请自由地享受和参与开源。
