> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>victory-native-xl</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/FormidableLabs/victory-native-xl">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/victory-native-xl)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/victory-native-xl Releases](https://github.com/react-native-oh-library/victory-native-xl/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm install @react-native-oh-tpl/victory-native-xl@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/victory-native-xl@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import * as React from "react";
import { useState } from "react";
import { View, Text } from "react-native";
import { CartesianChart, Line } from "victory-native";

function randomNumber() {
  return Math.floor(Math.random() * 26) + 12;
}
const DATA = (numberPoints = 13) =>
  Array.from({ length: numberPoints }, (_, index) => ({
    day: index + 1,
    highTmp: randomNumber(),
  }));

const [data, setData] = useState(DATA());

export default function LineChartExample() {
  return (
    <>
      <View style={{height: 300}}>
      <Text>Line Chart</Text>
      <CartesianChart
        data={data}
        xKey="day"
        yKeys={["highTmp"]}
      >
        {({ points }) => (
          <>
          <Line 
            points={points.highTmp} 
            color="red" 
            strokeWidth={3} 
            curveType="catmullRom"
            animate={{ type: "timing", duration: 300}}
            connectMissingData={true}
          />
          </>
        )}
      </CartesianChart>
      </View>
      </>
  );
}
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated、 @react-native-oh-tpl/react-native-skia的原生端代码，如已在鸿蒙工程中引入过这两个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-skia](/zh-cn/react-native-skia.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/victory-native-xl Releases](https://github.com/react-native-oh-library/victory-native-xl/releases)

## 属性

详情见 [victory-native-xl](https://github.com/FormidableLabs/victory-native-xl) Props tables

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Cartesian Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An array of objects to be used as data points for the chart | array[]  | yes     | all | yes
| xKey  | A string value indicating the key of each data[number] object to be used on the independent (x) axis for charting. E.g. "day" if you want to use the "day" field of the data points for the x-axis |  string | yes  | all | yes
| yKeys   | A string[] array of string indicating the keys of each data[number] object to be used on the dependent (y) axis for charting. E.g. yKeys={["lowTmp", "highTmp"]} if you want to chart both high and low temperatures on the y-axis and those values have keys of lowTmp and highTmp respectively | string[] | yes  | all | yes
| children  | The children prop is a render function whose sole argument is an object that exposes transformed data for you to use in your drawing operations. For example, the children render function's argument has a points field that exposes a version of your input data that's transformed to be plotted on the Canvas (see the Example section above for an example of this)| function | yes  | all | yes
| padding | A number or an object of shape { left?: number; right?: number; top?: number; bottom?: number; } that specifies that padding between the outer bounds of the Skia canvas and where the charting bounds will occur | number | no  | all | yes
| domain | An object of shape { x?: [number] \| [number, number]; y?: [number] \| [number, number] } that can be specified to control the upper and lower bounds of each axis. It defaults to the min and max of each range respectively | object | no  | all | yes
| domainPadding | A number or an object of shape { left?: number; right?: number; top?: number; bottom?: number; } that specifies that padding between the outer bounds of the charting area (e.g. where the axes lie) and where chart elements will be plotted | object  | no  | all | yes
| axisOptions | The axisOptions is an optional prop allows you to configure the axes and grid of the chart. If it is not present then the chart will not render any axes or grid | object  | no  | all | yes
| chartPressState | The chartPressState prop allows you to pass in Reanimated SharedValues that will be used to track the user's "press" gesture on the chart. This is generally used for creating some sort of tooltip/active value indicator. See the Chart Gestures page for more in-depth information on how to use this prop | object  | no  | all | yes
| renderOutside | The renderOutside prop is identical to the children prop in form, but it will render elements at the root of the Skia canvas (not inside of a clipping group). This allows you to render elements outside of the bounds of any axes that you have configured | object  | no  | all | yes
| onChartBoundsChange | The onChartBoundsChange prop is a function of the shape onChartBoundsChange?: (bounds: ChartBounds) => void; that exposes the chart bounds, useful if you need access to the chart's bounds for your own custom drawing purposes | function   | no  | all | yes
| gestureLongPressDelay | The gestureLongPressDelay prop allows you to set the delay in milliseconds before the pan gesture is activated. Defaults to 100 | number   | no  | all | yes


### Line Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points  | A PointsArray array that comes from a field of the points object exposed the children render function of CartesianChart, as illustrated in the example above | array[]  | no     | all | yes
| animate  | The animate prop takes a PathAnimationConfig object and will animate the path when the points changes |  object | no  | all | yes
| curveType   | A CurveType value that indicates the type of curve should be drawn (e.g. linear or natural) | string | no  | all | yes
| connectMissingData  | The connectMissingData: boolean value that indicates whether missing data should be interpolated for the resulting Path. If set to true, the output will be a single, connected line chart path (even if there are missing data values). If set to false, if there is missing data values – the path will consist of multiple disconnected "parts"| boolean | no  | all | yes
| children | A children pass-thru that will be rendered inside of the Skia Path element, useful if you'd like to make e.g. a gradient path | object | no  | all | yes


### Area Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points | A PointsArray array that comes from a field of the points object exposed the children render function of CartesianChart, as illustrated in the example above  | array[]   | no  | all | yes
| y0  | A number that indicates where the "bottom" of the area path should run. This number should be in canvas coordinates | number  | no  | all | yes
| animate | The animate prop takes a PathAnimationConfig object and will animate the path when the points changes | object  | no  | all | yes
| curveType | A CurveType value that indicates the type of curve should be drawn (e.g. linear or natural) | string   | no  | all | yes
| connectMissingData | The connectMissingData: boolean value that indicates whether missing data should be interpolated for the resulting Path. If set to true, the output will be a single, connected area chart path (even if there are missing data values). If set to false, if there is missing data values – the path will consist of multiple disconnected "parts"  | boolean | no  | all | yes
| children  | A children pass-thru that will be rendered inside of the Skia Path element, useful if you'd like to make e.g. a gradient path | object   | no  | all | yes


### Bar Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points | A PointsArray array that comes from a field of the points object exposed the children render function of CartesianChart, as illustrated in the example above | array[]  | no  | all | yes
| chartBounds | A ChartBounds object needed to appropriately draw the bars. This generally comes from the chartBounds render argument of CartesianChart | object  | no  | all | yes
| innerPadding | An optional number between 0 and 1 that represents what fraction of the horizontal space between the first and last bars should be "white space". Defaults to 0.2. Use 0 for no gap between bars, and values closer to 1 to make bars increasingly narrow | number | no  | all | yes
| animate | The animate prop takes a PathAnimationConfig object and will animate the path when the points change | object   | no  | all | yes
| roundedCorners | The roundedCorners prop allows you to customize the roundedness of each corner of the Bar component. It's an object type that defines the radii for the top-left, top-right, bottom-right, and bottom-left corners | object  | no  | all | yes
| barWidth | The barWidth prop takes a number and sets the width of the bar to that number. If not provided, the default is determined by the chartBounds and number of data points. Takes precendence over the barCount prop. Use this for the most fine grained control of bar width | number    | no  | all | yes
| barCount | The barCount prop takes a number and sets the width of the bar as if there X data points. If not provided, the default is determined by the chartBounds and number of data points. Useful for getting a fixed bar width regardless of the number of data points. Use this for a more general control of bar width | number  | no  | all | yes
| labels | The labels prop allows you to enable and customize the data label of the Bar component. The data label text is the Y-axis value associated with the Bar component | object | no  | all | yes
| children | A children pass-thru that will be rendered inside of the Skia Path element, useful if you'd like to make e.g. a gradient path  | object | no  | all | yes


### BarGroup Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| chartBounds | A ChartBounds object needed to appropriately draw the bars. This generally comes from the chartBounds render argument of CartesianChart | object  | no  | all | yes
| betweenGroupPadding | An optional number between 0 and 1 that represents what fraction of the horizontal space between the first and last bar groups should be "white space". Defaults to 0.2. Use 0 for no gap between groups, and values closer to 1 to make bars increasingly narrow  | number  | no  | all | yes
| withinGroupPadding | An optional number between 0 and 1 that represents what fraction of the horizontal space between the first and last bars within a group should be "white space". Defaults to 0.2. Use 0 for no gap between bars within a group, and values closer to 1 to make bars increasingly narrow | number   | no  | all | yes
| barWidth | The barWidth prop takes a number and sets the width of the bar to that number. If not provided, the default is determined by a combination of the total available width for the group of bars, the number of bars in the group, and the padding between the bars within the group. Takes precedence over barCount prop. Use this for the most fine grained control of bar width | number   | no  | all | yes
| barCount | The barCount prop takes a number and sets the width of the bar as if there X data points. If not provided, the default is determined by the chartBounds and number of data points. Useful for getting a fixed bar width regardless of the number of data points. Use this for a more general control of bar width | number   | no  | all | yes
| onBarSizeChange | That alerts the consumer when the size of the bars/groups changes, useful for if you're building a custom tooltip and need to know the size of the groups/bars | function  | no  | all | yes
| roundedCorners | The roundedCorners prop allows you to customize the roundedness of each corner of a BarGroup.Bar component. It's an object type that defines the radii for the top-left, top-right, bottom-right, and bottom-left corners | object   | no  | all | yes
| children | An array of BarGroup.Bar elements (see below) that represent the bars to add to the bar group | object  | no  | all | yes


### Scatter Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| points | TA PointsArray array that comes from a field of the points object exposed the children render function of CartesianChart, as illustrated in the example above | array[]   | no  | all | yes
| radius |  radius of the circle, half the width of the square | number  | no  | all | yes
| shape   | One of the following ScatterShape values that determines the shape of each point to be drawn  | ScatterShape   | no  | all | yes
| animate | The animate prop takes a PathAnimationConfig object and will animate the path when the points change | object   | no  | all | yes
| children | An array of BarGroup.Bar elements (see below) that represent the bars to add to the bar group | object  | no  | all | yes

### Polar Chart

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data | An array of objects to be used as data points for the chart  | array[]   | yes  | all | yes
| labelKey | A string value indicating the key of each data[number] object to be used. Currently only used on the legend part of the chart. In the future we may add support for a variety of labels within the chart  | string   | yes  | all | yes
| valueKey | A string value indicating the key of each data[number] object to be used to draw a slice of the Pie  | string   | yes  | all | yes
| colorKey | A string value indicating the key of each data[number] object to be used to draw a slice of the Pie  | string   | yes  | all | yes
| children | The only supported children of a PolarChart is currently a Pie.Chart See the Pie Chart for more details  | object   | no  | all | yes
| containerStyle | A StyleProp<ViewStyle> that styles the View which wraps the Canvas of the Polar chart  | object   | no  | all | yes
| canvasStyle | A StyleProp<ViewStyle> that styles the Canvas upon which the Polar chart is drawn  | object   | no  | all | yes

### Pie.Chart

**Bar related props for making Capped Bar chart**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| innerRadius | TA number or string (as a percentage) which turns the Pie chart into a Donut chart. The innerRadius prop is the radius of the inner circle of the donut chart. If not provided, the chart will remain a Pie chart   | number  | no  | all | yes
| circleSweepDegrees | A number which defines how many degrees of the chart should be drawn. The default is 360 which will draw a full circle. If you want to draw a partial circle, you can set this prop to a value between 0 and 360  | number   | no  | all | yes
| startAngle | A number which defines the starting angle of the chart. Changing this prop will rotate the chart     | number   | no  | all | yes
| children | The children prop is a render function which maps through the data and whose sole argument is each individual slice of the pie, allowing you to customize each slice as needed. E.g. this slice will have all the data needed to render a Pie.Slice />   | function  | no  | all | yes

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)]( https://www.mit-license.org/) ，请自由地享受和参与开源。
