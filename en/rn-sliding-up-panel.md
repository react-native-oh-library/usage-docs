> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-sliding-up-panel</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/octopitus/rn-sliding-up-panel">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/octopitus/rn-sliding-up-panel/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/octopitus/rn-sliding-up-panel)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install rn-sliding-up-panel@2.4.6
```

#### **yarn**

```bash
yarn add rn-sliding-up-panel@2.4.6
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { createRef } from 'react';
import { StyleSheet, Text, View, Dimensions, Animated } from 'react-native';
import SlidingUpPanel from 'rn-sliding-up-panel';

const { height } = Dimensions.get('window')

export function SlidingUpPanelExample() {
  const panelRef = createRef<SlidingUpPanel>();
  const draggableRange = { top: height + 180 - 64, bottom: 180 }
  const _draggedValue = new Animated.Value(180);

  const { top, bottom } = draggableRange;

  const backgoundOpacity = _draggedValue.interpolate({
    inputRange: [height - 48, height],
    outputRange: [1, 0],
    extrapolate: "clamp"
  });

  const iconTranslateY = _draggedValue.interpolate({
    inputRange: [height - 56, height, top],
    outputRange: [0, 56, 180 - 32],
    extrapolate: "clamp"
  });

  const textTranslateY = _draggedValue.interpolate({
    inputRange: [bottom, top],
    outputRange: [0, 8],
    extrapolate: "clamp"
  });

  const textTranslateX = _draggedValue.interpolate({
    inputRange: [bottom, top],
    outputRange: [0, -112],
    extrapolate: "clamp"
  });

  const textScale = _draggedValue.interpolate({
    inputRange: [bottom, top],
    outputRange: [1, 0.7],
    extrapolate: "clamp"
  });

  return (
    <View style={styles.container}>
      <Text onPress={() => panelRef.current!.show(360)}>Show panel</Text>
      <SlidingUpPanel
        ref={panelRef}
        draggableRange={draggableRange}
        animatedValue={_draggedValue}
        snappingPoints={[360]}
        height={height + 180}
        friction={0.5}
      >
        <View style={styles.panel}>
          <Animated.View
            style={[
              styles.iconBg,
              {
                opacity: backgoundOpacity,
                transform: [{ translateY: iconTranslateY }]
              }
            ]}
          />
          <View style={styles.panelHeader}>
            <Animated.View
              style={{
                transform: [
                  { translateY: textTranslateY },
                  { translateX: textTranslateX },
                  { scale: textScale }
                ]
              }}
            >
              <Text style={styles.textHeader}>Sliding Up Panel</Text>
            </Animated.View>
          </View>
          <View style={styles.container}>
            <Text>Bottom sheet content</Text>
          </View>
        </View>
      </SlidingUpPanel>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#f8f9fa",
    alignItems: "center",
    justifyContent: "center"
  },
  panel: {
    flex: 1,
    backgroundColor: "white",
    position: "relative"
  },
  panelHeader: {
    height: 180,
    backgroundColor: "#b197fc",
    justifyContent: "flex-end",
    padding: 24
  },
  textHeader: {
    fontSize: 28,
    color: "#FFF"
  },
  icon: {
    alignItems: "center",
    justifyContent: "center",
    position: "absolute",
    top: -24,
    right: 18,
    width: 48,
    height: 48,
    zIndex: 1
  },
  iconBg: {
    backgroundColor: "#2b8a3e",
    position: "absolute",
    top: -24,
    right: 18,
    width: 48,
    height: 48,
    borderRadius: 24,
    zIndex: 1
  }
});

```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Props

| Name | Description | Type | Default | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| animatedValue | An **Animated.Value** number between the top and bottom of draggable range. This number represents the position of the panel. If you update this prop, the panel will correspondingly update to the frame at that progress value. Default to **Animated.Value(0)** (Hidden at bottom of screen). | Animated.Value | 0 | No | All | yes |
| draggableRange | Boundary limits for draggable area. `top` default to visible height of device, `bottom` default to 0. | {top: number, bottom: number} | 0 | No | All | yes |
| snappingPoints | Must be an incremental array of number and all values must be within the `top` & `bottom` of draggableRange. | number[] | null | No | All | yes |
| minimumVelocityThreshold | Velocity threshold in **pixel/s** to trigger the fling animation after you release finger. Default is 0.1. | number | 0.1 | No | All | yes |
| minimumDistanceThreshold | Distance threshold in **pixel** (virtual, not physical) to trigger the fling animation after you release finger. Default is 0.24. | number | 0.24 | No | All | yes |
| height | Height of panel. Typically this should equal to the top value of `draggablerange.` | number | null | No | All | yes |
| friction | Determines how quickly the fling animation settles down and stops. The higher the value, the faster the velocity decreases. Default is 0.998. | number | 0.998 | No | All | yes |
| backdropOpacity | Opacity of the backdrop when the panel is active. Default is 0.75. | number | 0.75 | No | All | yes |
| containerStyle | Custom style for the container. | Style | null | No | All | yes |
| backdropStyle | Custom style for the backdrop. | Style | null | No | All | yes |
| showBackdrop | Controls the visibility of backdrop. Default `true`. | boolean | true | No | All | yes |
| allowMomentum | If `false`, panel will not continue to move when you release your finger. | boolean | null | No | All | yes |
| allowDragging | Default `true`. Setting this to `false` to disable dragging. | boolean | true | No | All | yes |
| avoidKeyboard | If `true` every time animated value changes keyboard will be dismissed. Default `true`. | boolean | true | No | All | yes |
| onBackButtonPress | By default when you press back button (Android) the panel will be closed (Move to `bottom` position of `draggableRange`). Implement this function if you want to custom the behavior. Returning `true` means the event has been handled. | () => boolean | null | No | All | yes |
| onDragStart | Called when the panel is about to start dragging. | (position: number, gestureState: GestureState) => void | null | No | All | yes |
| onDragEnd | Called when you release your finger. | (position: number: gestureState: GestureState) => void | null | No | All | yes |
| onMomentumDragStart | Called when the momentum drag starts. Works exactly the same way of [ScrollView#onMomentumScrollBegin](https://facebook.github.io/react-native/docs/scrollview#onmomentumscrollbegin). | (position: number) => void | null | No | All | yes |
| onMomentumDragEnd | Called when the momentum drag ends. Works exactly the same way of [ScrollView#onMomentumScrollEnd](https://facebook.github.io/react-native/docs/scrollview#onmomentumscrollend). | (position: number) => void | null | No | All | yes |
| onBottomReached | Called when the panel is hidden / reaches the bottom of the screen. | () => void | null | No | All | yes |
| children | Accepts passing a function as component. Invoked with `dragHandlers` (that can be passed into another View like this `<View {...dragHandlers}>`) when the panel is mounted. Useful when you want only a part of your content becomes the drag handler. | React.Element \| Function | null | No | All | yes |

### Methods

| Name | Description | Type | Default | Required | Platform | HarmonyOS Support |
| --- | --- | --- | --- | --- | --- | --- |
| show | Calling `show()` without any parameter will showmove the panel to top position (of draggableRange). | Function(value?: number \| Object) | null | No | All | yes |
| hide | Move the panel to the bottom position of draggable range. Note: This method is triggered if you touch the backdrop (If it's visible). | Function | null | No | All | yes |
| scrollIntoView | Typically you don't need to use this method, But if an element is stuck under the keyboard or out of view, you can use this ensure it is visible within the viewable area. | Function(node: number) | null | No | All | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/octopitus/rn-sliding-up-panel/blob/master/LICENSE) ，请自由地享受和参与开源。
