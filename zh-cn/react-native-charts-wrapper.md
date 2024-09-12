模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-charts-wrapper)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-charts-wrapper/Releases](https://github.com/react-native-oh-library/react-native-charts-wrapper/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-charts-wrapper@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-charts-wrapper@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

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

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-charts-wrapper": "file:../../node_modules/@react-native-oh-tpl/react-native-charts-wrapper/harmony/charts_wrapper.har"
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

### 在 ArkTs 侧引入 BarCharts、LineCharts、HorizontalBarCharts 、BubbleCharts、PieCharts、RadarCharts、ScatterCharts、CandleStickCharts、CombinedCharts 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

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

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

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

### 3.在 ArkTs 侧引入 ChartsWrapperPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-charts-wrapper/Releases](https://github.com/react-native-oh-library/react-native-charts-wrapper/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Common Props

#### Description

| Name      | Description                      | Type   | Required | Platform    | HarmonyOS Support |
| --------- | -------------------------------- | ------ | -------- | ----------- | ----------------- |
| text      | 设置要显示为说明的文本           | string | No       | iOS/Android | Yes               |
| textColor | 设置用于标签的文本颜色           | number | No       | iOS/Android | Yes               |
| textSize  | 设置标签文本的大小               | number | No       | iOS/Android | Yes               |
| positionX | 设置说明文本在屏幕上的自定义位置 | number | No       | iOS/Android | Yes               |
| positionY | 设置说明文本在屏幕上的自定义位置 | number | No       | iOS/Android | Yes               |

#### Legend

| Name                | Description              | Type                                         | Required | Platform    | HarmonyOS Support |
| ------------------- | ------------------------ | -------------------------------------------- | -------- | ----------- | ----------------- |
| enabled             | 是否设置图表图例部件     | bool                                         | No       | iOS/Android | Yes               |
| text                | 设置要显示为图例的文本   | string                                       | No       | iOS/Android | Yes               |
| textColor           | 设置图例文本的颜色       | number                                       | No       | iOS/Android | Yes               |
| textSize            | 设置图例文本的大小       | number                                       | No       | iOS/Android | Yes               |
| fontFamily          | 图例部件的字体           | string                                       | No       | iOS/Android | Yes               |
| wordWrapEnabled     | 设置图例文字是否换行     | bool                                         | No       | iOS/Android | Yes               |
| maxSizePercent      | 图例部件最大大小百分比   | number                                       | No       | iOS/Android | NO                |
| horizontalAlignment | 图例部件水平对齐         | one of `'LEFT', 'CENTER', 'RIGHT'`           | No       | iOS/Android | Yes               |
| verticalAlignment   | 图例部件垂直对齐         | one of `'TOP', 'CENTER', 'BOTTOM'`           | No       | iOS/Android | Yes               |
| orientation         | 设置图例的方向           | one of `'HORIZONTAL', 'VERTICAL'`            | No       | iOS/Android | Yes               |
| drawInside          | 图例部件是否在内部绘制   | bool                                         | No       | iOS/Android | Yes               |
| direction           | 设置图例的文本方向       | one of `LEFT_TO_RIGHT', 'RIGHT_TO_LEFT`      | No       | iOS/Android | Yes               |
| form                | 设置图例形式的形式/形状  | string                                       | No       | iOS/Android | Yes               |
| formSize            | 设置图例格式的大小       | number                                       | No       | iOS/Android | Yes               |
| xEntrySpace         | 设置横轴上图例条目的间距 | number                                       | No       | iOS/Android | Yes               |
| yEntrySpace         | 设置竖轴上图例条目的间距 | number                                       | No       | iOS/Android | Yes               |
| formToTextSpace     | 图例部件图标到文字的间距 | number                                       | No       | iOS/Android | Yes               |
| custom              | 设置自定义图例的条目数组 | {` `colors: [number],` `labels: [string]` `} | No       | iOS/Android | NO                |

#### xAxis and yAxis

| Name                     | Description                              | Type                                                                  | Required | Platform    | HarmonyOS Support |
| ------------------------ | ---------------------------------------- | --------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| enabled                  | 是否绘制该组件                           | bool                                                                  | No       | iOS/Android | Yes               |
| drawLabels               | 设置绘制此轴的标签                       | bool                                                                  | No       | iOS/Android | Yes               |
| drawAxisLine             | 设置轴旁边的线                           | bool                                                                  | No       | iOS/Android | Yes               |
| drawGridLines            | 是否启用此轴的网格线绘制                 | bool                                                                  | No       | iOS/Android | Yes               |
| textColor                | 设置用于标签的文本颜色                   | number                                                                | No       | iOS/Android | Yes               |
| textSize                 | 设置用于标签的文本大小                   | number                                                                | No       | iOS/Android | Yes               |
| fontFamily               | X 轴 Y 轴标签的字体                      | string                                                                | No       | iOS/Android | Yes               |
| gridColor                | 设置此坐标轴的网格线（水平线）的颜色     | bool                                                                  | No       | iOS/Android | Yes               |
| gridLineWidth            | 设置远离每个轴绘制的栅格线的宽度         | bool                                                                  | No       | iOS/Android | Yes               |
| axisLineColor            | 设置图表周围边框的颜色                   | bool                                                                  | No       | iOS/Android | Yes               |
| axisLineWidth            | 设置图表周围边框的宽度                   | bool                                                                  | No       | iOS/Android | Yes               |
| gridDashedLine           | 设置以虚线模式绘制网格线                 | {` `lineLength: number,` `spaceLength: number,` `phase: number` `}` ` | No       | iOS/Android | Yes               |
| limitLines               | 设置限制线                               | array[]                                                               | No       | iOS/Android | Yes               |
| drawLimitLinesBehindData | 设置在实际数据之后绘制限制线             | bool                                                                  | No       | iOS/Android | Yes               |
| axisMaximum              | 设置轴的最大标签数                       | number                                                                | No       | iOS/Android | Yes               |
| axisMinimum              | 设置轴的最小标签数                       | number                                                                | No       | iOS/Android | Yes               |
| granularity              | 设置轴放大时的最小间隔                   | number                                                                | No       | iOS/Android | Yes               |
| granularityEnabled       | 设置轴值间隔的粒度控制                   | bool                                                                  | No       | iOS/Android | Yes               |
| labelCount               | 设置 y 轴的标签条目数                    | number                                                                | No       | iOS/Android | Yes               |
| labelCountForce          | 设置 y 轴的标签条目数                    | bool                                                                  | No       | iOS/Android | Yes               |
| centerAxisLabels         | 将轴标签居中，而不是在其原始位置绘制它们 | bool                                                                  | No       | iOS/Android | Yes               |

### xAxis

| Name                   | Description                                         | Type   | Required | Platform    | HarmonyOS Support |
| ---------------------- | --------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| labelRotationAngle     | 设置绘制 X 轴标签的角度（以度为单位）               | number | No       | iOS/Android | Yes               |
| avoidFirstLastClipping | 如果设置为 true，图表将避免第一个和最后一个标签条目 | bool   | No       | iOS/Android | Yes               |
| position               | 设置 X 轴标签的位置                                 | string | No       | iOS/Android | Yes               |
| yOffset                | 为该轴上的标签设置使用的 y 轴偏移量                 | string | No       | iOS/Android | Yes               |

### yAxis

| Name        | Description                                        | Type                                                            | Required | Platform    | HarmonyOS Support |
| ----------- | -------------------------------------------------- | --------------------------------------------------------------- | -------- | ----------- | ----------------- |
| inverted    | 设置为 true，则反转 y 轴，这意味着低值位于图表底部 | number                                                          | No       | iOS/Android | Yes               |
| spaceTop    | 设置顶轴间距，以占满量程的百分比为单位             | bool                                                            | No       | iOS/Android | Yes               |
| spaceBottom | 设置底轴间距，以占满量程的百分比为单位             | number                                                          | No       | iOS/Android | Yes               |
| position    | 设置 y 标签的位置                                  | number                                                          | No       | iOS/Android | Yes               |
| maxWidth    | 设置轴可以采用的最大宽度                           | bool                                                            | No       | iOS/Android | Yes               |
| minWidth    | 设置轴可以采用的最小宽度                           | string                                                          | No       | iOS/Android | Yes               |
| zeroLine    | 设置网格线                                         | {` `enabled: bool,` `lineWidth: number,` `lineColor: number` `} | No       | iOS/Android | Yes               |

### Chart Base

| Name                         | Description          | Type        | Required | Platform    | HarmonyOS Support |
| ---------------------------- | -------------------- | ----------- | -------- | ----------- | ----------------- |
| animation                    | 设置图表动画         | object      | No       | iOS/Android | Yes               |
| chartBackgroundColor         | 设置图表背景颜色     | number      | No       | iOS/Android | Yes               |
| logEnabled                   | 启用日志             | bool        | No       | iOS/Android | NO                |
| noDataText                   | 设置无数据文本       | string      | No       | iOS/Android | Yes               |
| noDataTextColor              | 设置无数据文本颜色   | number      | No       | iOS/Android | Yes               |
| touchEnabled                 | 设置触摸             | bool        | No       | iOS/Android | Yes               |
| dragDecelerationEnabled      | 设置拖拽减速         | bool        | No       | iOS/Android | Yes               |
| dragDecelerationFrictionCoef | 设置阻力减速摩擦系数 | function    | No       | iOS/Android | Yes               |
| chartDescription             | 设置描述部件         | Description | No       | iOS/Android | Yes               |
| legend                       | 设置图例             | Legend      | No       | iOS/Android | Yes               |
| xAxis                        | 设置 X 轴            | Xaxis       | No       | iOS/Android | Yes               |
| highlights                   | 设置高亮             | object      | No       | iOS/Android | NO                |

### BarLineChartBase

| Name                   | Description                                                                                   | Type                            | Required | Platform    | HarmonyOS Support |
| ---------------------- | --------------------------------------------------------------------------------------------- | ------------------------------- | -------- | ----------- | ----------------- |
| drawGridBackground     | 是否设置网格背景颜色                                                                          | bool                            | No       | iOS/Android | Yes               |
| gridBackgroundColor    | 设置网格背景颜色                                                                              | number                          | No       | iOS/Android | Yes               |
| drawBorders            | 是否设置边框                                                                                  | bool                            | No       | iOS/Android | Yes               |
| borderColor            | 设置边框颜色                                                                                  | number                          | No       | iOS/Android | Yes               |
| borderWidth            | 设置边框宽度                                                                                  | number                          | No       | iOS/Android | Yes               |
| minOffset              | 设置最小偏移                                                                                  | number                          | No       | iOS/Android | Yes               |
| visibleRange           | 限制通过捏合和缩放可以看到的最大和最小 x 范围                                                 | object                          | No       | iOS/Android | NO                |
| autoScaleMinMaxEnabled | 是否设置 Y 轴的自动缩放标记                                                                   | bool                            | No       | iOS/Android | Yes               |
| keepPositionOnRotation | 设置图表在旋转（方向更改）后是否应保持其位置（缩放/滚动                                       | bool                            | No       | iOS/Android | NO                |
| scaleEnabled           | 是否启用缩放                                                                                  | bool                            | No       | iOS/Android | Yes               |
| scaleXEnabled          | 是否启用 X 轴缩放                                                                             | bool                            | No       | iOS/Android | Yes               |
| scaleYEnabled          | 是否启用 Y 轴缩放                                                                             | bool                            | No       | iOS/Android | Yes               |
| dragEnabled            | 是否设置拖动                                                                                  | bool                            | No       | iOS/Android | Yes               |
| pinchZoom              | 如果设置为 true，则 x 和 y 轴都可以用 2 个手指同时缩放，如果为 false，x 轴和 y 轴可以单独缩放 | bool                            | No       | iOS/Android | Yes               |
| doubleTapToZoomEnabled | 将此属性设置为 true 可通过双击图表启用放大功能                                                | bool                            | No       | iOS/Android | Yes               |
| yAksis                 | 设置 Y 轴                                                                                     | { left: YAksis, right: YAksis } | No       | iOS/Android | Yes               |
| zoom                   | 按给定的比例因子放大或缩小                                                                    | object                          | No       | iOS/Android | Yes               |
| viewPortOffsets        | 设置当前 ViewPort 的自定义偏移（在视图两侧的偏移）                                            | object                          | No       | iOS/Android | Yes               |

### Data Config Type

#### Common

| Name             | Description                                 | Type     | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| colors           | 设置应用于此数据集的颜色,由多个颜色组成     | number[] | No       | iOS/Android | Yes               |
| highlightEnabled | 设置是否高亮                                | bool     | No       | iOS/Android | Yes               |
| drawValues       | 设置绘制值                                  | bool     | No       | iOS/Android | Yes               |
| valueTextSize    | 设置值的文本大小                            | number   | No       | iOS/Android | Yes               |
| valueTextColor   | 设置值的文本颜色                            | number   | No       | iOS/Android | Yes               |
| visible          | 设置值是否可见                              | bool     | No       | iOS/Android | Yes               |
| valueFormatter   | 设置数据格式器                              | string   | No       | iOS/Android | NO                |
| axisDependency   | 设置绘制此数据集所依据的 Y 轴（左轴或右轴） | string   | No       | iOS/Android | Yes               |

#### barLineScatterCandleBubble

| Name           | Description                      | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | -------------------------------- | ------ | -------- | ----------- | ----------------- |
| highlightColor | 设置用于绘制突出显示指示器的颜色 | number | No       | iOS/Android | Yes               |

#### lineScatterCandleRadar

| Name                             | Description                                             | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------------- | ------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| drawVerticalHighlightIndicator   | 启用/禁用垂直突出显示指示器。如果禁用，则不绘制指示器。 | bool   | No       | iOS/Android | Yes               |
| drawHorizontalHighlightIndicator | 启用/禁用水平突出显示指示器。如果禁用，则不绘制指示器   | bool   | No       | iOS/Android | Yes               |
| highlightLineWidth               | 高亮线宽                                                | number | No       | iOS/Android | Yes               |

#### lineRadar

| Name       | Description | Type | Required | Platform    | HarmonyOS Support |
| ---------- | ----------- | ---- | -------- | ----------- | ----------------- |
| fillColor  | 填充颜色    | bool | No       | iOS/Android | Yes               |
| fillAlpha  | 填充透明度  | bool | No       | iOS/Android | Yes               |
| drawFilled | 是否填充    | bool | No       | iOS/Android | Yes               |

#### PieRadarChartBase

| Name            | Description                                  | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | -------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| minOffset       | 设置图表周围的最小偏移量（填充），默认值为 0 | number | No       | iOS/Android | Yes               |
| rotationEnabled | 将此属性设置为 true 可通过触摸启用图表的旋转 | bool   | No       | iOS/Android | Yes               |
| rotationAngle   | 为雷达图的旋转设置偏移量（以度为单位）       | number | No       | iOS/Android | Yes               |

### BarChart

| Name              | Description                                                           | Type    | Required | Platform    | HarmonyOS Support |
| ----------------- | --------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| drawValueAboveBar | 如果设置为 true，则所有值都绘制在其条形上方，而不是绘制在其顶部下方。 | bool    | No       | iOS/Android | Yes               |
| drawBarShadow     | 如果设置为 true，则在每个条形后面绘制一个灰色区域，表示最大值         | bool    | No       | iOS/Android | Yes               |
| data              | 柱状图数据                                                            | BarData | Yes      | iOS/Android | Yes               |

#### BarData Config

| Name                       | Description                                          | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| barShadowColor             | 设置用于绘制条形阴影的颜色                           | number                                                       | No       | iOS/Android | Yes               |
| highlightAlpha             | 设置用于绘制高光的 alpha 值（透明度                  | number                                                       | No       | iOS/Android | Yes               |
| stackLabels                | 为不同值的条形栈设置标签                             | string[]                                                     | No       | iOS/Android | NO                |
| common                     | 公共数据数据                                         | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | 柱状图、条形图、散点图、气泡图、烛台图的公共基础数据 | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |

#### BarData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| X    | X 轴数据    | number | Yes      | iOS/Android | Yes               |
| Y    | Y 轴数据    | number | Yes      | iOS/Android | Yes               |

### HorizontalBarChart

| Name | Description    | Type    | Required | Platform    | HarmonyOS Support |
| ---- | -------------- | ------- | -------- | ----------- | ----------------- |
| data | 水平柱状图数据 | BarData | Yes      | iOS/Android | Yes               |

### CandleStickChart

| Name | Description | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ---------- | -------- | ----------- | ----------------- |
| data | 烛台图数据  | CandleData | Yes      | iOS/Android | Yes               |

#### CandleData Config

| Name                       | Description                                                 | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | 公共数据数据                                                | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | 柱状图、条形图、散点图、气泡图、烛台图的公共基础数据        | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |
| lineScatterCandleRadar     | 柱状图、烛台图、散点图、雷达图的公共基础数据                | Data Config Type.CommonConfigType.lineScatterCandleRadar     | No       | iOS/Android | Yes               |
| barSpace                   | 设置在每个的左侧和右侧留出的空间 烛光                       | number                                                       | No       | iOS/Android | Yes               |
| shadowWidth                | 以像素为单位设置蜡烛阴影线的宽度。                          | number                                                       | No       | iOS/Android | Yes               |
| shadowColor                | 设置所有条目的阴影颜色                                      | number                                                       | No       | iOS/Android | Yes               |
| shadowColorSameAsCandle    | 将阴影颜色设置为与蜡烛颜色相同的颜色                        | bool                                                         | No       | iOS/Android | Yes               |
| neutralColor               | 设置在以下情况下应用于此数据集的唯一颜色 \*打开==关闭。     | number                                                       | No       | iOS/Android | Yes               |
| decreasingColor            | 设置在以下情况下应用于此数据集的唯一颜色 \*打开>关闭。      | number                                                       | No       | iOS/Android | Yes               |
| decreasingPaintStyle       | 设置打开>关闭时的绘制样式                                   | string                                                       | No       | iOS/Android | Yes               |
| increasingColor            | 设置在以下情况下应用于此数据集的唯一颜色 \* open <= close。 | number                                                       | No       | iOS/Android | Yes               |
| increasingPaintStyle       | 设置打开<关闭时的绘制样式                                   | string                                                       | No       | iOS/Android | Yes               |

#### CandleData Values

| Name    | Description | Type   | Required | Platform    | HarmonyOS Support |
| ------- | ----------- | ------ | -------- | ----------- | ----------------- |
| x       | X 轴数据    | number | No       | iOS/Android | Yes               |
| shadowH | 阴影 H      | number | Yes      | iOS/Android | Yes               |
| shadowL | 阴影 L      | number | Yes      | iOS/Android | Yes               |
| open    | 打开的      | number | Yes      | iOS/Android | Yes               |
| close   | 关闭的      | number | Yes      | iOS/Android | Yes               |

### CombinedChart

| Name | Description | Type         | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------------ | -------- | ----------- | ----------------- |
| data | 组合图数据  | combinedData | Yes      | iOS/Android | Yes               |

#### combinedData

| Name        | Description | Type        | Required | Platform    | HarmonyOS Support |
| ----------- | ----------- | ----------- | -------- | ----------- | ----------------- |
| lineData    | 折线图数据  | lineData    | No       | iOS/Android | Yes               |
| barData     | 柱状图数据  | barData     | No       | iOS/Android | Yes               |
| scatterData | 散点图数据  | scatterData | No       | iOS/Android | Yes               |
| candleData  | 烛台图数据  | candleData  | No       | iOS/Android | Yes               |
| bubbleData  | 气泡图数据  | bubbleData  | No       | iOS/Android | Yes               |

### BubbleChart

| Name | Description | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ---------- | -------- | ----------- | ----------------- |
| data | 气泡图数据  | bubbleData | Yes      | iOS/Android | Yes               |

#### BubbleData Config

| Name                       | Description                                          | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | 公共数据数据                                         | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | 柱状图、条形图、散点图、气泡图、烛台图的公共基础数据 | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |

#### BubbleData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| x    | X 轴数据    | number | No       | iOS/Android | Yes               |
| y    | Y 轴数据    | number | Yes      | iOS/Android | Yes               |
| size | 大小        | number | Yes      | iOS/Android | Yes               |

### LineChart

| Name | Description | Type     | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | -------- | -------- | ----------- | ----------------- |
| data | 折线图数据  | LineData | Yes      | iOS/Android | Yes               |

#### LineData Config

| Name                       | Description                                                     | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | --------------------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | 公共数据数据                                                    | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | 柱状图、条形图、散点图、气泡图、烛台图的公共基础数据            | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |
| lineScatterCandleRadar     | 柱状图、烛台图、散点图、雷达图的公共基础数据                    | Data Config Type.CommonConfigType.lineScatterCandleRadar     | No       | iOS/Android | Yes               |
| lineRadar                  | 折线图、雷达图公共数据                                          | Data Config Type.lineRadar                                   | No       | iOS/Android | Yes               |
| circleRadius               | 设置绘制的圆的半径                                              | number                                                       | No       | iOS/Android | Yes               |
| drawCircles                | 将此值设置为 true 以启用此的圆圈指示器的绘制数据集，默认为 true | bool                                                         | No       | iOS/Android | Yes               |
| mode                       | 设置 lineDataSet 的绘制模式                                     | object                                                       | No       | iOS/Android | Yes               |
| lineWidth                  | 折线宽度                                                        | number                                                       | No       | iOS/Android | Yes               |
| drawCubicIntensity         | 设置曲线弧度                                                    | number                                                       | No       | iOS/Android | NO                |
| circleColor                | 设置应该用于此数据集的唯一颜色                                  | number                                                       | No       | iOS/Android | Yes               |
| circleColors               | 设置应该用于此数据集的颜色集                                    | number[]                                                     | No       | iOS/Android | Yes               |
| circleHoleColor            | 设置线条圆的内圆的颜色。                                        | number                                                       | No       | iOS/Android | Yes               |
| drawCircleHole             | 许在每个数据圆圈中绘制一个孔                                    | bool                                                         | No       | iOS/Android | Yes               |
| dashedLine                 | 折线设置为虚线                                                  | object                                                       | No       | iOS/Android | Yes               |
| fillFormatter              | 设置填充                                                        | object                                                       | No       | iOS/Android | Yes               |

#### LineData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| x    | X 轴数据    | number | No       | iOS/Android | Yes               |
| y    | Y 轴数据    | number | Yes      | iOS/Android | Yes               |

### ScatterChart

| Name | Description | Type        | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ----------- | -------- | ----------- | ----------------- |
| data | 散点图数据  | ScatterData | Yes      | iOS/Android | Yes               |

#### ScatterData Config

| Name                       | Description                                          | Type                                                         | Required | Platform    | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| common                     | 公共数据数据                                         | Data Config Type.Common                                      | No       | iOS/Android | Yes               |
| barLineScatterCandleBubble | 柱状图、条形图、散点图、气泡图、烛台图的公共基础数据 | Data Config Type.CommonConfigType.barLineScatterCandleBubble | No       | iOS/Android | Yes               |
| lineScatterCandleRadar     | 柱状图、烛台图、散点图、雷达图的公共基础数据         | Data Config Type.CommonConfigType.lineScatterCandleRadar     | No       | iOS/Android | Yes               |

#### ScatterData Values

| Name | Description | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------- | ----------------- |
| x    | X 轴数据    | number | No       | iOS/Android | Yes               |
| y    | Y 轴数据    | number | Yes      | iOS/Android | Yes               |

### PieChart

| Name                    | Description                                                                       | Type    | Required | Platform    | HarmonyOS Support |
| ----------------------- | --------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| extraOffsets            | 图数据                                                                            | object  | No       | iOS/Android | Yes               |
| drawEntryLabels         | 将此属性设置为 true 可将条目标签绘制到饼图扇区中                                  | bool    | No       | iOS/Android | Yes               |
| usePercentValues        | 如果启用此选项，则 PieChart 中的值将以百分比显示                                  | bool    | No       | iOS/Android | Yes               |
| centerText              | 设置显示在 PieChart 中心的文本字符串。                                            | string  | No       | iOS/Android | Yes               |
| styledCenterText        | 设置显示在 PieChart 中心的文本字符串的样式                                        | object  | No       | iOS/Android | Yes               |
| centerTextRadiusPercent | 中心文本边界框的矩形半径,以饼图的百分比表示                                       | number  | No       | iOS/Android | Yes               |
| holeRadius              | 设置饼图中心孔的半径，以百分比为单位 \*最大半径（max=整个图表的半径），默认为 50% | number  | No       | iOS/Android | Yes               |
| holeColor               | 设置在饼图中心绘制的孔的颜色                                                      | number  | No       | iOS/Android | Yes               |
| transparentCircleRadius | 设置在孔旁边绘制的透明圆的半径                                                    | number  | No       | iOS/Android | Yes               |
| transparentCircleColor  | 设置在孔旁边绘制的透明圆的颜色                                                    | number  | No       | iOS/Android | Yes               |
| entryLabelColor         | 设置绘制条目标签的颜色                                                            | number  | No       | iOS/Android | Yes               |
| entryLabelTextSize      | 以 vp 为单位设置条目标签的大小。                                                  | number  | No       | iOS/Android | Yes               |
| entryLabelFontFamily    | 为条目标签的绘制设置自定义字体                                                    | string  | No       | iOS/Android | Yes               |
| maxAngle                | 设置用于计算饼图圆的最大角度                                                      | number  | No       | iOS/Android | Yes               |
| data                    | 饼图数据                                                                          | PieData | Yes      | iOS/Android | Yes               |

#### PieData Config

| Name              | Description                            | Type                               | Required | Platform    | HarmonyOS Support |
| ----------------- | -------------------------------------- | ---------------------------------- | -------- | ----------- | ----------------- |
| common            | 公共数据数据                           | Data Config Type.Common            | No       | iOS/Android | Yes               |
| PieRadarChartBase | 饼图、雷达图数据                       | Data Config Type.PieRadarChartBase | No       | iOS/Android | Yes               |
| sliceSpace        | 设置在 vp 中的饼图切片之间留出的空间。 | number                             | No       | iOS/Android | Yes               |
| selectionShift    | 设置此数据集的突出显示饼图扇区的距离   | number                             | No       | iOS/Android | Yes               |
| xValuePosition    | 标签显示在饼图里面还是外面             | string                             | No       | iOS/Android | Yes               |
| yValuePosition    | 标签显示在饼图里面还是外面             | string                             | No       | iOS/Android | Yes               |

#### PieData Values

| Name  | Description | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------ | -------- | ----------- | ----------------- |
| value | 数据        | number | Yes      | iOS/Android | Yes               |
| label | 标签        | number | No       | iOS/Android | Yes               |

### RadarChart

| Name              | Description                                          | Type                               | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------- | ---------------------------------- | -------- | ----------- | ----------------- |
| yAxis             | Y 轴                                                 | YAxis                              | No       | iOS/Android | Yes               |
| drawWeb           | 饼图、雷达图数据                                     | Data Config Type.PieRadarChartBase | No       | iOS/Android | Yes               |
| skipWebLineCount  | 设置在执行以下操作之前应在图表 Web 上跳过的 Web 行数 | number                             | No       | iOS/Android | Yes               |
| webLineWidth      | 设置来自中心的腹板线的宽度                           | number                             | No       | iOS/Android | Yes               |
| webLineWidthInner | 设置 Web 线的宽度，这些 Web 线位于来自 \*中心。      | number                             | No       | iOS/Android | Yes               |
| webAlpha          | 设置所有 Web 线的透明度（alpha）值                   | number                             | No       | iOS/Android | Yes               |
| webColor          | 设置来自中心的腹板线的颜色。                         | number                             | No       | iOS/Android | Yes               |
| webColorInner     | 设置 Web 线之间的颜色，这些线来自\*中心。            | number                             | No       | iOS/Android | Yes               |
| data              | 雷达图数据                                           | RadarData                          | Yes      | iOS/Android | Yes               |

#### RadarData Config

| Name                   | Description                                  | Type                                                     | Required | Platform    | HarmonyOS Support |
| ---------------------- | -------------------------------------------- | -------------------------------------------------------- | -------- | ----------- | ----------------- |
| common                 | 公共数据数据                                 | Data Config Type.Common                                  | No       | iOS/Android | Yes               |
| lineScatterCandleRadar | 柱状图、烛台图、散点图、雷达图的公共基础数据 | Data Config Type.CommonConfigType.lineScatterCandleRadar | No       | iOS/Android | Yes               |
| lineRadar              | 折线图、雷达图公共数据                       | Data Config Type.lineRadar                               | No       | iOS/Android | Yes               |

#### RadarData Values

| Name  | Description | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------- | ------ | -------- | ----------- | ----------------- |
| value | 数据        | number | Yes      | iOS/Android | Yes               |

## 遗留问题

## 其他
- [ ] 图例的maxSizePercent最大百分比属性在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/995)
- [ ] 图例的custom属性，设置后会覆盖原有的图例，但自定义图例也不显示在Android和iOS中，属性不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/996)
- [ ] logEnabled 会开启安卓特有的日志logcat和 highlights属性在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/998)
- [ ] stackLabels 堆叠条形图设置无效果和 drawCubicIntensity 曲线角度属性在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/997)
- [ ] 在Android和iOS visibleRange 最大大小百分比限制通过缩放和缩放可以看到的最大和最小x范围不起作用， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/999)
- [ ] keepPositionOnRotation旋转后保持图表原始位置属性在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/999)
- [ ] valueFormatter格式化数据属性在Android和iOS不生效， HarmonyOS与Android,iOS表现一致。[原库 issue](https://github.com/wuxudong/react-native-charts-wrapper/issues/935)
## 开源协议

本项目基于 [The MIT License (MIT)](https://mitlicense.org/) ，请自由地享受和参与开源。
