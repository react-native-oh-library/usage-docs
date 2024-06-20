> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-redash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wcandillon/react-native-redash/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/wcandillon/react-native-redash/)

## 安装与使用

#### **yarn**

```bash
yarn add react-native-redash@^18.1.3
```

#### **npm**

```bash
npm install react-native-redash@^18.1.3
```

<!-- tabs:end -->

redash库依赖react-native-reanimated动画库，为适配 HarmonyOS 环境，需要把库里的依赖改成@react-native-oh-tpl/react-native-reanimated。下面的代码展示了这个库的基本使用场景：

<!-- {% raw %} -->
```js
// findLastIndex 为例
import {
  mix,
  round,
  bin,
  cubicBezier,
  clamp,
  between,
  avg,
  toRad,
  toDeg} from 'react-native-redash/src/Math';
import {
  canvas2Cartesian,
  cartesian2Canvas,
  cartesian2Polar,
  polar2Cartesian
} from 'react-native-redash/src/Coordinates'

const mix = (value: number, x: number, y: number) => number
const bin: (value: boolean) => 0 | 1;
const toRad = (deg: number) => number;
const toDeg = (rad: number) => number;
const clamp = (value: number, lowerBound: number, upperBound: number) => number;
const avg = (values: number[]) => number;
const between = (value: number, lowerBound: number, upperBound: number, inclusive?: boolean) => boolean;
const round = (value: Animated.Adaptable<number>, precision: Animated.Adaptable<number> = 0) => Animated.Node<number>;
const cubicBezier = (t: number, p0: number, p1: number, p2: number, p3: number) => number;
const cartesian2Canvas: ({ x, y }: Vector, center: Vector) => Vector;
const cartesian2Polar: ({ x, y }: Vector, center: Vector) => { radius: number, theta: number };
const polar2Cartesian: ({ theta, radius }: PolarPoint) => Vector;
const polar2Canvas: ({ theta, radius }: PolarPoint, center: Vector) => Vector;
const canvas2Polar: ({ x, y }: Vector, center: Vector) => {
    theta: number;
    radius: number;
};
```

动画演示示例

1.位置移动演示动画，通过snapPoint运行指定的位置地点

```js
import { snapPoint } from "react-native-redash/src/Physics";
import {
  useSharedValue,
  withSequence,
  withTiming,
  withRepeat,
} from "@react-native-oh-tpl/react-native-reanimated";

const offset = useSharedValue(0);

const translateAnimatedStyles = useAnimatedStyle(() => {
  return {
    transform: [
      {
        translateX: offset.value * 2,
      },
    ],
  };
});

const translate = () => {
  offset.value = withSequence(
    withTiming(-snapPoint(96, 600, [0, 125, 393]), { duration: 1000 }),
    withRepeat(
      withTiming(snapPoint(96, 600, [0, 125, 393]), { duration: 1000 }),
      60,
      true,
    ),
    withTiming(0, { duration: 50 }),
  );
};
```

2.颜色渐变动画演示，通过mixColor进行颜色渐变

```js
import { mixColor } from "react-native-redash/src/Colors";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

const progress = useSharedValue(0);

const colorAnimatedStyle = useAnimatedStyle(() => {
  return {
    backgroundColor: mixColor(progress.value, "#b58df1", "#38ffb3"),
  };
});

const handleColorPress = () => {
  progress.value = withRepeat(
    withTiming(1 - progress.value, { duration: 1000 }),
    60,
    true,
  );
};
```

3.redash目前有两个动画辅助方法：useTiming、useSpring。useTiming可以使用贝塞尔曲线来进行运动,useSpring可以不将持续时间作为参数，而是由sprin物理特性作为运动轨迹。

```js
import { useTiming, useSpring } from "react-native-redash/src/Transitions";
import Animated from "@react-native-oh-tpl/react-native-reanimated";

const timing = useSpring(255, { duration: 1000 });
const spring = useTiming(255, { duration: 1000 });

const customSpringStyles = useAnimatedStyle(() => {
  return {
    transform: [
      {
        translateX: spring.value,
      },
    ],
  };
});

const customTimingStyles = useAnimatedStyle(() => {
  return {
    transform: [
      {
        translateX: timing.value,
      },
    ],
  };
});

return (
  <View>
    <Animated.View style={[styles.box, defaultSpringStyles]} />
    <Animated.View style={[styles.box, defaultTimingStyles]} />
  </View>
);
```

4.redash提供能接受字符串动画节点属性的文本组件

