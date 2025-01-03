Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-charts-wrapper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wuxudong/react-native-charts-wrapper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mitlicense.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-charts-wrapper)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-charts-wrapper/Releases](https://github.com/react-native-oh-library/react-native-charts-wrapper/releases). For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-charts-wrapper
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-charts-wrapper
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { BarChart } from "react-native-charts-wrapper";
const BarChartDemo = () => {
  const data = [
    { x: 1, y: 20 },
    { x: 2, y: 43 },
    { x: 3, y: 21 },
    { x: 4, y: 33 },
    { x: 5, y: 23 },
    { x: 6, y: 44 },
    { x: 7, y: 5 },
    { x: 8, y: 12 },
  ];
  return (
    <BarChart
      style={styles.chart}
      data={{
        dataSets: [
          {
            label: "demo",
            values: data,
          },
        ],
      }}
      animation={{ durationX: 2000, durationY: 2000 }}
    />
  );
};
export default BarChartDemo;
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-charts-wrapper": "file:../../node_modules/@react-native-oh-tpl/react-native-charts-wrapper/harmony/charts_wrapper.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing BarCharts, LineCharts, HorizontalBarCharts, BubbleCharts, PieCharts, RadarCharts, ScatterCharts, CandleStickCharts, and CombinedCharts Components to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import {
+  BarCharts,
+  LineCharts,
+  HorizontalBarCharts,
+  BubbleCharts,
+  PieCharts,
+  RadarCharts,
+  ScatterCharts,
+  CandleStickCharts,
+  CombinedCharts
+ } from "@react-native-oh-tpl/react-native-charts-wrapper"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+    if (ctx.componentName === BarCharts.NAME) {
+      BarCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === LineCharts.NAME) {
+      LineCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === HorizontalBarCharts.NAME) {
+      HorizontalBarCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === BubbleCharts.NAME) {
+      BubbleCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === PieCharts.NAME) {
+      PieCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === RadarCharts.NAME) {
+      RadarCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === ScatterCharts.NAME) {
+      ScatterCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === CandleStickCharts.NAME) {
+      CandleStickCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
+    if (ctx.componentName === CombinedCharts.NAME) {
+      CombinedCharts({
+        ctx: ctx.rnComponentContext,
+        tag: ctx.tag
+      })
+    }
 ...
}
```

> [!TIP] The repository uses a mixed solution, so the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ BarCharts.NAME,
+ LineCharts.NAME,
+ HorizontalBarCharts.NAME,
+ BubbleCharts.NAME,
+ PieCharts.NAME,
+ RadarCharts.NAME,
+ ScatterCharts.NAME,
+ CandleStickCharts.NAME,
+ CombinedCharts.NAME
  ];
```

### 4. Introducing ChartsWrapperPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {ChartsWrapperPackage} from '@react-native-oh-tpl/react-native-charts-wrapper/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ChartsWrapperPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-charts-wrapper/Releases](https://github.com/react-native-oh-library/react-native-charts-wrapper/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Common Props

#### Description

| Name      | Description                      | Type   | Required | Platform    | HarmonyOS Support |
| --------- | -------------------------------- | ------ | -------- | ----------- | ----------------- |
| text      | Sets the description to be displayed.          | string | No       | iOS/Android | Yes               |
| textColor | Sets the text color for labels.          | number | No       | iOS/Android | Yes               |
| textSize  | Sets the text size for labels.              | number | No       | iOS/Android | Yes               |
| positionX | Sets the custom position of the description on the screen.| number | No       | iOS/Android | Yes               |
| positionY | Sets the custom position of the description on the screen.| number | No       | iOS/Android | Yes               |

#### Legend

| Name                | Description              | Type                                         | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------ | -------------------------------------------- | -------- | ----------- | ----------------- |
| enabled             | Sets whether to enable Legend.    | bool                                         | No       | iOS/Android | Yes               |
| text                | Sets the text to be displayed as a legend.  | string                                       | No       | iOS/Android | Yes               |
| textColor           | Sets the color of the legend text.      | number                                       | No       | iOS/Android | NO                |
| textSize            | Sets the size of the legend text.      | number                                       | No       | iOS/Android | Yes               |
| fontFamily          | Sets the font family of Legend.          | string                                       | No       | iOS/Android | Yes               |
| wordWrapEnabled     | Sets whether to wrap the legend text.    | bool                                         | No       | iOS/Android | Yes               |
| maxSizePercent      | Sets the maximum size percentage of Legend.  | number                                       | No       | iOS/Android | NO                |
| horizontalAlignment | Sets the horizontal alignment mode of Legend.        | one of `'LEFT', 'CENTER', 'RIGHT'`           | No       | iOS/Android | Yes               |
| verticalAlignment   | Sets the vertical alignment mode of Legend.        | one of `'TOP', 'CENTER', 'BOTTOM'`           | No       | iOS/Android | Yes               |
| orientation         | Sets the legend orientation.          | one of `'HORIZONTAL', 'VERTICAL'`            | No       | iOS/Android | Yes               |
| drawInside          | Sets whether to draw Legend inside.  | bool                                         | No       | iOS/Android | Yes               |
| direction           | Sets the text direction of the legend.      | one of `LEFT_TO_RIGHT', 'RIGHT_TO_LEFT`      | No       | iOS/Android | Yes               |
| form                | Sets the legend form or shape. | string                                       | No       | iOS/Android | Yes               |
| formSize            | Sets the form size of the legend.      | number                                       | No       | iOS/Android | Yes               |
| xEntrySpace         | Sets the space between legends on the horizontal axis.| number                                       | No       | iOS/Android | Yes               |
| yEntrySpace         | Sets the space between legends on the vertical axis.| number                                       | No       | iOS/Android | Yes               |
| formToTextSpace     | Sets the space between Legend icon and text.| number                                       | No       | iOS/Android | Yes               |
| custom              | Sets the item array of the custom legend.| {` `colors: [number],` `labels: [string]` `} | No       | iOS/Android | NO                |

#### xAxis and yAxis

| Name                     | Description                              | Type                                                         | Required | Platform    | HarmonyOS Support |
| ------------------------ | ---------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| enabled                  | Sets whether to draw the component.                          | bool                                                         | No       | iOS/Android | Yes               |
| drawLabels               | Sets the label to draw this axis.                      | bool                                                         | No       | iOS/Android | Yes               |
| drawAxisLine             | Sets the line next to the axis.                          | bool                                                         | No       | iOS/Android | Yes               |
| drawGridLines            | Sets whether to draw the grid line for this axis.                | bool                                                         | No       | iOS/Android | Yes               |
| textColor                | Sets the text color for labels.                  | number                                                       | No       | iOS/Android | Yes               |
| textSize                 | Sets the text size for labels.                  | number                                                       | No       | iOS/Android | Yes               |
| fontFamily               | Sets the fonts of X-axis and Y-axis labels.                     | string                                                       | No       | iOS/Android | Yes               |
| gridColor                | Sets the grid line (horizontal line) color of this axis.    | bool                                                         | No       | iOS/Android | Yes               |
| gridLineWidth            | Sets the width of the grid line drawn away from each axis.        | bool                                                         | No       | iOS/Android | Yes               |
| axisLineColor            | Sets the color of the chart border.                  | bool                                                         | No       | iOS/Android | Yes               |
| axisLineWidth            | Sets the width of the chart border.                  | bool                                                         | No       | iOS/Android | Yes               |
| gridDashedLine           | Sets to draw the grid with dashed lines.                | {` `lineLength: number,` `spaceLength: number,` `phase: number` `}` ` | No       | iOS/Android | Yes               |
| limitLines               | Sets the limit line.                              | array[]                                                      | No       | iOS/Android | Yes               |
| drawLimitLinesBehindData | Sets to draw the limit line behind data.            | bool                                                         | No       | iOS/Android | Yes               |
| axisMaximum              | Sets the maximum number of labels for the axis.                      | number                                                       | No       | iOS/Android | Yes               |
| axisMinimum              | Sets the minimum number of labels for the axis.                      | number                                                       | No       | iOS/Android | Yes               |
| granularity              | Sets the minimum interval for axis zoom-in.                  | number                                                       | No       | iOS/Android | Yes               |
| granularityEnabled       | Sets the granularity control of the axis value interval.                  | bool                                                         | No       | iOS/Android | Yes               |
| labelCount               | Sets the number of labels on the Y axis.                   | number                                                       | No       | iOS/Android | Yes               |
| labelCountForce          | Sets the number of labels on the Y axis.                   | bool                                                         | No       | iOS/Android | Yes               |
| centerAxisLabels         | Sets axis labels as the center instead of drawing them in their original location.| bool                                                         | No       | iOS/Android | Yes               |

### xAxis

| Name                   | Description                                         | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------- | --------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| labelRotationAngle     | Sets the angle (in degrees) at which the X-axis label is drawn.              | number | No       | iOS/Android | Yes               |
| avoidFirstLastClipping | If it is set to **true**, the chart will avoid the first and last labels.| bool   | No       | iOS/Android | Yes               |
| position               | Sets the position of the X-axis label.                                | string | No       | iOS/Android | Yes               |
| yOffset                | Sets the Y-axis offset for the label on this axis.                | string | No       | iOS/Android | Yes               |

### yAxis

| Name        | Description                                        | Type                                                         | Required | Platform    | HarmonyOS Support |
| ----------- | -------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| inverted    | If it is set to **true**, the Y axis is inverted, which means that the low value is at the bottom of the chart.| number                                                       | No       | iOS/Android | Yes               |
| spaceTop    | Sets the top axis space, in percentage of the full scale.            | bool                                                         | No       | iOS/Android | Yes               |
| spaceBottom | Sets the bottom axis space, in percentage of the full scale.            | number                                                       | No       | iOS/Android | Yes               |
| position    | Sets the position of the Y label.                                 | number                                                       | No       | iOS/Android | Yes               |
| maxWidth    | Sets the maximum width of the axis.                          | bool                                                         | No       | iOS/Android | Yes               |
| minWidth    | Sets the minimum width of the axis.                          | string                                                       | No       | iOS/Android | Yes               |
| zeroLine    | Sets the grid line.                                        | {` `enabled: bool,` `lineWidth: number,` `lineColor: number` `} | No       | iOS/Android | Yes               |

### Chart Base

| Name                         | Description          | Type        | Required | Platform    | HarmonyOS Support |
| ---------------------------- | -------------------- | ----------- | -------- | ----------- | ----------------- |
| animation                    | Sets the chart animation.        | object      | No       | iOS/Android | Yes               |
| chartBackgroundColor         | Sets the chart background color.    | number      | No       | iOS/Android | NO                |
| logEnabled                   | Enables logs.            | bool        | No       | iOS/Android | NO                |
| noDataText                   | Sets the text without data.      | string      | No       | iOS/Android | Yes               |
| noDataTextColor              | Sets the color of the text without data.  | number      | No       | iOS/Android | Yes               |
| touchEnabled                 | Enables touch.            | bool        | No       | iOS/Android | Yes               |
| dragDecelerationEnabled      | Sets the drag deceleration.        | bool        | No       | iOS/Android | Yes               |
| dragDecelerationFrictionCoef | Sets the friction coefficient of resistance deceleration.| function    | No       | iOS/Android | Yes               |
| chartDescription             | Sets the description component.        | Description | No       | iOS/Android | Yes               |
| legend                       | Sets the legend.            | Legend      | No       | iOS/Android | Yes               |
| xAxis                        | Sets the X axis.           | Xaxis       | No       | iOS/Android | Yes               |
| highlights                   | Sets the highlight.            | object      | No       | iOS/Android | NO                |

### BarLineChartBase

| Name                   | Description                                                  | Type                          | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | ----------------------------- | -------- | ----------- | ----------------- |
| drawGridBackground     | Sets whether to draw the grid background color.                                        | bool                          | No       | iOS/Android | Yes               |
| gridBackgroundColor    | Sets the grid background color.                                            | number                        | No       | iOS/Android | Yes               |
| drawBorders            | Sets whether to draw borders.                                                | bool                          | No       | iOS/Android | Yes               |
| borderColor            | Sets the border color.                                                | number                        | No       | iOS/Android | Yes               |
| borderWidth            | Sets the border width.                                                | number                        | No       | iOS/Android | Yes               |
| minOffset              | Sets the minimum offset.                                                | number                        | No       | iOS/Android | Yes               |
| maxVisibleValueCount   | Sets the maximum counts.                                              | number                        | No       | iOS/Android | Yes               |
| visibleRange           | Limits the visible maximum and minimum x range through pinch zooming.               | object                        | No       | iOS/Android | NO                |
| autoScaleMinMaxEnabled | Whether to set the autoscale label of the Y axis.                                 | bool                          | No       | iOS/Android | Yes               |
| keepPositionOnRotation | Whether a chart should keep its position (zoom/scroll) after rotation (orientation change).     | bool                          | No       | iOS/Android | NO                |
| scaleEnabled           | Whether to enable scaling.                                                | bool                          | No       | iOS/Android | Yes               |
| scaleXEnabled          | Whether to enable X-axis scaling.                                           | bool                          | No       | iOS/Android | Yes               |
| scaleYEnabled          | Whether to enable Y-axis scaling.                                           | bool                          | No       | iOS/Android | Yes               |
| dragEnabled            | Whether to enable drag.                                                | bool                          | No       | iOS/Android | Yes               |
| pinchZoom              | If it is set to **true**, the X and Y axes can be zoomed with two fingers at the same time. If it is set to **false**, the X and Y axes can be zoomed separately.| bool                          | No       | iOS/Android | Yes               |
| doubleTapToZoomEnabled | If it is set to **true**, you can double-tap the chart to enable zooming.              | bool                          | No       | iOS/Android | Yes               |
| yAxis                  | Sets the Y axis.                                                   | { left: YAxis, right: YAxis } | No       | iOS/Android | Yes               |
| zoom                   | Zooms in or out based on a specified scale factor.                                  | object                        | No       | iOS/Android | Yes               |
| viewPortOffsets        | Sets the custom offset of the current viewport (offset on both sides of the view).          | object                        | No       | iOS/Android | Yes               |

### Data Config Type

#### Common

| Name             | Description                                 | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| colors           | Sets the color applied to the dataset. It consists of multiple colors.    | number[] | No       | iOS/Android | Yes               |
| highlightEnabled | Sets whether to enable highlight.                               | bool     | No       | iOS/Android | Yes               |
| drawValues       | Sets the drawing value.                                 | bool     | No       | iOS/Android | Yes               |
| valueTextSize    | Sets the text size of a value.                           | number   | No       | iOS/Android | Yes               |
| valueTextColor   | Sets the text color of a value.                           | number   | No       | iOS/Android | Yes               |
| visible          | Sets whether the value is visible.                             | bool     | No       | iOS/Android | Yes               |
| valueFormatter   | Sets the data formatter.                             | string   | No       | iOS/Android | NO                |
| axisDependency   | Sets the Y axis (left or right) on which the dataset is drawn.| string   | No       | iOS/Android | Yes               |

#### barLineScatterCandleBubble

| Name           | Description                      | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | -------------------------------- | ------ | -------- | ----------- | ----------------- |
| highlightColor | Sets the color used to draw the highlight indicator.| number | No       | iOS/Android | Yes               |

#### lineScatterCandleRadar

| Name                             | Description                                             | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------------- | ------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| drawVerticalHighlightIndicator   | Whether to enable the vertical highlight indicator. If the value is **false**, the indicator is not drawn.| bool   | No       | iOS/Android | Yes               |
| drawHorizontalHighlightIndicator | Whether to enable the horizontal highlight indicator. If the value is **false**, the indicator is not drawn.  | bool   | No       | iOS/Android | Yes               |
| highlightLineWidth               | Highlights the line width.                                               | number | No       | iOS/Android | Yes               |

#### lineRadar

| Name       | Description | Type | Required | Platform    | HarmonyOS Support |
| ---------- | ----------- | ---- | -------- | ----------- | ----------------- |
| fillColor  | Fill color.   | bool | No       | iOS/Android | Yes               |
| fillAlpha  | Sets the fill transparency. | bool | No       | iOS/Android | Yes               |
| drawFilled | Sets whether to enable fill.   | bool | No       | iOS/Android | Yes               |

#### PieRadarChartBase

| Name            | Description                                  | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | -------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| minOffset       | Sets the minimum offset (fill) around the chart. The default value is **0**.| number | No       | iOS/Android | Yes               |
| rotationEnabled | If it is set to **true**, you can enable the rotation gestures on the chart.| bool   | No       | iOS/Android | Yes               |
| rotationAngle   | Sets the offset (in degrees) for the radar chart rotation.      | number | No       | iOS/Android | Yes               |

### BarChart

| Name              | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| drawValueAboveBar | If it is set to **true**, all values are drawn above the bars, not below the top.| bool    | No       | iOS/Android | Yes               |
| drawBarShadow     | If it is set to **true**, a gray area is drawn after each bar, indicating the maximum value.| bool    | No       | iOS/Android | Yes               |
| barWidth          | Sets the width of each bar on the X axis.                           | number  | No       | iOS/Android | Yes               |
| topRadius         | Sets the top radius of the bar.                                            | number  | No       | iOS/Android | Yes               |
| group             | Groups all BarDataSet objects.                              | object  | No       | iOS/Android | Yes               |
| data              | Column chart data.                                                  | BarData | Yes      | iOS/Android | Yes               |

#### BarData Config

| Name                       | Description                                          | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| barShadowColor             | Sets the color used to draw bar shadows.                          | number                                                       | No       | iOS/Android | Yes               |
| highlightAlpha             | Sets the alpha value used to draw highlights (transparency).                 | number                                                       | No       | iOS/Android | Yes               |
| stackLabels                | Sets labels for bar stacks with different values.                            | string[]                                                     | No       | iOS/Android | NO                |
| common                     | Common data.                                        | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | Common basic data of column chart, bar chart, scatter chart, bubble chart, and candlestick chart.| Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |

#### BarData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| X    | X-axis data.   | number | Yes      | iOS/Android | Yes               |
| Y    | Y-axis data.   | number | Yes      | iOS/Android | Yes               |

### HorizontalBarChart

| Name | Description    | Type    | Required | Platform    | HarmonyOS Support |
| ---- | -------------- | ------- | -------- | ----------- | ----------------- |
| data | Horizontal bar chart data.| BarData | Yes      | iOS/Android | Yes               |

### CandleStickChart

| Name | Description | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ---------- | -------- | ----------- | ----------------- |
| data | Candlestick chart data. | CandleData | Yes      | iOS/Android | Yes               |

#### CandleData Config

| Name                       | Description                                                 | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | Common data.                                               | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | Common basic data of column chart, bar chart, scatter chart, bubble chart, and candlestick chart.       | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |
| lineScatterCandleRadar     | Common basic data of column chart, candlestick chart, scatter chart, and radar chart.               | Data Config Type.CommonConfigType.lineScatterCandleRadar     | No       | iOS/Android | Yes               |
| barSpace                   | Sets the space on the left and right sides of each bar.                      | number                                                       | No       | iOS/Android | Yes               |
| shadowWidth                | Sets the width of the candle shadow line, in pixels.                         | number                                                       | No       | iOS/Android | Yes               |
| shadowColor                | Sets the shadow color of all bars.                                     | number                                                       | No       | iOS/Android | Yes               |
| shadowColorSameAsCandle    | Sets the shadow color the same as the candle color.                       | bool                                                         | No       | iOS/Android | Yes               |
| neutralColor               | Sets the unique color applied to this dataset when \*open == close.    | number                                                       | No       | iOS/Android | Yes               |
| decreasingColor            | Sets the unique color applied to this dataset when \*open > close.     | number                                                       | No       | iOS/Android | Yes               |
| decreasingPaintStyle       | Sets the drawing style when open > close.                                  | string                                                       | No       | iOS/Android | Yes               |
| increasingColor            | Sets the unique color applied to the dataset when \*open <= close.| number                                                       | No       | iOS/Android | Yes               |
| increasingPaintStyle       | Sets the drawing style when open < close.                                  | string                                                       | No       | iOS/Android | Yes               |

#### CandleData Values

| Name    | Description | Type   | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------ | -------- | ----------- | ----------------- |
| x       | X-axis data.   | number | No       | iOS/Android | Yes               |
| shadowH | Shadow H.     | number | Yes      | iOS/Android | Yes               |
| shadowL | Shadow L.     | number | Yes      | iOS/Android | Yes               |
| open    | Opened.     | number | Yes      | iOS/Android | Yes               |
| close   | Closed.     | number | Yes      | iOS/Android | Yes               |

### CombinedChart

| Name | Description | Type         | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------------ | -------- | ----------- | ----------------- |
| data | Combined chart data. | combinedData | Yes      | iOS/Android | Yes               |

#### combinedData

| Name        | Description | Type        | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | ----------- | -------- | ----------- | ----------------- |
| lineData    | Line chart data. | lineData    | No       | iOS/Android | Yes               |
| barData     | Column chart data. | barData     | No       | iOS/Android | Yes               |
| scatterData | Scatter chart data. | scatterData | No       | iOS/Android | Yes               |
| candleData  | Candlestick chart data. | candleData  | No       | iOS/Android | Yes               |
| bubbleData  | Bubble chart data. | bubbleData  | No       | iOS/Android | Yes               |

### BubbleChart

| Name | Description | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ---------- | -------- | ----------- | ----------------- |
| data | Bubble chart data. | bubbleData | Yes      | iOS/Android | Yes               |

#### BubbleData Config

| Name                       | Description                                          | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | Common data.                                        | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | Common basic data of column chart, bar chart, scatter chart, bubble chart, and candlestick chart.| Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |

#### BubbleData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| x    | X-axis data.   | number | No       | iOS/Android | Yes               |
| y    | Y-axis data.   | number | Yes      | iOS/Android | Yes               |
| size | Size.       | number | Yes      | iOS/Android | Yes               |

### LineChart

| Name | Description | Type     | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | -------- | -------- | ----------- | ----------------- |
| data | Line chart data. | LineData | Yes      | iOS/Android | Yes               |

#### LineData Config

| Name                       | Description                                                  | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | Common data.                                                | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | Common basic data of column chart, bar chart, scatter chart, bubble chart, and candlestick chart.        | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |
| lineScatterCandleRadar     | Common basic data of column chart, candlestick chart, scatter chart, and radar chart.                | Data Config Type.CommonConfigType.lineScatterCandleRadar     | No       | iOS/Android | Yes               |
| lineRadar                  | Common data of line chart and radar chart.                                      | Data Config Type.lineRadar                                   | No       | iOS/Android | Yes               |
| circleRadius               | Sets the radius of the drawn circle.                                          | number                                                       | No       | iOS/Android | Yes               |
| drawCircles                | Set to **true** to enable the drawing dataset of this circle indicator. The default value is **true**.| bool                                                         | No       | iOS/Android | Yes               |
| mode                       | Sets the drawing mode of lineDataSet.                                 | object                                                       | No       | iOS/Android | Yes               |
| lineWidth                  | Sets the line width.                                                    | number                                                       | No       | iOS/Android | Yes               |
| drawCubicIntensity         | Sets the curve radian.                                                | number                                                       | No       | iOS/Android | NO                |
| circleColor                | Sets the unique color applied for this dataset.                              | number                                                       | No       | iOS/Android | Yes               |
| circleColors               | Sets the color set applied for this dataset.                                | number[]                                                     | No       | iOS/Android | Yes               |
| circleHoleColor            | Sets the inner rounded circle color of the line.                                    | number                                                       | No       | iOS/Android | Yes               |
| drawCircleHole             | Whether to draw a hole in each data circle.                                | bool                                                         | No       | iOS/Android | Yes               |
| dashedLine                 | Sets the polyline to a dashed line.                                              | object                                                       | No       | iOS/Android | Yes               |
| fillFormatter              | Sets filling.                                                    | object                                                       | No       | iOS/Android | Yes               |

#### LineData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| x    | X-axis data.   | number | No       | iOS/Android | Yes               |
| y    | Y-axis data.   | number | Yes      | iOS/Android | Yes               |

### ScatterChart

| Name | Description | Type        | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ----------- | -------- | ----------- | ----------------- |
| data | Scatter chart data. | ScatterData | Yes      | iOS/Android | Yes               |

#### ScatterData Config

| Name                       | Description                                          | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | Common data.                                        | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | Common basic data of column chart, bar chart, scatter chart, bubble chart, and candlestick chart.| Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |
| lineScatterCandleRadar     | Common basic data of column chart, candlestick chart, scatter chart, and radar chart.        | Data Config Type.CommonConfigType.lineScatterCandleRadar     | No       | iOS/Android | Yes               |
| scatterShapeSize           | Sets the size of the drawn scatter shape.                | number                                                       | No       | iOS/Android | Yes               |
| scatterShape               | Sets the scatter shape used to draw DataSet.               | string                                                       | No       | iOS/Android | Yes               |
| scatterShapeHoleColor      | Sets the hole color in a shape.                                  | number                                                       | No       | iOS/Android | Yes               |
| scatterShapeHoleRadius     | Sets the hole radius in a shape (applicable to squares, circles, and triangles).    | number                                                       | No       | iOS/Android | Yes               |

#### ScatterData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| x    | X-axis data.   | number | No       | iOS/Android | Yes               |
| y    | Y-axis data.   | number | Yes      | iOS/Android | Yes               |

### PieChart

| Name                    | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| extraOffsets            | Sets the chart data.                                                      | object  | No       | iOS/Android | Yes               |
| drawEntryLabels         | If it is set to **true**, labels can be drawn into the pie chart sector.            | bool    | No       | iOS/Android | Yes               |
| usePercentValues        | If it is enabled, the values in the pie chart are displayed in percentage.            | bool    | No       | iOS/Android | Yes               |
| centerText              | Sets the text string displayed in the center of the pie chart.                      | string  | No       | iOS/Android | Yes               |
| styledCenterText        | Sets the style of the text string displayed in the center of the pie chart.                  | object  | No       | iOS/Android | Yes               |
| centerTextRadiusPercent | Sets the rectangle radius of the center text bounding box, in percentage of the pie chart.                 | number  | No       | iOS/Android | Yes               |
| holeRadius              | Sets the radius of the center hole of the pie chart, in percentage. \*The maximum radius (max = the radius of the chart) is **50%** by default.| number  | No       | iOS/Android | Yes               |
| holeColor               | Sets the color of the hole drawn in the center of the pie chart.                                | number  | No       | iOS/Android | Yes               |
| transparentCircleRadius | Sets the radius of the transparent circle drawn next to the hole.                              | number  | No       | iOS/Android | Yes               |
| transparentCircleColor  | Sets the color of the transparent circle drawn next to the hole.                              | number  | No       | iOS/Android | Yes               |
| entryLabelColor         | Sets the color of the label to be drawn.                                      | number  | No       | iOS/Android | Yes               |
| entryLabelTextSize      | Sets the size of a label in vp.                            | number  | No       | iOS/Android | Yes               |
| entryLabelFontFamily    | Sets custom fonts for the drawing of labels.                              | string  | No       | iOS/Android | Yes               |
| maxAngle                | Sets the maximum angle for calculating the pie chart circle.                                | number  | No       | iOS/Android | Yes               |
| data                    | Sets the pie chart data.                                                    | PieData | Yes      | iOS/Android | Yes               |

#### PieData Config

| Name              | Description                            | Type                               | Required | Platform    | HarmonyOS Support |
| ----------------- | -------------------------------------- | ---------------------------------- | -------- | ----------- | ----------------- |
| common            | Common data.                          | Data Config Type.Common            | No       | iOS/Android | Yes               |
| PieRadarChartBase | Sets pie chart and radar chart data.                      | Data Config Type.PieRadarChartBase | No       | iOS/Android | Yes               |
| sliceSpace        | Sets the space between pie chart slices in vp.| number                             | No       | iOS/Android | Yes               |
| selectionShift    | Sets the distance of the highlighted pie chart sector of the dataset.  | number                             | No       | iOS/Android | Yes               |
| xValuePosition    | Sets whether the label is displayed inside or outside the pie chart.            | string                             | No       | iOS/Android | Yes               |
| yValuePosition    | Sets whether the label is displayed inside or outside the pie chart.            | string                             | No       | iOS/Android | Yes               |

#### PieData Values

| Name  | Description | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------ | -------- | ----------- | ----------------- |
| value | Data       | number | Yes      | iOS/Android | Yes               |
| label | Alpha tag.       | number | No       | iOS/Android | Yes               |

### RadarChart

| Name              | Description                                          | Type                               | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------- | ---------------------------------- | -------- | ----------- | ----------------- |
| yAxis             | Y axis.                                                | YAxis                              | No       | iOS/Android | Yes               |
| drawWeb           | Sets pie chart and radar chart data.                                    | Data Config Type.PieRadarChartBase | No       | iOS/Android | Yes               |
| skipWebLineCount  | Sets the number of web rows that should be skipped on the chart web before next operations.| number                             | No       | iOS/Android | Yes               |
| webLineWidth      | Sets the web line width in the center.                          | number                             | No       | iOS/Android | Yes               |
| webLineWidthInner | Sets the web line width in the \*center.     | number                             | No       | iOS/Android | Yes               |
| webAlpha          | Sets the transparency (alpha) value for all web lines.                  | number                             | No       | iOS/Android | Yes               |
| webColor          | Sets the web line color in the center.                        | number                             | No       | iOS/Android | Yes               |
| webColorInner     | Sets the web lines color in the \*center.           | number                             | No       | iOS/Android | Yes               |
| data              | Radar chart data.                                          | RadarData                          | Yes      | iOS/Android | Yes               |

#### RadarData Config

| Name                   | Description                                  | Type                                                     | Required | Platform    | HarmonyOS Support |
| ---------------------- | -------------------------------------------- | -------------------------------------------------------- | -------- | ----------- | ----------------- |
| common                 | Common data.                                | Data Config Type.Common                                  | No       | iOS/Android | Yes               |
| lineScatterCandleRadar | Common basic data of column chart, candlestick chart, scatter chart, and radar chart.| Data Config Type.CommonConfigType.lineScatterCandleRadar | No       | iOS/Android | Yes               |
| lineRadar              | Common data of line chart and radar chart.                      | Data Config Type.lineRadar                               | No       | iOS/Android | Yes               |

#### RadarData Values

| Name  | Description | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------ | -------- | ----------- | ----------------- |
| value | Data       | number | Yes      | iOS/Android | Yes               |

## Known Issues

## Others

- The **maxSizePercent** property does not take effect on Android and iOS. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/995)
- The **custom** property will overwrite the original legend after being set. However, the custom legend is not displayed on Android and iOS, and the property does not take effect. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/996)
- The **logEnabled** property enables the **logcat** and **highlights** properties specific to Android. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/998)
- The **stackLabels** property setting does not take effect, and the **drawCubicIntensity** property setting does not take effect on Android and iOS. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/997)
- After the **visibleRange** property is set on Android and iOS, the maximum and minimum x ranges that can be viewed through scaling do not take effect. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/999)
- The **keepPositionOnRotation** property setting does not take effect on Android and iOS. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/999)
- The **valueFormatter** property does not take effect on Android and iOS. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/935)
- The **chartBackgroundColor** property setting does not take effect in the original library, because in the original library, the background color of the grid is the same as that of the chart. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/1001)
- The text in Legend has the same effect with the label in data, therefore, they are not supported in the original library. The performance on HarmonyOS is the same as that on Android and iOS. [Original issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/1003)

## License

This project is licensed under [The MIT License (MIT)](https://mitlicense.org/).
