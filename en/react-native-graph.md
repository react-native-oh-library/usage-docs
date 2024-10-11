> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-graph</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/margelo/react-native-graph">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/margelo/react-native-graph/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/margelo/react-native-graph)

## 安装与使用


进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install react-native-graph@1.1.0
```

#### **yarn**

```bash
yarn add react-native-graph@1.1.0
```

下面的代码展示了这个库的基本使用场景：

```ts
import React, {  useState } from 'react'
import { View, StyleSheet, Text, Button } from 'react-native'
import { LineGraph } from 'react-native-graph'
import { GestureHandlerRootView } from 'react-native-gesture-handler';

interface GraphPoint {
    value: number
    date: Date
  }
interface GraphXRange {
    min: Date;
    max: Date;
}
interface GraphYRange {
    min: number;
    max: number;
}
interface GraphPathRange {
    x: GraphXRange;
    y: GraphYRange;
}
type GraphRange = Partial<GraphPathRange>;
type Color = string | Float32Array | number | number[];

export default function() {
    const generateRandomGraphData=(length: number): GraphPoint[]=>{
        return Array<number>(length)
          .fill(0)
          .map((_, index) => ({
            date: new Date(
              new Date(2000, 0, 1).getTime() + 1000 * 60 * 60 * 24 * index
            ),
            value: Math.random()*10,
          }))
      }
    const POINT_COUNT=50
      const POINTS = generateRandomGraphData(POINT_COUNT)
      const [points, setPoints] = useState(POINTS)
      const [isAnimated, setIsAnimated] = useState(true)
      const [enablePanGesture, setEnablePanGesture] = useState(false)

      const color='#dd4400'
  
      
    return (
        <View style={{ flex: 1 }}>
    <GestureHandlerRootView style={{ flex: 1 }}>
        <Text>{`enablePanGesture value is ${enablePanGesture}`}</Text>
        <LineGraph 
        style={styles.graph}
        animated={isAnimated}
        color={color}
        points={points}
        enablePanGesture={enablePanGesture}
        />
        <Button title='change enablePanGesture' onPress={()=>setEnablePanGesture(!enablePanGesture)} />
     </GestureHandlerRootView>
    </View>
    )

}

const styles = StyleSheet.create({

    graph: {
        alignSelf: 'center',
        width: '100%',
        aspectRatio: 1.4,
        marginVertical: 20,
      },
})
```
## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated , @react-native-oh-tpl/react-native-gesture-handler , @react-native-oh-tpl/react-native-skia 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated文档](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-gesture-handler文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-skia文档](/zh-cn/react-native-skia.md)、进行引入
## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.28; SDK：HarmonyOS NEXT Developer Beta5 5.0.0.60; IDE：DevEco Studio 5.0.3.655; ROM：3.0.0.60

2. RNOH：0.72.31; SDK：HarmonyOS NEXT Beta1 SDK 5.0.0.68; IDE：DevEco Studio 5.0.3.810; ROM：5.0.0.60

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                          | Description                                     | Type     | Required | Platform    | HarmonyOS Support |
| ----------------------------- | ----------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| `animated` | Whether to animate between data changes             | Boolean   | yes       | iOS/Android | yes               |
| `points` | All points to be marked in the graph. Coordinate system will adjust to scale automatically.                   | GraphPoint[]   | yes       | iOS/Android | yes               |
| `color`| Color of the graph line (path)              | String   | yes       | iOS/Android | yes               |
| `enableFadeInMask` |Enable the Fade-In Gradient Effect at the beginning of the Graph| Boolean| no       | iOS/Android | yes               |
| `lineThickness` |The width of the graph line (path)| Number | no       | iOS/Android | yes               |
| `gradientFillColors` |(Optional) Colors for the fill gradient below the graph line| Color[] | no       | iOS/Android | yes               |
| `range` |Range of the graph's x and y-axis. The range must be greaterthan the range given by the points| GraphRange | no       | iOS/Android | yes               |
| `enablePanGesture`| Whether to enable the pan gesture.(animated Property must be true)              | Boolean   | no       | iOS/Android | yes               |
| `horizontalPadding` | Horizontal padding applied to graph, so the pan gesture dot doesn't get cut off horizontally(animated Property must be true)      | Number   | no       | iOS/Android | yes               |
| `verticalPadding`| Vertical padding applied to graph, so the pan gesture dot doesn't get cut off vertically(animated Property must be true) | Number  | no       | iOS/Android | yes               |
| `enableIndicator`| Enables an indicator which is displayed at the end of the graph(animated Property must be true)  | Boolean  | no       | iOS/Android | yes               |
| `indicatorPulsating`  | Let's the indicator pulsate(animated GraphEnableIndicator Property must be true) | Boolean  | no       | iOS/Android | yes               |
| `panGestureDelay`| Delay after which the pan gesture starts(animated enablePanGesture Property must be true)`}| Number  | no       | iOS/Android | yes               |
| `onPointSelected`  | Called for each point while the user is scrubbing/panning through the graph(animated enablePanGesture Property must be true)| (point: GraphPoint) => void | no       | iOS/Android | yes               |
| `onGestureStart` |Called once the user starts scrubbing/panning through the graph (animated enablePanGesture Property must be true)|  () => void | no       | iOS/Android | yes               |
| `onGestureEnd` |Called once the user stopped scrubbing/panning through the graph (animated enablePanGesture Property must be true)| () => void | no       | iOS/Android | yes               |
| `SelectionDot`|The element that renders the selection dot(animated enablePanGesture Property must be true)| React.ComponentType\<SelectionDotProps> \| null | no       | iOS/Android | yes               |
| `TopAxisLabel` |The element that gets rendered above the Graph (usually the "max" point/value of the Graph)(animated Property must be true)| React.ReactElement \| null | no       | iOS/Android | yes               |
| `BottomAxisLabel` |The element that gets rendered below the Graph (usually the "min" point/value of the Graph)(animated Property must be true)| React.ReactElement \| null | no       | iOS/Android | yes               |



## 遗留问题

## 其他
- react-native-graph 的animated属性 原库代码现在有问题 无论是false还是true，数据变化都是静态变化，没有动画效果，原库中有使用者提issue和PR，添加合入相应PR代码后才能动画正常[issue#111](https://github.com/margelo/react-native-graph/pull/111)
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/margelo/react-native-graph/blob/main/LICENSE) ，请自由地享受和参与开源。

