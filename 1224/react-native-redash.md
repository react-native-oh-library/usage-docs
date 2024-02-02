> 模板版本：v14.2.2

<p align="center">
  <h1 align="center"> <code>react-native-redash</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wcandillon/react-native-redash/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://wcandillon.gitbook.io/redash/)

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

下面的代码展示了这个库的基本使用场景：

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
### 兼容性

在下述版本验证通过:
  1. IDE:Deveco Studio 4.1.3.412;
     SDK: OpenHarmony (Api11) 4.1.0.53;
     测试设备: Mate40 Pro (NOH-AN00);
     ROM: 2.0.0.52 (SP22C00E52R1P17log);
     RNOH: 0.72.11。

## 静态方法

详情查看[redash官方文档](https://github.com/wcandillon/react-native-redash)

如下是已验证接口展示:

 #### **Animations**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| defineAnimation() | This utility function enables you to declare custom animations that can be invoked on both the JS and UI thread. | function | NO | NO |
| animationParameter(animation) | Access animations passed as parameters safely on both the UI and JS thread with the proper static types. Animations can receive other animations as parameter | function | NO | NO |
| withPause() | Make an animation pausable. The state of the animation (paused or not) is controlled by a boolean shared value. | function | NO | NO |
| withBouncing() | Add a bouncing behavior to a physics-based animation. An animation is defined as being physics-based if it contains a velocity in its state. | function | NO | NO |

#### **Coordinates**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| canvas2Cartesian() | Convert plane coordinate system to Cadir coordinate system | function | NO | yes |
| cartesian2Canvas() |  Convert Kadir coordinate system to plane coordinate system | NO | yes |
| cartesian2Polar() | Conversion from Kadir coordinate system to polar coordinate system | function | NO | yes |
| polar2Cartesian() | Convert polar coordinate system to Cadir coordinate system | function | NO | yes |
| polar2Canvas() | Convert polar coordinate system to Cadir coordinate system  | function | NO | yes |
| canvas2Polar() | Convert plane coordinate system to polar coordinate system  | function | NO | yes |

#### **Strings**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| <ReText /> | This component is like <Text> but accepts a string animation node as property. Behind the scene, <ReText> is using <TextInput> with some default styling. Therefore there might be some slight inconsistencies with <Text>. | function | NO | NO |

#### **Math**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| mix() | mix performs a linear interpolation between x and y using a to weight between them. The return value is computed as x * (1 - value) + y * value | function | NO | yes |
| bin() | Convert a boolean value into a number. This can be useful in reanimated since 0 and 1 are used for conditional statements. | function | NO | yes | Math |
| toRad() | Transforms an angle from degrees to radians. | function | NO | yes |
| toDeg() | Transforms an angle from radians to degrees. | function | NO | yes |
| clamp() | Clamps a node with a lower and upper bound. | function | NO | yes |
| avg() | Returns the average value of an array | function | NO | yes | Math |
| between() | Returns true if node is within lowerBound and upperBound. | function | NO | yes |
| round() | Computes animation node rounded to precision. | function | NO | yes |
| cubicBezier() | Returns the coordinate of a cubic bezier curve. t is the length of the curve from 0 to 1. cubicBezier(0, p0, p1, p2, p3) equals p0 and cubicBezier(1, p0, p1, p2, p3) equals p3. p0 and p3 are respectively the starting and ending point of the curve. p1 and p2 are the control points. | function | NO | yes |
| cubicBezierYForX() | Given a cubic Bèzier curve, return the y value for x | function | NO | NO |

#### **Transitions**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| useTiming() | Transitions can attach an animation value to a change of React state. | function | NO | NO |
| useSpring() | Transitions can attach an animation value to a change of React state. | function | NO | NO |

#### **Vectors**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| useVector() | Returns a vector of shared values. | function | NO | NO |

#### **Paths**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| createPath(path, {x, y}) | Create a new path | function | NO | NO |
| addCurve(path, {c1: {x, y}, c2: {x, y}, to: {x, y}}) | Add a Bèzier curve command to a path | function | NO | NO |
| close(path) | Add a close command to a path. | function | NO | NO |
| parse(path) | Parse an SVG path into a sequence of Bèzier curves. The SVG is normalized to have absolute values and to be approximated to a sequence of Bèzier curves. | function | NO | NO |
| serialize(path) | Serialize a path into an SVG path string. | function | NO | NO |
| interpolatePath() | Interpolate between paths.| function | NO | NO |

#### **Physics**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| snapPoint() | Select a point where the animation should snap to given the value of the gesture and it's velocity. | function | NO | NO |

#### **Colors**

| Name | Description | Type | Required | HarmonyOS Support |
| ---- | ---- | ---- | -------- | -------- |
| mixColor() | Identical to interpolateColor() but with an animation value that goes from 0 to 1. | function | NO | NO |

## 遗留问题
Animations、Strings、Transitions、Vectors、Paths、Physics、Colors等
部分接口依赖react-native-reanimated实现，目前react-native-reanimated暂不支持，所以无法实现。  
## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wcandillon/react-native-redash/blob/master/LICENSE) ，请自由地享受和参与开源。
