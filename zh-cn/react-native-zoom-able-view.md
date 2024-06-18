> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-zoomable-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/openspacelabs/react-native-zoomable-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/openspacelabs/react-native-zoomable-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/openspacelabs/react-native-zoomable-view)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @openspacelabs/react-native-zoomable-view@2.1.6
```

#### **yarn**

```bash
yarn add @openspacelabs/react-native-zoomable-view@2.1.6
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, StyleSheet, Image, Animated } from "react-native";
import React from "react";
import { ReactNativeZoomableView } from "@openspacelabs/react-native-zoomable-view";

export function ReactNativeZoomableViewExample() {
  const zoomAnimatedValue = React.useRef(new Animated.Value(1)).current;
  const scale = Animated.divide(1, zoomAnimatedValue);
  return (
    <View style={styles.container}>
      <View style={styles.box}>
        <ReactNativeZoomableView
          maxZoom={30}
          initialZoom={1.5}
          contentWidth={300}
          contentHeight={150}
          panBoundaryPadding={500}
          style={{ padding: 10, backgroundColor: "red" }}
        >
          <View style={styles.contents}>
            <Image
              style={styles.img}
              source={require("../assets/placeholder2000x2000.jpg")}
            />

            {[20, 40, 60, 80].map((left) =>
              [20, 40, 60, 80].map((top) => (
                <Animated.View
                  key={`${left}x${top}`}
                  style={[
                    styles.marker,
                    { left: `${left}%`, top: `${top}%` },
                    { transform: [{ scale }] },
                  ]}
                />
              ))
            )}
          </View>
        </ReactNativeZoomableView>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
    padding: 20,
  },
  contents: {
    flex: 1,
    alignSelf: "stretch",
  },
  box: {
    borderWidth: 5,
    flexShrink: 1,
    height: 500,
    width: 310,
  },
  img: {
    width: "100%",
    height: "100%",
    resizeMode: "contain",
  },
  marker: {
    position: "absolute",
    top: "50%",
    left: "50%",
    width: 20,
    height: 20,
    marginLeft: -10,
    marginTop: -10,
    borderRadius: 10,
    backgroundColor: "white",
    borderWidth: 2,
  },
});
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.26; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.25;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Type     | Description                                                      | Required | Platform | HarmonyOS Support |
| -------------------------- | -------- | ---------------------------------------------------------------- | -------- | -------- | ----------------- |
| zoomEnabled                | boolean  | Can be used to enable or disable the zooming dynamically                                                                                                                                                                                                                                                                             | no       | All      | yes               |
| panEnabled                 | boolean  | Can be used to enable or disable the panning dynamically                                                                                                                                                                                                                                                                             | no       | All      | yes               |
| initialZoom                | number   | Initial zoom level on startup                                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| maxZoom                    | number   | Maximum possible zoom level (zoom in). Can be set to`null` to allow unlimited zooming                                                                                                                                                                                                                                                | no       | All      | yes               |
| minZoom                    | number   | Minimum possible zoom level (zoom out)                                                                                                                                                                                                                                                                                               | no       | All      | yes               |
| disablePanOnInitialZoom    | boolean  | If true, panning is disabled when zoom level is equal to the initial zoom level                                                                                                                                                                                                                                                      | no       | All      | yes               |
| doubleTapDelay             | number   | How much delay will still be recognized as double press (ms)                                                                                                                                                                                                                                                                         | no       | All      | yes               |
| doubleTapZoomToCenter      | boolean  | If true, double tapping will always zoom to center of View instead of the direction it was double tapped in                                                                                                                                                                                                                          | no       | All      | yes               |
| bindToBorders              | boolean  | If true, it makes sure the object stays within box borders                                                                                                                                                                                                                                                                           | no       | All      | yes               |
| zoomStep                   | number   | How much zoom should be applied on double tap                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| pinchToZoomInSensitivity   | number   | the level of resistance (sensitivity) to zoom in (0 - 10) - higher is less sensitive                                                                                                                                                                                                                                                 | no       | All      | yes               |
| pinchToZoomOutSensitivity  | number   | the level of resistance (sensitivity) to zoom out (0 - 10) - higher is less sensitive                                                                                                                                                                                                                                                | no       | All      | yes               |
| movementSensibility        | number   | how resistant should shifting the view around be? (0.5 - 5) - higher is less sensitive                                                                                                                                                                                                                                               | no       | All      | yes               |
| initialOffsetX             | number   | The horizontal offset the image should start at                                                                                                                                                                                                                                                                                      | no       | All      | yes               |
| initialOffsetY             | number   | The vertical offset the image should start at                                                                                                                                                                                                                                                                                        | no       | All      | yes               |
| contentHeight              | number   | Specify if you want to treat the height of the**centered** content inside the zoom subject as the zoom subject's height                                                                                                                                                                                                              | no       | All      | yes               |
| contentWidth               | number   | Specify if you want to treat the width of the**centered** content inside the zoom subject as the zoom subject's width                                                                                                                                                                                                                | no       | All      | yes               |
| panBoundaryPadding         | number   | At certain scales, the edge of the content is bounded too close to the edge of the container, making it difficult to pan to and interact with the edge of the content. To fix this, we'd wanna allow the content to pan just a little further away from the container's edge. Hence, the "pan boundary padding", measured in pixels. | no       | All      | yes               |
| longPressDuration          | number   | Duration in ms until a press is considered a long press                                                                                                                                                                                                                                                                              | no       | All      | yes               |
| visualTouchFeedbackEnabled | boolean  | Whether to show a touch feedback circle on touch                                                                                                                                                                                                                                                                                     | no       | All      | yes               |
| onTransform                | function | Will be called when the transformation configuration (zoom level and offset) changes                                                                                                                                                                                                                                                 | no       | All      | yes               |
| onDoubleTapBefore          | function | Will be called, at the start of a double tap                                                                                                                                                                                                                                                                                         | no       | All      | yes               |
| onDoubleTapAfter           | function | Will be called at the end of a double tap                                                                                                                                                                                                                                                                                            | no       | All      | yes               |
| onShiftingBefore           | function | Will be called, when user taps and moves the view, but before our view movement work kicks in (so this is the place to interrupt movement, if you need to)                                                                                                                                                                           | no       | All      | yes               |
| onShiftingAfter            | function | Will be called, when user taps and moves the view, but after the values have changed already                                                                                                                                                                                                                                         | no       | All      | yes               |
| onShiftingEnd              | function | Will be called, when user stops a tap and move gesture                                                                                                                                                                                                                                                                               | no       | All      | yes               |
| onZoomBefore               | function | Will be called, while the user pinches the screen, but before our zoom work kicks in (so this is the place to interrupt zooming, if you need to)                                                                                                                                                                                     | no       | All      | yes               |
| onZoomAfter                | function | Will be called, while the user pinches the screen, but after the values have changed already                                                                                                                                                                                                                                         | no       | All      | yes               |
| onZoomEnd                  | function | Will be called after pinchzooming has ended                                                                                                                                                                                                                                                                                          | no       | All      | yes               |
| onLongPress                | function | Will be called after the user pressed on the image for a while                                                                                                                                                                                                                                                                       | no       | All      | yes               |
| onStartShouldSetPanResponder                     | function |     Determines whether the view group responds to touch events when a finger is pressed.      | no       | All      | yes               |                                                                                                                                                                                                                                                                | no       | All      | yes               |
| onPanResponderGrant                     | function |     The gesture has started      | no       | All      | yes               |                                                                                                                                                                                                                                                                | no       | All      | yes               |
| onPanResponderEnd                     | function |    Will be called when gesture ends (more accurately, on pan responder "release")       | no       | All      | yes               |                                                                                                                                                                                                                                                                | no       | All      | yes               |
| onPanResponderTerminate                     | function |    Will be called when the gesture is force-interrupted by another handler       | no       | All      | yes               |                                                                                                                                                                                                                                                                | no       | All      | yes               |
| onPanResponderTerminationRequest                     | function |    Callback asking whether the gesture should be interrupted by another handler       | no       | IOSs      | yes               |                                                                                                                                                                                                                                                                | no       | All      | yes               |
| onPanResponderMove                     | function |    Will be called when user moves while touching       | no       | All      | yes               |                                                                                                                                                                                                                                                                | no       | All      | yes               |
| onShouldBlockNativeResponder                     | function |   Returns whether this component should block native components from becoming the JS responder   | no       | All      | yes               |

| zoomTo                     | function | Changes the zoom level to a specific number                                                                                                                                                                                                                                                                                          | no       | All      | yes               |
| zoomBy                     | function | Changes the zoom level relative to the current level (use positive numbers to zoom in, negative numbers to zoom out)                                                                                                                                                                                                                 | no       | All      | yes               |
| moveTo                     | function | Shifts the zoomed part to a specific point (in px relative to x: 0, y: 0)                                                                                                                                                                                                                                                            | no       | All      | yes               |
| moveBy                     | function | Shifts the zoomed part by a specific pixel number                                                                                                                                                                                                                                                                                    | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/openspacelabs/react-native-zoomable-view/blob/master/LICENSE) ，请自由地享受和参与开源。