```js
import { ReText } from "react-native-redash";
import { useSharedValue } from "@react-native-oh-tpl/react-native-reanimated";

const price = useSharedValue(42);
const formattedPrice = useDerivedValue(() => `${price.value}`.toLocaleString());

return (
  <View>
    <ReText
      text={formattedPrice}
      style={{
        color: "#black",
        fontVariant: ["tabular-nums"],
        backgroundColor: "#38ffb3",
      }}
    />
  </View>
);
```
<!-- {% endraw %} -->

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated 文档的 Link 章节](/zh-cn/react-native-reanimated.md#link)进行引入

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.11;
   SDK：OpenHarmony(api11) 4.1.0.53;
   IDE：DevEco Studio 4.1.3.412;
   ROM：2.0.0.52;
2. RNOH：0.72.13;
   SDK：HarmonyOS NEXT Developer Preview1;
   IDE：DevEco Studio 4.1.3.500;
   ROM：2.0.0.59;

## 静态方法
> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

如下是已验证接口展示:

### **Animations**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| defineAnimation()             | This utility function enables you to declare custom animations that can be invoked on both the JS and UI thread.                                              | function | No       | iOS/Android               | yes               |
| animationParameter(animation) | Access animations passed as parameters safely on both the UI and JS thread with the proper static types. Animations can receive other animations as parameter | function | No       | iOS/Android               | yes               |
| withPause()                   | Make an animation pausable. The state of the animation (paused or not) is controlled by a boolean shared value.                                               | function | No       | iOS/Android               | yes               |
| withBouncing()                | Add a bouncing behavior to a physics-based animation. An animation is defined as being physics-based if it contains a velocity in its state.                  | function | No       | iOS/Android               | yes               |
### **Coordinates**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| canvas2Cartesian() | Convert plane coordinate system to Cadir coordinate system         | function | No       | iOS/Android               | yes               |
| cartesian2Canvas() | Convert Kadir coordinate system to plane coordinate system         | function | No       | iOS/Android               | yes               |
| cartesian2Polar()  | Conversion from Kadir coordinate system to polar coordinate system | function | No       | iOS/Android               | yes               |
| polar2Cartesian()  | Convert polar coordinate system to Cadir coordinate system         | function | No       | iOS/Android               | yes               |
| polar2Canvas()     | Convert polar coordinate system to Cadir coordinate system         | function | No       | iOS/Android               | yes               |
| canvas2Polar()     | Convert plane coordinate system to polar coordinate system         | function | No       | iOS/Android               | yes               |
### **Strings**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| ReText | This component is like <Text> but accepts a string animation node as property. Behind the scene, <ReText> is using <TextInput> with some default styling. Therefore there might be some slight inconsistencies with <Text>. | function | No       | iOS/Android               | yes               |
### **Math**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| mix()              | mix performs a linear interpolation between x and y using a to weight between them. The return value is computed as x _ (1 - value) + y _ value   | function       | No       | iOS/Android               | yes               |
| bin()              | Convert a boolean value into a number. This can be useful in reanimated since 0 and 1 are used for conditional statements.  | function | No       | iOS/Android               | yes               |
| toRad()            | Transforms an angle from degrees to radians| function | No       | iOS/Android               | yes               |
| toDeg()            | Transforms an angle from radians to degrees| function | No       | iOS/Android               | yes               |
| clamp()            | Clamps a node with a lower and upper bound  | function | No       | iOS/Android               | yes               |
| avg()              | Returns the average value of an array        | function | No       | iOS/Android               | yes               |
| between()          | Returns true if node is within lowerBound and upperBound| function | No       | iOS/Android               | yes               |
| round()            | Computes animation node rounded to precision  | function | No       | iOS/Android               | yes               |
| cubicBezier()      | Returns the coordinate of a cubic bezier curve. t is the length of the curve from 0 to 1. cubicBezier(0, p0, p1, p2, p3) equals p0 and cubicBezier(1, p0, p1, p2, p3) equals p3. p0 and p3 are respectively the starting and ending point of the curve. p1 and p2 are the control points. | function | No       | iOS/Android               | yes               |
| cubicBezierYForX() | Given a cubic Bèzier curve, return the y value for x  | function | No       | iOS/Android               | yes               |
### **Transitions**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| useTiming() | Transitions can attach an animation value to a change of React state. | function | No       | iOS/Android               | yes               |
| useSpring() | Transitions can attach an animation value to a change of React state. | function | No       | iOS/Android               | yes               |
### **Vectors**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| useVector() | Returns a vector of shared values. | function | No       | iOS/Android               | yes               |
### **Paths**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| createPath(path, {x, y})                             | Create a new path  | function | No       | iOS/Android               | yes               |
| addCurve(path, {c1: {x, y}, c2: {x, y}, to: {x, y}}) | Add a Bèzier curve command to a path | function | No       | iOS/Android               | yes               |
| close(path)                                          | Add a close command to a path | function | No       | iOS/Android               | yes               |
| parse(path)                                          | Parse an SVG path into a sequence of Bèzier curves. The SVG is normalized to have absolute values and to be approximated to a sequence of Bèzier curves. | function | No       | iOS/Android               | yes               |
| serialize(path)                                      | Serialize a path into an SVG path string | function | No       | iOS/Android               | yes               |
| interpolatePath()                                    | Interpolate between paths | function | No       | iOS/Android               | yes               |
### **Physics**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| snapPoint() | Select a point where the animation should snap to given the value of the gesture and it's velocity. | function | No       | iOS/Android               | yes               |
### **Colors**
|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
| mixColor() | Identical to interpolateColor() but with an animation value that goes from 0 to 1. | function | No       | iOS/Android               | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wcandillon/react-native-redash/blob/master/LICENSE) ，请自由地享受和参与开源。
