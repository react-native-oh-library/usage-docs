> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-gifted-charts</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/Abhinandan-Kushwaha/react-native-gifted-charts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Abhinandan-Kushwaha/react-native-gifted-charts/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-gifted-charts)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-gifted-charts Releases](https://github.com/react-native-oh-library/react-native-gifted-charts/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-gifted-charts@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-gifted-charts@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import { BarChart, LineChart, PieChart, PopulationPyramid } from "react-native-gifted-charts";

export default function () {
  const data = [{ value: 50 }, { value: 80 }, { value: 90 }, { value: 70 }];

  return (
    <>
      <BarChart data={data} />
      <LineChart data={data} />
      <PieChart data={data} />
      <PopulationPyramid data={[{ left: 10, right: 12 }, { left: 9, right: 8 }]} />
      <BarChart data={data} horizontal />
      <LineChart data={data} areaChart />
      <PieChart data={data} donut />
    </>
  )
}
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-svg、@react-native-oh-tpl/react-native-linear-gradient 的原生端代码，如已在鸿蒙工程中引入过这两个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档](/zh-cn/react-native-svg-capi.md)、[@react-native-oh-tpl/react-native-linear-gradient 文档](/zh-cn/react-native-linear-gradient.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-gifted-charts Releases](https://github.com/react-native-oh-library/react-native-gifted-charts/releases)

## 属性

详情见 [react-native-gifted-charts](https://github.com/Abhinandan-Kushwaha/react-native-gifted-charts) Props tables

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### BarChart, Horizontal BarChart and Stacked Bar Chart

**Basic props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An item object represents a bar in the bar chart. It is described in the next table. | barDataItem[]  | no     | all | yes
| width  | Width of the Bar chart |  number | no  | all | yes
| height   | Height of the Bar chart (excluding the bottom label)  | number | no  | all | yes
| onPress  | Callback function called on press of a Bar (takes item and index as parameter)    | Function | no  | all | yes
| onLongPress | Callback function called on long press of a Bar (takes item and index as parameter) | Function | no  | all | yes
| onPressOut   | Callback function called on press out of a Bar (takes item and index as parameter) | Function | no  | all | yes        
| focusBarOnPress  | used to focus a bar on press by applying styles defined in focusedBarConfig | boolean | no  | all | yes   
| focusedBarConfig  | styles for the focused bar including color, width, opacity, borderRadius etc   | FocusedBarConfig | no  | all | yes     
| focusedBarIndex    | index of the initially focused bar, works only when focusBarOnPress is  | number  | no  | all | yes     
| maxValue  | Maximum value shown in the Y axis   | number  | no  | all | yes     
| yAxisOffset   | Starting (minimum) value in the Y axis (value at the origin)  | number | no  | all | yes
| mostNegativeValue  | The most negative value shown in the Y axis (to be used only if the data set has negative values too)  | number | no  | all | yes     
| noOfSections | Number of sections in the Y axis   | number  | no  | all | yes
| noOfSectionsBelowXAxis | Number of sections in the Y axis below X axis (in case the data set has negative values too)       | number  | no  | all | yes
| stepValue | Value of 1 step/section in the Y axis | number  | no  | all | yes
| stepHeight | Height of 1 step/section in the Yaxis | number  | no  | all | yes
| negativeStepValue| Value of 1 step/section in the Y axis for negative values (in the 4th quadrant) | number | no  | all | yes
| negativeStepHeight | Height of 1 step/section in the Y axis for negative values (in the 4th quadrant)  | number  | no  | all | yes
| spacing   | Distance between 2 consecutive bars in the Bar chart  | number | no  | all | yes
| backgroundColor | Background color of the Bar chart  | ColorValue | no  | all | yes
| sectionColors | Background color of the horizontal sections of the chart | ColorValue  | no  | all | yes
| scrollref   | ref object that can be used to control the horizontal ScrollView inside which the chart is rendered | any  | no  | all | yes
| scrollToIndex  | scroll to a particular index on chart load | number | no  | all | yes
| disableScroll | To disable horizontal scroll | boolean | no  | all | yes
| showScrollIndicator | To show horizontal scroll indicator| boolean | no  | all | yes
| indicatorColor  |  (iOS only) The color of the scroll indicators - ('black', 'white' or 'default') | String  | no  | iOS | yes
| showLine  | To show a Line chart over the Bar chart with the same data  | boolean | no  | all | yes
| lineData   | The data object for the line chart (use only when showLine is true). To hide any datapoint pass hideDataPoint prop as true in specific data item. | Array of items | no  | all | yes
| lineConfig  | Properties of the Line chart shown over the Bar chart (lineConfigType) is described below  | lineConfigType  | no  | all | yes
| lineData2  | The data object for the second line chart (use only when showLine is true)  | Array of items | no  | all | yes
| lineConfig2   | Properties of the second Line chart shown over the Bar chart (lineConfigType) is described below  | lineConfigType  | no  | all | yes
| lineBehindBars  | When set to true, the line chart will appear behind the Bars in case of overlap    | boolean  | no  | all | yes
| autoShiftLabels  | When set to true, automatically shifts the X axis labels for negative values | boolean  | no  | all | yes
| scrollToEnd  | When set to true, the chart automatically scrolls to the rightmost bar  | boolean  | no  | all | yes
| scrollAnimation   | When set to true, scroll animation is visible when the chart automatically scrolls to the rightmost bar | boolean | no  | all | yes
| scrollEventThrottle  | (only for iOS) see https://reactnative.dev/docs/scrollview#scrolleventthrottle-ios| number | no  | iOS | yes
| onScroll  | callback function called when the chart is scrolled horizontally    | Function | no  | all | yes
| onMomentumScrollEnd    | callback function called when scroll is completed       | Function  | no  | all | yes
| initialSpacing  | distance of the first bar from the Y axis | number  | no  | all | yes
| renderTooltip    | tooltip component appearing above the bar when it is pressed, takes item and index as parameters     | Function  | no  | all | yes
| leftShiftForTooltip  | The distance by which the tooltip component should shift towards left | number | no  | all | yes
| leftShiftForLastIndexTooltip | The distance by which the tooltip component of the last bar should shift towards left | number  | no  | all | yes
| adjustToWidth   | When set to true, it auto-computes the barWidth and spacing to fit the chart in the available width / parentWidth  | boolean   | no  | all | yes
| parentWidth  | The width of the parent View or the width that the chart should auto-fit into when `adjustToWidth` is true | number | no  | all | yes 

**Combine Line Chart using showLine**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| initialSpacing | distance of the first data point from the Y axis  | number   | no  | all | yes
| curved  | To show curved line joining the data points | boolean  | no  | all | yes
| isAnimated | To show animates Line Chart | boolean  | no  | all | yes
| delay | Delay (in milliseconds) before starting the animation of the line | number   | no  | all | yes
| thickness | Thickness of the Line  | number | no  | all | yes
| color  | Color of the Line | ColorValue   | no  | all | yes
| hideDataPoints  | To hide data points along the Line chart | boolean   | no  | all | yes
| dataPointsShape | Shape of the data points (_'rectangular'_ or _'circular'_) | String   | no  | all | yes
| dataPointsWidth | Width of data points (when data points' shape is rectangular) | number   | no  | all | yes
| dataPointsHeight | Height of data points (when data points' shape is rectangular) | number    | no  | all | yes
| dataPointsColor  | Color of the data points | ColorValue  | no  | all | yes
| dataPointsRadius | Radius of data points (when data points' shape is _circular_)  | number   | no  | all | yes
| textColor | Color of the dataPointText  | ColorValue    | no  | all | yes
| textFontSize | Font size of the dataPointText | number  | no  | all | yes
| textShiftX | To shift the dataPointText text horizontally | number    | no  | all | yes
| textShiftY | To shift the dataPointText text vertically | number   | no  | all | yes
| shiftY | To shift the Line chart up or down by the given quantity m  | number   | no  | all | yes
| startIndex | Start index for data line (used to display data lines having breaks) | number   | no  | all | yes
| endIndex | End index for data line (used to display data lines having breaks) | number   | no  | all | yes

**Item description (barDataItem)**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| value | Value of the item representing height of the bar | number  | no  | all | yes
| barWidth | Width of the bar | number  | no  | all | yes
| onPress | Function called on pressing the bar | function | no  | all | yes
| onLongPress | Function called on long pressing the bar | function   | no  | all | yes
| onPressOut | Callback function called on press out of a bar | Function  | no  | all | yes
| disablePress | Prop to disable the press action, defaults to false | boolean    | no  | all | yes
| frontColor | Color of the bar | ColorValue  | no  | all | yes
| sideColor | Color of the side view of the bar, only for 3 D | ColorValue | no  | all | yes
| sideWidth | Width of the side view of the bar, only for 3 D  | number | no  | all | yes
| topColor | Color of the top view of the bar, only for 3 D | ColorValue | no  | all | yes
| barStyle | style object for the Bars | object  | no  | all | yes
| showGradient | Prop to enable linear gradient for the bar color, defaults to false | boolean  | no  | all | yes
| gradientColor | Along with frontColor, this prop constitutes the 2 colors for gradient | ColorValue | no  | all | yes
| label | Label text appearing below the bar (under the X axis)  | string   | no  | all | yes
| labelWidth | Width of the Label text appearing below the bar (under the X axis) | number | no  | all | yes
| labelTextStyle | Style object for the label text appearing below the bar | object | no  | all | yes
| labelComponent | Custom label component appearing below the bar | Component | no  | all | yes
| labelsDistanceFromXaxis | Distance of the X Axis label from the X axis | number  | no  | all | yes
| topLabelComponent | Custom component appearing above the bar  | Component | no  | all | yes
| topLabelContainerStyle | Style object for the container of the custom component appearing above the bar| object  | no  | all | yes
| cappedBars | To show caps on the top of bar | boolean | no  | all | yes
| capThickness | Thickness of the bar cap | number | no  | all | yes
| capColor | Color of the bar cap | ColorValue | no  | all | yes
| capRadius | Border radius of the bar cap | number  | no  | all | yes
| barBorderRadius | Border radius of the bar | number | no  | all | yes
| barBorderTopLeftRadius | Top left border radius of the bar | number| no  | all | yes
| barBorderTopRightRadius | Top right border radius of the bar | number   | no  | all | yes
| barBorderBottomLeftRadius | Bottom left border radius of the bar | number  | no  | all | yes
| barBorderBottomRightRadius | Bottom right border radius of the bar| number | no  | all | yes
| barMarginBottom  | margin at the bottom of the bar (above X axis)   | number  | no  | all | yes
| spacing  | Distance of the next Bar from the currennt Bar  | number  | no  | all | yes
| barBackgroundPattern  | A svg component containing the background pattern for bars | Component | no  | all | yes
| patternId  | ID of the pattern component  | String | no  | all | yes
| leftShiftForTooltip | The distance by which the tooltip component should shift towards left | number | no  | all | yes
| showXAxisIndex  | show small graduation at the X axis for the corresponding bar  | boolean  | no  | all | yes

**Axes and rules related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| xAxisLength | X axis length | number  | no  | all | yes
| xAxisColor | X axis color  | ColorValue  | no  | all | yes
| xAxisThickness | X axis thickness | number   | no  | all | yes
| yAxisColor | Y axis color | ColorValue   | no  | all | yes
| yAxisThickness | Y axis thickness | number   | no  | all | yes
| yAxisExtraHeight | Extra length of Y axis at the top | number  | no  | all | yes
| xAxisType | solid or dotted/dashed | RuleType   | no  | all | yes
| yAxisLabelWidth | Width of the Y axis Label container | number  | no  | all | yes
| yAxisTextStyle | Style object for the Y axis text style | object | no  | all | yes
| yAxisTextNumberOfLines | Number of lines for y axis label text | number  | no  | all | yes
| yAxisLabelContainerStyle | Style object for the Y axis label container | object   | no  | all |  yes
| trimYAxisAtTop  | Removes the extra length of the Y axis from the top  | boolean   | no  | all | yes
| horizontalRulesStyle | Style object for the horizontal rules container | object   | no  | all | yes
| showFractionalValues | Allow fractional values for the Y axis label | boolean   | no  | all | yes
| roundToDigits | Rounds the y axis values to given number of digits after decimal point | number   | no  | all | yes
| yAxisLabelPrefix | The String prepended to the y axis label text (for example- '$') | String  | no  | all | yes
| yAxisLabelSuffix | The String appended to the y axis label text | String   | no  | all | yes
| hideYAxisText | To hide Y axis label text | boolean   | no  | all | yes  
| formatYLabel | a callback function that takes the label generated by the library and modifies it. | (label: string) => string |  no  | all | yes
| yAxisSide | Tells which side of the chart, should the y axis be present, defaults to 'left' | String  | no  | all |  yes
| rulesLength | Length of the horizontal rules | number   | no  | all | yes
| rulesColor  | Color of the horizontal rules   | ColorValue   | no  | all | yes
| rulesThickness | Thickness of the horizontal rules | number  | no  | all | yes
| hideRules | To hide the horizontal rules | boolean   | no  | all | yes
| rulesType  | solid or dotted/dashed | RuleType   | no  | all | yes
| dashWidth | width of each dash | number  | no  | all | yes
| dashGap | gap between 2 dashes | number   | no  | all | yes
| rulesConfigArray | Array of rulesConfig objects, used to customise the properties (like color, type etc) of specific rules | Array<RulesConfig> | no  | all | yes
| referenceLine1Config | properties of reference line like thickness, color etc (described below the table) | referenceConfigType   | no  | all | yes
| referenceLine1Position | position of reference line | number    | no  | all | yes
| showReferenceLine2 | show second reference line | boolean  | no  | all | yes
| referenceLine2Config | properties of reference line like thickness, color etc (described below the table) | referenceConfigType  | no  | all | yes
| referenceLine2Position | position of second reference line | number   | no  | all | yes
| showReferenceLine3 | show third reference line  | boolean     | no  | all | yes
| referenceLine3Config | properties of reference line like thickness, color etc (described below the table)    | referenceConfigType   | no  | all | yes
| referenceLine3Position | position of third reference line | number   | no  | all | yes
| referenceLinesOverChartContent | used to render the reference lines over the rest of the chart content. | boolean   | no  | all | yes
| showVerticalLines | To show vertical lines | boolean   | no  | all | yes
| verticalLinesColor | Color of the vertical lines  | ColorValue  | no  | all | yes
| verticallinesThickness  | Thickness of the vertical lines | number    | no  | all | yes
| verticalLinesHeight | Height of the vertical lines | number   | no  | all | yes
| verticalLinesStrokeDashArray | Array of 2 numbers denoting the dashWidth and dashGap of the lines. Used to render dashed/dotted vertical line  | Array<number>   | no  | all | yes
| verticalLinesShift | vertical lines are aligned with bars. Shift them left or right using +ve or -ve value of verticalLinesShift  | number   | no  | all | yes
| verticalLinesZIndex | Z index of the vertical lines | number  | no  | all | yes
| noOfVerticalLines | Number of vertical lines displayed | number  | no  | all | yes
| verticalLinesSpacing  | Distance between consecutive vertical lines | number    | no  | all | yes
| showXAxisIndices | To show the pointers on the X axis  | boolean   | no  | all | yes
| xAxisIndicesHeight | Height of the pointers on the X axis | number   | no  | all | yes
| xAxisIndicesWidth | Width of the pointers on the X axis | number   | no  | all | yes
| xAxisIndicesColor | Color of the pointers on the X axis  | ColorValue   | no  | all | yes
| showYAxisIndices  | To show the pointers on the Y axis  | boolean     | no  | all | yes
| yAxisIndicesHeight  | Height of the pointers on the Y axis  | number   | no  | all | yes
| yAxisIndicesWidth | Width of the pointers on the Y axis | number   | no  | all | yes
| yAxisIndicesColor | Color of the pointers on the X axis  | ColorValue  | no  | all | yes
| yAxisLabelTexts  | Array of label texts to be displayed along y axis | Array<string>   | no  | all | yes
| xAxisLabelTexts | Array of label texts to be displayed below x axis | Array<string>   | no  | all | yes
| xAxisLabelTextStyle | Style of label texts to be displayed below x axis | object  | no  | all | yes
| rotateLabel | To rotate the X axis labels (by 60deg) | boolean   | no  | all | yes
| hideAxesAndRules | To hide axes, rules, labels altogether  | boolean  | no  | all | yes
| hideOrigin | To hide the y Axis label at origin (i.e. 0)  | boolean   | no  | all | yes
| labelWidth | Width of the Label text appearing below the bar (under the X axis) | number   | no  | all | yes
| labelsDistanceFromXaxis | Distance of the X Axis label from the X axis  | number   | no  | all | yes
| xAxisTextNumberOfLines | Number of lines for x axis label text | number  | no  | all | yes
| xAxisLabelsHeight | Height of X axis labels container    | number   | no  | all | yes
| xAxisLabelsVerticalShift | prop to adjust the vertical position of X axis labels (move X axis labels up or down)     | number  | no  | all | yes
| labelsExtraHeight | used to display large rotated labels on X-axis (use this only when using the **rotateLabel** prop) | number   | no  | all | yes
| secondaryYAxis | displays and controls the properties of the secondary Y axis on the right side | secondaryYAxisType  | no  | all | yes
| secondaryData | the secondary data that will be rendered along the secondary Y axis  | Array of items   | no  | all | yes           

**Bar related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| barWidth | Width of the bar | number    | no  | all | yes
| barStyle | style object for the Bars | object    | no  | all | yes
| isThreeD | Prop to render 3 dimensional bars | boolean   | no  | all | yes
| frontColor | Color of the bar | ColorValue   | no  | all | yes
| sideColor | Color of the side view of the bar, only for 3 D | ColorValue    | no  | all | yes
| topColor | Color of the top view of the bar, only for 3 D | ColorValue   | no  | all | yes
| sideWidth | Width of the side view of the bar, only for 3 D  | number   | no  | all | yes
| showGradient | Prop to enable linear gradient for the bar color | boolean    | no  | all | yes
| gradientColor | Along with frontColor, gradientColor constitutes the 2 colors for gradient | ColorValue    | no  | all | yes
| roundedTop | To show rounded top | boolean     | no  | all | yes
| roundedBottom | To show rounded bottom  | boolean   | no  | all | yes
| activeOpacity  | activeOpacity on pressing the bar | number    | no  | all | yes
| disablePress | Prop to disable the bar press action | boolean    | no  | all | yes
| barBorderWidth | Border width of the bar | number    | no  | all | yes
| barBorderColor | Border color of the bar  | ColorValue | no  | all | yes
| barBorderRadius | Border radius of the bar | number | no  | all | yes
| barBorderTopLeftRadius | Top left border radius of the bar | number | no  | all | yes
| barBorderTopRightRadius | Top right border radius of the bar   | number | no  | all | yes
| barBorderBottomLeftRadius | Bottom left border radius of the bar | number | no  | all | yes
| barBorderBottomRightRadius | Bottom right border radius of the bar | number | no  | all | yes
| barMarginBottom | margin at the bottom of the bar (above X axis)  | number | no  | all | yes
| barBackgroundPattern | A svg component containing the background pattern for bars | Component  | no  | all | yes
| patternId  | ID of the pattern component | String  | no  | all | yes
| minHeight | Minimum height of the Bars | number  | no  | all | yes

**Animation related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isAnimated | To show animates BarChart. Animation occurs onLoad and on value change | boolean   | no  | all | yes
| animationDuration | Duration of the animations | number  | no  | all | yes
| animationEasing   | Easing applied to the animation  | Easing  | no  | all | yes

**Pagination related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onEndReached | Callback function called when the chart is scrolled upto end  | Function   | no  | all | yes
| onStartReached | Callback function called when the chart is scrolled upto start   | Function   | no  | all | yes

**Bar related props for making Capped Bar chart**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| cappedBars | To show caps on the top of bars   | boolean  | no  | all | yes
| capThickness | Thickness of the bar caps  | number   | no  | all | yes
| capColor | Color of the bar caps     | ColorValue   | no  | all | yes
| capRadius | Border radius of the bar caps   | number  | no  | all | yes

**pointerConfig**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| height | Height of the pointer |  number  | no  | all | yes
| width  | width of the pointer |  number  | no  | all | yes
| radius  | radius of the pointer   |  number  | no  | all | yes
| pointerColor  |  pointer color   |  ColorValue  | no  | all | yes
| pointerColorsForDataSet | When using pointers with dataSet, you can set pointer colors on each data line using the pointerColorsForDataSet which is an array of color values.  |  ColorValue[]  | no  | all | yes
| secondaryPointerColor | Secondary pointer color  |  ColorValue  | no  | all | yes
| pointerComponent | is a function that returns the component to be rendered as a pointer  |  Function  | no  | all | yes
| showPointerStrip | show pointer bar |  boolean  | no  | all | yes
| pointerStripWidth  | width of the pointer bar |  number  | no  | all | yes
| pointerStripHeight  | height of the pointer bar  |  number  | no  | all | yes
| pointerStripColor  | color of the pointer bar   |  ColorValue  | no  | all | yes
| pointerStripUptoDataPoint | Pointer stripped to data point  |  boolean  | no  | all | yes
| pointerLabelComponent | is a function that returns the component to be rendered as a Label. It takes 2 parameters - 1. an array of items 2 |  Function  | no  | all | yes
| stripOverPointer | strip to over pointer  |  boolean  | no  | all | yes
| autoAdjustPointerLabelPosition | Adjust the position of the pointer  |  boolean  | no  | all | yes
| shiftPointerLabelX | x-axis displacement pointer label  |  number  | no  | all | yes
| shiftPointerLabelY | y-axis displacement pointer label  |  number  | no  | all | yes
| pointerLabelWidth  | pointer label width |  number  | no  | all | yes
| pointerLabelHeight | pointer label height |  number  | no  | all | yes
| pointerVanishDelay | Pointer disappearance delay |  number  | no  | all | yes
| activatePointersOnLongPress |Long press to activate pointer  |  boolean  | no  | all | yes
| activatePointersDelay | activation pointer delay |  number  | no  | all | yes
| persistPointer | persistent pointer |  boolean  | no  | all | yes
| strokeDashArray | Array of 2 numbers denoting the dashWidth and dashGap of the lines. Used to render dashed/dotted pointer |  number[]  | no  | all | yes
| barTouchable  | touchable bar |  boolean  | no  | all | yes
| pointerEvents | pointer event in Bars |  PointerEvents  | no  | all | yes
| stripBehindBars | hide the strip in Bars |  boolean  | no  | all | yes

**Props for horizontal BarChart**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| horizontal | Render horizontal        | boolean   | no  | all | yes
| rtl | Render the chart from right to left | boolean   | no  | all | yes
| shiftX  | Shift the chart towards left or right by given value (only in horizontal charts) | number  | no  | all | yes
| shiftY  | Shift the chart upwards or downwards by given value (only in horizontal charts)  | number  | no  | all | yes
| rotateYAxisTexts | angle by which the Y axis label texts should rotate in horizontal charts | number   | no  | all | yes
| yAxisAtTop | In horizontal BarCharts the Y axis appears at bottom by default. Set it to true for otherwise | boolean  | no  | all | yes
| intactTopLabel | To rotate the top label component to make it intact with the Bars    | boolean   | no  | all | yes

**Props for Stacked Bar Charts**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| stackData   | A stack array represents a stack of bars in the bar chart. It is described in the next table  | Array of stack arrays | no  | all | yes
| barBorderRadius | Border radius of each bar of the stack  | number| no  | all | yes
| barBorderTopLeftRadius | Top left border radius of each bar of the stack | number| no  | all | yes
| barBorderTopRightRadius | Top right border radius of each bar of the stack | number | no  | all | yes
| barBorderBottomLeftRadius | Bottom left border radius of each bar of the stack | number | no  | all | yes
| barBorderBottomRightRadius | Bottom right border radius of each bar of the stack | number | no  | all | yes
| stackBorderRadius | Border radius of the top and bottom bars of the stack  | number | no  | all | yes
| stackBorderTopLeftRadius | Top left border radius of the top bar of the stack | number| no  | all | yes
| stackBorderTopRightRadius | Top right border radius of the top bar of the stack  | number | no  | all | yes
| stackBorderBottomLeftRadius  | Bottom left border radius of the bottom bar of the stack      | number  | no  | all | yes
| stackBorderBottomRightRadius  | Bottom right border radius of the bottom bar of the stack     | number | no  | all | yes
| autoShiftLabelsForNegativeStacks | Whether the x axis labels should auto shift to a position below the bar, if the bar is under x-axis due to negative value | boolean| no  | all | yes

**Stack Array description**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| stacks array | A stack is made of 1 or more objects of the type described in the next table |  Array of stack items| no  | all | yes                                      
| label | Label text appearing below the stack (under the X axis) | string | no  | all | yes
| labelTextStyle  | Style object for the label text appearing below the stack | object| no  | all | yes
| barWidth     | Width of the stack bar | number| no  | all | yes
| spacing | Distance between 2 consecutive bars in the stack Bar chart | number| no  | all | yes
| borderRadius | Border radius of each bar of the stack | number| no  | all | yes
| borderTopLeftRadius | Top left border radius of the top bar of the stack     | number| no  | all | yes
| borderTopRightRadius | Top right border radius of the top bar of the stack   | number| no  | all | yes
| borderBottomLeftRadius  | Bottom left border radius of the bottom bar of the stack  | number| no  | all | yes
| borderBottomRightRadius | Bottom right border radius of the bottom bar of the stack | number| no  | all | yes

**Stack item description**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| value   | Value of the item representing height of the stack item | number | no  | all | yes
| color | Color of the stack item | ColorValue | no  | all | yes
| onPress |  Function called on pressing the stack item | function | no  | all | yes
| onLongPress    | Function called on long pressing the stack item | function | no  | all | yes
| onPressOut   | Callback function called on press out of a bar | Function  | no  | all | yes
| marginBottom | margin below a particular stack sectio | number     n   | no  | all | yes
| barBorderRadius   | Border radius of a stack section  | number  | no  | all | yes
| borderTopLeftRadius   | borderTopLeftRadius for a stack section  | number | no  | all | yes
| borderTopRightRadius  | borderTopRightRadius for a stack section    | number | no  | all | yes
| borderBottomLeftRadius | borderBottomLeftRadius for a stack section  | number   | no  | all | yes
| borderBottomRightRadius | borderBottomRightRadius for a stack section | number  | no  | all | yes
| showGradient | Prop to enable linear gradient for the bar color, defaults to false | boolean | no  | all | yes
| gradientColor | Along with frontColor, this prop constitutes the 2 colors for gradient| ColorValue | no  | all | yes
| barWidth | Width of the bar | number | no  | all | yes
| showXAxisIndex | show small graduation at the X axis for the corresponding stack  | boolean  | no  | all | yes

### LineChart and AreaChart

**Basic props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data | An item object represents a point in the line chart. It is described in the next table.   | Array <lineDataItem>  | no  | all | yes
| data2 | Second set of dataPoint for the second line | Array <lineDataItem> | no  | all | yes
| data3 | Third set of dataPoint for the third line | Array <lineDataItem>| no  | all | yes
| data4 | Fourth set of dataPoint for the fourth line | Array <lineDataItem> | no  | all | yes
| data5 | Fifth set of dataPoint for the third line| Array <lineDataItem> | no  | all | yes
| dataSet | Array of data sets (used instead of using `data2`, `data3`, `data4` etc)  | Array<DataSet>| no  | all | yes
| width | Width of the Bar chart  | number  | no  | all | yes
| height| Height of the Bar chart (excluding the bottom label)   | number  | no  | all | yes
| overflowTop | Extra space at the top of the chart to make room for dataPointText | number  | no  | all | yes
| overflowBottom | Extra space at the bottom of the chart to make room for dataPoints or dataPointText | number | no  | all | yes
| maxValue | Maximum value shown in the Y axis | number  | no  | all | yes
| mostNegativeValue | The most negative value shown in the Y axis (to be used only if the data set has negative values too)  | number  | no  | all | yes
| noOfSections | Number of sections in the Y axis | number  | no  | all | yes
| noOfSectionsBelowXAxis | Number of sections in the Y axis below X axis (in case the data set has negative values too)| number | no  | all | yes
| stepValue | Value of 1 step/section in the Y axis  | number  | no  | all | yes
| stepHeight | Height of 1 step/section in the Y axis| number | no  | all | yes
| negativeStepValue | Value of 1 step/section in the Y axis for negative values (in the 4th quadrant)| number | no  | all | yes
| negativeStepHeight | Height of 1 step/section in the Y axis for negative values (in the 4th quadrant) | number  | no  | all | yes
| spacing | Distance between 2 consecutive bars in the Bar chart | number  | no  | all | yes
| adjustToWidth | When set to true, it auto computes the spacing value to fit the Line chart in the available width | boolean  | no  | all | yes
| backgroundColor | Background color of the Bar chart | ColorValue | no  | all | yes
| sectionColors | Background color of the horizontal sections of the chart | ColorValue | no  | all | yes
| scrollref | ref object that can be used to control the horizontal ScrollView inside which the chart is rendered | any    | no  | all | yes
| scrollToIndex | scroll to a particular index on chart load  | number  | no  | all | yes
| disableScroll  | To disable horizontal scroll | boolean | no  | all | yes
| showScrollIndicator | To show horizontal scroll indicator | boolean  | no  | all | yes
| indicatorColor | (iOS only) The color of the scroll indicators - ('black', 'white' or 'default')  | String  | no  | all | yes
| isAnimated | To show animated Line or Area Chart. Animation occurs when the chart load for the first time | boolean  | no  | all | yes
| animateOnDataChange  | To show animation on change in data. A smooth transition takes place between the iold and new line | boolean  | no  | all | yes
| onDataChangeAnimationDuration | Duration (milliseconds) in which the transition animation takes place on a change in data | number   | no  | all | yes
| onPress | The callback function that handles the press event. `item` and `index` are received as props | Function          | no  | all | yes
| scrollToEnd  | When set to true, the chart automatically scrolls to the rightmost data point  | boolean | no  | all | yes
| scrollAnimation | When set to true, scroll animation is visible when the chart automatically scrolls to the rightmost data point | boolean | no  | all | yes
| scrollEventThrottle | (only for iOS) see https://reactnative.dev/docs/scrollview#scrolleventthrottle-ios | number  | no  | iOS | yes
| onScroll | callback function called when the chart is scrolled horizontally| Function | no  | all | yes
| onMomentumScrollEnd | callback function called when scroll is completed   | Function| no  | all | yes
| initialSpacing | distance of the first data point from the Y axis| number | no  | all | yes
| endSpacing | distance/padding left at the end of the line chart | number  | no  | all | yes

**Item description (lineDataItem)**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| value| Value of the item representing representing its position | number | no  | all | yes
| onPress | Function called on pressing the data point | function | no  | all | yes
| label | Label text appearing under the X axis | string   | no  | all | yes
| labelTextStyle | Style object for the label text appearing under the X axis | object | no  | all | yes
| labelComponent | custom label component appearing under the X axis | Function | no  | all | yes
| yAxisLabelText | Y axis label text | string  | no  | all | yes
| dataPointText  | Text appearing near the data points | string | no  | all | yes
| textShiftX | To shift the dataPointText text horizontally  | number | no  | all | yes
| textShiftY | To shift the dataPointText text vertically    | number | no  | all | yes
| textColor | Color of the dataPointText | ColorValue| no  | all | yes
| textFontSize  | Font size of the dataPointText   | number | no  | all | yes
| dataPointHeight | Height of the data point (when data point's shape is rectangular)  | number | no  | all | yes
| dataPointWidth | Width of the data point (when data point's shape is rectangular)  | number | no  | all | yes
| dataPointRadius | Radius of the data point (when data points' shape is circular) | number| no  | all | yes
| dataPointColor  | Color of the data point  | ColorValue  | no  | all | yes
| dataPointShape | Shape of the data point (rectangular or circular) defaults to circular  | string  | no  | all | yes
| hideDataPoint | To hide the data point   | boolean  | no  | all | yes
| showVerticalLine | When set to true, a vertical line will be displayed along that data point | boolean   | no  | all | yes
| verticalLineUptoDataPoint | When set to true, it sets the height of the vertical line upto the corresponding data point | boolean | no  | all | yes
| verticalLineColor | Color of the vertical Line displayed along the data point | ColorValue | no  | all | yes 
| verticalLineThickness | Thickness of the vertical Line displayed along the data point | number| no  | all | yes 
| dataPointLabelWidth | width of the label shown beside a data point  | number  | no  | all | yes
| dataPointLabelShiftX | horizontal shift of a label from its corresponding data point  | number | no  | all | yes 
| dataPointLabelShiftY | vertical shift of a label from its corresponding data point | number | no  | all | yes 
| dataPointLabelComponent | custom component rendered above a data point| Function | no  | all | yes
| focusedDataPointLabelComponent | custom component rendered above a data point only when focused/selected (when the user presses) | Function  | no  | all | yes 
| showStrip | To show a vertical strip along the data point (even if it's not focused/selected) | boolean  | no  | all | yes 
| stripHeight | Height of the vertical strip that becomes visible on pressing the corresponding area of the chart, or when showStrip is set to true  | number| no  | all | yes 
| stripWidth | Width of the vertical strip that becomes visible on pressing the corresponding area of the chart, or when showStrip is set to true  | number| no  | all | yes 
| stripColor | Color of the vertical strip that becomes visible on pressing the corresponding area of the chart, or when showStrip is set to true | ColorValue| no  | all | yes 
| stripOpacity | Opacity of the vertical strip that becomes visible on pressing the corresponding area of the chart, or when showStrip is set to true | number| no  | all | yes 
| pointerShiftX  | Shifts the pointer for that item horizontally by given quantity (used only when pointerConfig prop is passed) | number| no  | all | yes 
| pointerShiftY | Shifts the pointer for that item vertically by given quantity (used only when pointerConfig prop is passed)  | number | no  | all | yes 

**Pagination related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| onEndReached     | Callback function called when the chart is scrolled upto end | Function | no  | all | yes 
| onStartReached   | Callback function called when the chart is scrolled upto start | Function | no  | all | yes 

**Axes and rules related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| xAxisLength | X axis length   | number | no  | all | yes
| xAxisColor| X axis color | ColorValue  | no  | all | yes
| xAxisThickness | X axis thickness  | number | no  | all | yes
| xAxisType  | solid or dotted/dashed  | RuleType | no  | all | yes
| yAxisColor | Y axis color  | ColorValue | no  | all | yes
| yAxisThickness | Y axis thickness  | number  | no  | all | yes
| yAxisLabelWidth | Width of the Y axis Label container | number   | no  | all | ye
| yAxisTextStyle | Style object for the Y axis text style | object   | no  | all | yes
| yAxisTextNumberOfLines | Number of lines for y axis label text | number  | no  | all | yes
| yAxisLabelContainerStyle | Style object for the Y axis label container  | object | no  | all | yes
| trimYAxisAtTop | Removes the extra length of the Y axis from the top  | boolean | no  | all | yes
| yAxisExtraHeight | Extra length of Y axis at the top  | number | no  | all | yes 
| yAxisOffset | Starting value on Y Axis | number | no  | all | yes 
| horizontalRulesStyle | Style object for the horizontal rules container | object  | no  | all | yes
| showFractionalValues | Allow fractional values for the Y axis label | boolean  | no  | all | yes 
| roundToDigits | Rounds the y axis values to given number of digits after decimal point | number | no  | all | yes 
| yAxisLabelPrefix | The String prepended to the y axis label text (for example- '$')  | String| no  | all | yes 
| yAxisLabelSuffix   |The String appended to the y axis label text | String| no  | all | yes 
| hideYAxisText | To hide Y axis label text  | boolean | no  | all | yes
| formatYLabel | a callback function that takes the label generated by the library and modifies it.  | (label: string) => string | no  | all | yes 
| yAxisSide  | Tells which side of the chart, should the y axis be present, defaults to 'left'  | String | no  | all | yes 
| rulesLength | Length of the horizontal    | number | no  | all | yes
| rulesColor | Color of the horizontal rules | ColorValue  | no  | all | yes    |
| rulesThickness | Thickness of the horizontal | number | no  | all | yes 
| hideRules  | To hide the horizontal | boolean  | no  | all | yes
| rulesType | solid or dotted/dashed | RuleType | no  | all | yes
| dashWidth | width of each dash | number | no  | all | yes 
| dashGap  | gap between 2     | number | no  | all | yes
| rulesConfigArray | Array of rulesConfig objects, used to customise the properties (like color, type etc) of specific rules   | Array<RulesConfig> | no  | all | yes 
| showReferenceLine1   | show reference line       | boolean   | no  | all | yes
| referenceLine1Config | properties of reference line like thickness, color etc (described below the table) | referenceConfigType | no  | all | yes 
| referenceLine1Position  | position of reference     | number | no  | all | yes
| showReferenceLine2  | show second reference         | boolean  | no  | all | yes
| referenceLine2Config | properties of reference line like thickness, color etc (described below the table) | referenceConfigType| no  | all | yes 
| referenceLine2Position | position of second reference  | number | no  | all | yes
| showReferenceLine3  | show third reference  | boolean   | no  | all | yes 
| referenceLine3Config  | properties of reference line like thickness, color etc (described below the table)  | referenceConfigType | no  | all | yes 
| referenceLine3Position | position of third reference line  | number| no  | all | yes
| showVerticalLines | To show vertical lines | boolean  | no  | all | yes
| verticalLinesUptoDataPoint | To set the height of the vertical lines upto the corresponding data point| boolean | no  | all | yes 
| verticallinesThickness | Thickness of the vertical lines | number  | no  | all | yes
| verticalLinesHeight  | Height of the vertical lines  | number   | no  | all | yes 
| verticalLinesStrokeDashArray | Array of 2 numbers denoting the dashWidth and dashGap of the lines. Used to render dashed/dotted vertical line | Array<number>| no  | all   |yes
| verticalLinesShift  | vertical lines are aligned with data point. Shift them left or right using +ve or -ve value of verticalLinesShift| number| no  | all   |yes 
| verticalLinesZIndex | Z index of the vertical lines | number   | no  | all | yes
| noOfVerticalLines  | Number of vertical lines displayed  | number      | no  | all | yes 
| verticalLinesSpacing | Distance between consecutive vertical lines | number    | no  | all | yes
| showXAxisIndices | To show the pointers on the X axis| boolean | no  | all | yes
| xAxisIndicesHeight | Height of the pointers on the X axis | number  | no  | all | yes 
| xAxisIndicesWidth | Width of the pointers on the X axis  | number  | no  | all | yes
| xAxisIndicesColor | Color of the pointers on the X axis | ColorValue | no  | all | yes
| showYAxisIndices | To show the pointers on the Y axis | boolean | no  | all | yes
| yAxisIndicesHeight | Height of the pointers on the Y axis | number   | no  | all | yes
| yAxisIndicesWidth | Width of the pointers on the Y axis | number   | no  | all | yes
| yAxisIndicesColor | Color of the pointers on the X axis | ColorValue   | no  | all | yes
| yAxisIndicesColor | To hide axes, rules, labels altogether  | boolean  | no  | all | yes
| yAxisLabelTexts | Array of label texts to be displayed along y axis  | Array<string>| no  | all   |yes
| xAxisLabelTexts | Array of label texts to be displayed below x axis | Array<string>| no  | all   |yes
| xAxisLabelTextStyle | Style of label texts to be displayed below x axis | object | no  | all | yes
| xAxisTextNumberOfLines | Number of lines for x axis label text | number  | no  | all | yes
| xAxisLabelsHeight | Height of X axis labels container   | number   | no  | all | yes
| xAxisLabelsVerticalShift | prop to adjust the vertical position of X axis labels (move X axis labels up or down) | number | no  | all   |yes
| rotateLabel | To rotate the X axis labels (by 60deg) | boolean  | no  | all | yes
| hideOrigin | To hide the y Axis label at origin (i.e. 0)  | boolean  | no  | all | ye
| secondaryYAxis | displays and controls the properties of the secondary Y axis on the right side | secondaryYAxisType | no  | all   |yes
| secondaryData | the secondary data that will be rendered along the secondary Y axis  | Array of items | no  | all   |yes
| secondaryLineConfig | properties of the secondary data line (secondaryLineConfigType is described below) | secondaryLineConfigType| no  | all   |yes

**Line related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| curved | To show curved line joining the data points  | boolean| no  | all   |yes
| color | Color of the lines joining the data points   | ColorValue | no  | all | yes
| color1| Color of the lines joining the first set of data points  | ColorValue | no  | all | yes
| color2 | Color of the lines joining the second set of data points  | ColorValue| no  | all | yes
| color3 | Color of the lines joining the third set of data points  | ColorValue| no  | all | yes
| color4 | Color of the lines joining the fourth set of data points  | ColorValue| no  | all | yes
| color5 | Color of the lines joining the fifth set of data points  | ColorValue| no  | all | yes
| thickness | Thickness of the lines joining the data points  | number| no  | all | yes
| thickness1 | Thickness of the lines joining the first set of data points | number | no  | all | yes
| thickness2 | Thickness of the lines joining the second set of data points | number | no  | all | yes
| thickness3 | Thickness of the lines joining the third set of data points | number     | no  | all | yes
| thickness4 | Thickness of the lines joining the fourth set of data points | number| no  | all | yes
| thickness5 | Thickness of the lines joining the fifth set of data points  | number | no  | all | yes
| zIndex1 | zIndex of the lines joining the first set of data points | number | no  | all | yes
| zIndex2 | zIndex of the lines joining the second set of data points  | number | no  | all | yes
| zIndex3 | zIndex of the lines joining the third set of data points| number | no  | all | yes
| zIndex4  | zIndex of the lines joining the fourth set of data points | number | no  | all | yes
| zIndex5 | zIndex of the lines joining the fifth set of data points | number | no  | all | yes
| strokeDashArray | Array of 2 numbers denoting the dashWidth and dashGap of the lines. Used to render dashed/dotted line chart | Array<number>| no  | all | yes
| strokeDashArray1 | Array of 2 numbers denoting the dashWidth and dashGap of line1. Used to render dashed/dotted line chart| Array<number> | no  | all | yes
| strokeDashArray2| Array of 2 numbers denoting the dashWidth and dashGap of line2. Used to render dashed/dotted line chart | Array<number>| no  | all | yes
| strokeDashArray3 | Array of 2 numbers denoting the dashWidth and dashGap of line3. Used to render dashed/dotted line chart | Array<number>| no  | all | yes
| strokeDashArray4 | Array of 2 numbers denoting the dashWidth and dashGap of line4. Used to render dashed/dotted line chart | Array<number>| no  | all | yes
| strokeDashArray5 | Array of 2 numbers denoting the dashWidth and dashGap of line5. Used to render dashed/dotted line chart | Array<number> | no  | all | yes
| lineSegments | Array of objects used to customize segments (parts) of line | Array<LineSegment> | no  | all | yes
| lineSegments2 | Array of objects used to customize segments (parts) of line2 | Array<LineSegment>      | no  | all | yes
| lineSegments3 | Array of objects used to customize segments (parts) of line3 | Array<LineSegment> | no  | all | yes
| lineSegments4 | Array of objects used to customize segments (parts) of line4  | Array<LineSegment> | no  | all | yes
| lineSegments5 | Array of objects used to customize segments (parts) of line5  | Array<LineSegment> | no  | all | yes
| highlightedRange | renders the parts of lines lying in a given data range with a different style (color, thickness,type)| HighlightedRange | no  | all | yes
| startIndex | Start index for data line (used to display data lines having breaks)  | number   | no  | all | yes
| startIndex1 | Start index for data line 1 (used to display data lines having breaks) | number| no  | all | yes
| startIndex2 | Start index for data line 2 (used to display data lines having breaks) | number | no  | all | yes
| startIndex3 | Start index for data line 3 (used to display data lines having breaks) | number | no  | all | yes
| startIndex4 | Start index for data line 4 (used to display data lines having breaks) | number | no  | all | yes
| startIndex5 | Start index for data line 5 (used to display data lines having breaks) | number| no  | all | yes
| endIndex | End index for data line (used to display data lines having breaks) | number| no  | all | yes
| endIndex1 | End index for data line 1 (used to display data lines having breaks) | number | no  | all | yes
| endIndex2 | End index for data line 2 (used to display data lines having breaks) | number| no  | all | yes
| endIndex3 | End index for data line 3 (used to display data lines having breaks)  | number| no  | all | yes
| endIndex4 | End index for data line 4 (used to display data lines having breaks) | number | no  | all | yes
| endIndex5 | End index for data line 5 (used to display data lines having breaks)  | number| no  | all | yes
| lineGradient | this prop is used to render the line with a gradient blend of colors | boolean| no  | all | yes
| lineGradientComponent  | this prop defines the svg gradient that should be applied to the line (requires lineGradient to be truthy) | Function| no  | all | yes
| lineGradientId | id of the <LinearGradient> (needed along with lineGradientComponent prop) | string| no  | all | yes
| lineGradientDirection  | 'vertical'/'horizontal' | string  | no  | all | yes 
| lineGradientStartColor | Start gradient color for the line (requires lineGradient to be truthy) | string| no  | all | yes
| lineGradientEndColor | End gradient color for the line (requires lineGradient to be truthy)  | string | no  | all | yes

**The arrow**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| showArrows | To show an arrow at the end of each data line  | boolean | no  | all | yes
| arrowConfig  | Object describing the properties of the arrows like length, width, strokeWidth, strokeColor, fillColor | arrowType  | no  | all | yes
| showArrow1   | To show an arrow at the end of the first data line | boolean | no  | all | yes
| arrowConfig1  | Object describing the properties of the first arrow | arrowType| no  | all | yes
| showArrow2  | To show an arrow at the end of the second data line | boolean | no  | all | yes
| arrowConfig2 | Object describing the properties of the second arrow | arrowType | no  | all | yes
| showArrow3   | To show an arrow at the end of the third data line | boolean | no  | all | yes
| arrowConfig3 | Object describing the properties of the third arrow | arrowType | no  | all | yes
| showArrow4   | To show an arrow at the end of the fourth data line| boolean   | no  | all | yes
| arrowConfig4 | Object describing the properties of the fourth arrow| arrowType | no  | all | yes
| showArrow5  | To show an arrow at the end of the fifth data line | boolean  | no  | all | yes
| arrowConfig5| Object describing the properties of the fifth arrow | arrowType | no  | all | yes

**Data points related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| hideDataPoints  | To hide data points   | boolean | no  | all | yes
| dataPointsHeight  | Height of data points (when data points' shape is rectangular) | number | no  | all | yes
| dataPointsWidth | Width of data points (when data points' shape is rectangular)  | number| no  | all | yes
| dataPointsRadius | Radius of data points (when data points' shape is circular)  | number| no  | all | yes
| dataPointsColor  | Color of the data points  | ColorValue  | no  | all | yes
| dataPointsShape | Shape of the data points (_'rectangular'_ or _'circular'_)  | string| no  | all | yes
| hideDataPoints1 | To hide data points for the first set of data  | boolean | no  | all | yes
| dataPointsHeight1 | Height of data points for the first dataset (when data points' shape is rectangular)  | number | no  | all | yes
| dataPointsWidth1  | Width of data points for the first dataset (when data points' shape is rectangular) | number| no  | all | yes
| dataPointsRadius1  | Radius of data points for the first dataset (when data points' shape is circular) | number| no  | all | yes
| dataPointsColor1 | Color of data points for the first dataset | ColorValue | no  | all | yes
| dataPointsShape1 | Shape of data points for the first dataset   | string | no  | all | yes
| hideDataPoints2 | To hide data points for the second set of data   | boolean | no  | all | yes
| dataPointsHeight2 | Height of data points for the second dataset (when data points' shape is rectangular)  | number| no  | all | yes
| dataPointsWidth2  | Width of data points for the second dataset (when data points' shape is rectangular)  | number | no  | all | yes
| dataPointsRadius2  | Radius of data points for the second dataset (when data points' shape is circular) | number| no  | all | yes
| dataPointsColor2   | Color of data points for the second dataset   | ColorValue| no  | all | yes
| dataPointsShape2 | Shape of data points for the second dataset (_'rectangular'_ or _'circular'_) | string| no  | all | yes
| hideDataPoints3   | To hide data points for the third set of data | boolean | no  | all | yes
| dataPointsHeight3  | Height of data points for the third dataset (when data points' shape is rectangular)        | number | no  | all | yes
| dataPointsWidth3  | Width of data points for the third dataset (when data points' shape is rectangular)  | number | no  | all | yes
| dataPointsRadius3 | Radius of data points for the third dataset (when data points' shape is circular) | number | no  | all | yes
| dataPointsColor3   | Color of data points for the third dataset  | ColorValue| no  | all | yes
| dataPointsShape3 | Shape of data points for the third dataset (_'rectangular'_ or _'circular'_) | string| no  | all | yes
| hideDataPoints4 | To hide data points for the fourth set of data  | boolean | no  | all | yes
| dataPointsHeight4 | Height of data points for the fourth dataset (when data points' shape is rectangular) | number | no  | all | yes
| dataPointsWidth4  | Width of data points for the fourth dataset (when data points' shape is rectangular)  | number | no  | all | yes
| dataPointsRadius4 | Radius of data points for the fourth dataset (when data points' shape is circular)  | number| no  | all | yes
| dataPointsColor4 | Color of data points for the fourth dataset  | ColorValue| no  | all | yes
| dataPointsShape4  | Shape of data points for the fourth dataset (_'rectangular'_ or _'circular'_) | string| no  | all | yes
| hideDataPoints5  | To hide data points for the fifth set of data  | boolean | no  | all | yes
| dataPointsHeight5 | Height of data points for the fifth dataset (when data points' shape is rectangular) | number | no  | all | yes
| dataPointsWidth5 | Width of data points for the fifth dataset (when data points' shape is rectangular) | number| no  | all | yes
| dataPointsRadius5  | Radius of data points for the fifth dataset (when data points' shape is circular)   | number | no  | all | yes
| dataPointsColor5 | Color of data points for the fifth dataset | ColorValue| no  | all | yes
| dataPointsShape5  | Shape of data points for the fifth dataset (_'rectangular'_ or _'circular'_)        | string| no  | all | yes
| focusedDataPointIndex | Index of the focused data point, works only when focusEnabled prop is used     | number | no  | all | yes
| focusedDataPointShape    | Shape of the data points when focused due to press event   | String | no  | all | yes
| focusedDataPointWidth | Width of the data points when focused due to press event     | number | no  | all | yes
| focusedDataPointHeight | Height of the data points when focused due to press event    | number | no  | all | yes
| focusedDataPointColor  | Color of the data points when focused due to press event     | ColorValue | no  | all | yes
| focusedDataPointRadius | Radius of the data points when focused due to press event  | number| no  | all | yes
| focusedCustomDataPoint | Custom data point when focused due to press event| Function| no  | all | yes
| textColor  | Color of the dataPointText  | ColorValue | no  | all | yes
| textFontSize | Font size of the dataPointText  | number  | no  | all | yes
| textShiftX | To shift the dataPointText text horizontally   | number  | no  | all | yes
| textShiftY | To shift the dataPointText text vertically | number | no  | all | yes
| customDataPoint | A callback function to render a custom component as the data points  | Function  | no  | all | yes
| dataPointLabelWidth | width of the label shown beside a data point | number | no  | all | yes
| dataPointLabelShiftX | horizontal shift of a label from its corresponding data point  | number | no  | all | yes
| dataPointLabelShiftY | vertical shift of a label from its corresponding data point | number | no  | all | yes
| showValuesAsDataPointsText | When set to true, the data item value will be shown as a label text near data point | boolean  | no  | all | yes
| pointerColorsForDataSet | When using pointers with dataSet, you can set pointer colors on each data line using this array   | ColorValue[] | no  | all | yes


**pointerConfig**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| height | Height of the pointer |  number  | no  | all | yes
| width  | width of the pointer |  number  | no  | all | yes
| radius  | radius of the pointer   |  number  | no  | all | yes
| pointerColor  |  pointer color   |  ColorValue  | no  | all | yes
| pointer1Color  |  pointer color  |  ColorValue  | no  | all | yes
| pointer2Color  |  pointer color  |  ColorValue  | no  | all | yes
| pointer3Color  |  pointer color  |  ColorValue  | no  | all | yes
| pointer4Color  |  pointer color  |  ColorValue  | no  | all | yes
| pointer5Color  |  pointer color  |  ColorValue  | no  | all | yes
| pointerColorsForDataSet | When using pointers with dataSet, you can set pointer colors on each data line using the pointerColorsForDataSet which is an array of color values.  |  ColorValue[]  | no  | all | yes
| secondaryPointerColor | Secondary pointer color  |  ColorValue  | no  | all | yes
| pointerComponent | is a function that returns the component to be rendered as a pointer  |  Function  | no  | all | yes
| showPointerStrip | show pointer bar |  boolean  | no  | all | yes
| pointerStripWidth  | width of the pointer bar |  number  | no  | all | yes
| pointerStripHeight  | height of dthe pointer bar  |  number  | no  | all | yes
| pointerStripColor  | color of the pointer bar   |  ColorValue  | no  | all | yes
| pointerStripUptoDataPoint | Pointer stripped to data point  |  boolean  | no  | all | yes
| pointerLabelComponent | is a function that returns the component to be rendered as a Label. It takes 2 parameters - 1. an array of items 2 |  Function  | no  | all | yes
| stripOverPointer | strip to over pointer  |  boolean  | no  | all | yes
| autoAdjustPointerLabelPosition | Adjust the position of the pointer  |  boolean  | no  | all | yes
| shiftPointerLabelX | x-axis displacement pointer label  |  number  | no  | all | yes
| shiftPointerLabelY | y-axis displacement pointer label  |  number  | no  | all | yes
| pointerLabelWidth  | pointer label width |  number  | no  | all | yes
| pointerLabelHeight | pointer label height |  number  | no  | all | yes
| pointerVanishDelay | Pointer disappearance delay |  number  | no  | all | yes
| activatePointersOnLongPress |Long press to activate pointer  |  boolean  | no  | all | yes
| activatePointersDelay | activation pointer delay |  number  | no  | all | yes
| persistPointer | persistent pointer |  boolean  | no  | all | yes
| hidePointer1 | hidden pointer |  boolean  | no  | all | yes
| hidePointer2 | hidden pointer |  boolean  | no  | all | yes
| hidePointer3 | hidden pointer |  boolean  | no  | all | yes
| hidePointer4 | hidden pointer | boolean  | no  | all | yes
| hidePointer5 | hidden pointer |  boolean  | no  | all | yes
| hideSecondaryPointer | Hide auxiliary pointer |  boolean  | no  | all | yes
| strokeDashArray | Array of 2 numbers denoting the dashWidth and dashGap of the lines. Used to render dashed/dotted pointer |  number[]  | no  | all | yes


**onFocus and strip related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| focusEnabled  | If set true, allows users to press on the chart and focuses the nearest data point (focus event can be then handled using the `onFocus` prop) | boolean| no  | all | yes
| onFocus  | The callback function that handles the focus event. `item` and `index` are received as props | Function| no  | all | yes
| focusedDataPointIndex  | Index of the focused data point, used to set initially focused data point and to override the focus behaviour on onFocus    | number| no  | all | yes
| showDataPointOnFocus | If set true, it shows the data point corresponding to the focused area of the chart | boolean    | no  | all | yes
| showStripOnFocus | If set true, it shows a vertical strip corresponding to the focused area of the chart   | boolean | no  | all | yes
| showTextOnFocus  | If set true, it shows the data point text corresponding to the focused area of the chart  | boolean | no  | all | yes
| showDataPointLabelOnFocus | If set true, it shows the data point corresponding to the focused area of the chart | boolea| no  | all | yes
| stripHeight  | Height of the vertical strip that becomes visible on pressing the corresponding area of the chart | number | no  | all | yes
| stripWidth    | Width of the vertical strip that becomes visible on pressing the corresponding area of the chart            | number | no  | all | yes
| stripColor   | Color of the vertical strip that becomes visible on pressing the corresponding area of the chart             | ColorValue| no  | all | yes
| stripOpacity  | Opacity of the vertical strip that becomes visible on pressing the corresponding area of the chart             | number | no  | all | yes
| unFocusOnPressOut     | If set true, it unselects/unfocuses the focused/selected data point     | boolean| no  | all | yes
| delayBeforeUnFocus   | Delay (in milliseconds) between the release of the press and ghe unfocusing of the data point  | number | no  | all | yes
| focusedDataPointShape | Shape of the data points when focused due to press    | String | no  | all | yes
| focusedDataPointWidth  | Width of the data points when focused due to press    | number  | no  | all  | yes
| focusedDataPointHeight | Height of the data points when focused due to press    | number  | no  | all  | yes
| focusedDataPointColor | Color of the data points when focused due to press    | ColorValue | no  | all  | yes
| focusedDataPointRadius  | Radius of the data points when focused due to press   | number   | no  | all  | yes
| focusedCustomDataPoint | Custom data point when focused due to press event    | Function  | no  | all   | yes

**Props for Area Chart**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| areaChart | If set true, renders area chart instead of line chart  | boolean| no  | all | yes
| areaChart1 | If set true, renders area chart for 1st data set instead of line chart | boolean | no  | all | yes
| areaChart2 | If set true, renders area chart for 2nd data set instead of line chartt | boolean  | no  | all | yes
| areaChart3 | If set true, renders area chart for 3rd data set instead of line chartt | boolean | no  | all | yes
| areaChart4 | If set true, renders area chart for 4th data set instead of line chartt | boolean | no  | all | yes
| areaChart5 | If set true, renders area chart for 5th data set instead of line chartt | boolean | no  | all | yes
| startFillColor | Start gradient color for the area chart | ColorValue | no  | all | yes
| endFillColor | End gradient color for the area chart | ColorValue | no  | all | yes
| startOpacity | Start gradient opacity for the area chart | number | no  | all | yes
| endOpacity | End gradient opacity for the area chart  | number  | no  | all | yes
| startFillColor1 | Start gradient color for the first dataset of the area chart | ColorValue| no  | all | yes
| endFillColor1 | End gradient color for the first dataset of the area chart | ColorValue  | no  | all | yes
| startOpacity1 | Start gradient opacity for the first dataset of the area chart | number  | no  | all | yes
| endOpacity1  | End gradient opacity for the first dataset of the area chart   | number | no  | all | yes
| startFillColor2 | Start gradient color for the second dataset of the area chart | ColorValue | no  | all | yes
| endFillColor2 | End gradient color for the second dataset of the area chart  | ColorValue  | no  | all | yes
| startOpacity2 | Start gradient color for the second dataset of the area chart | number    | no  | all | yes
| endOpacity2 | End gradient opacity for the second dataset of the area chart  | number   | no  | all | yes
| startFillColor3 | Start gradient color for the third dataset of the area chart | ColorValue| no  | all | yes
| endFillColor3 | End gradient color for the third dataset of the area chart  | ColorValue | no  | all | yes
| startOpacity3 | Start gradient color for the third dataset of the area chart | number  | no  | all | yes
| endOpacity3 | End gradient opacity for the third dataset of the area chart   | number  | no  | all | yes
| startFillColor4 | Start gradient color for the fourth dataset of the area chart | ColorValue | no  | all | yes
| endFillColor4 | End gradient color for the fourth dataset of the area chart   | ColorValue | no  | all | yes
| startOpacity4  | Start gradient color for the fourth dataset of the area chart       | number | no  | all | yes
| endOpacity4  | End gradient opacity for the fourth dataset of the area chart         | number | no  | all | yes
| startFillColor5 | Start gradient color for the fifth dataset of the area chart      | ColorValue         | no  | all | yes
| endFillColor5 | End gradient color for the fifth dataset of the area chart        | ColorValue          | no  | all | yes
| startOpacity5 | Start gradient color for the fifth dataset of the area chart        | number   | no  | all | yes
| endOpacity5 | End gradient opacity for the fifth dataset of the area chart          | number | no  | all | yes
| gradientDirection | Direction of the gradient (_'horizontal'_ or _'vertical'_)    | string  | no  | all | yes
| areaGradientComponent | this prop defines the svg gradient that should be applied to the area (requires areaChart to be truthy) | Function| no  | all | yes
| areaGradientId  | id of the <LinearGradient> (needed along with areaGradientComponent prop)      | string | no  | all | yes

### PieChart and DonutChart

**Basic props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An item object represents a section in the Pie chart. Descibed in the next table  | pieDataItem[]  | no  | all | yes
| radius  | Radius of the Pie | number   | no  | all | yes
| initialAngle | Starting angle in radians (illustrated below this table)| number | no  | all | yes
| isThreeD  | If set to true, it rotates and translates the chart to give it a 3D effect  | boolean  | no  | all | yes
| showGradient | Prop to enable radial gradient for the Pie sections  | boolean  | no  | all | yes
| gradientCenterColor | Gradient color at the center of the Pie chart | ColorValue            | no  | all | yes
| onPress   | Callback function called on press of Pie sections (takes item and index as parameter) | Function                | no  | all | yes
| focusOnPress  | When set to true, the pressed section of the Pie chart will have a bigger radius, hence appear focused   | boolean  | no  | all | yes
| toggleFocusOnPress | When set to true, if the user presses an already focused pie section, it will be unfocused  | boolean  | no  | all | yes
| extraRadiusForFocused  | Extra radius for the focused Pie section  | number | no  | all | yes
| inwardExtraLengthForFocused | Extra length of focused Pie section towards the center (only for donut charts) | number  | no  | all | yes
| sectionAutoFocus | In case you don't want focusOnPress but want a particular section to autofocus, this prop will be needed | boolean | no  | all | yes
| onLabelPress | Callback function called on press of a Label (takes item and index as parameter) | Function               | no  | all | yes
| tiltAngle | The angle by which the chart should be tilted  | Angle in deg           | no  | all | yes
| shadow  | Shadow to the Pie chart, when set to true, it enhances the 3D effect | boolean  | no  | all | yes
| shadowColor  | Color of the shadow   | ColorValue  | no  | all | yes
| shadowWidth  | Width of the shadow   | number  | no  | all | yes
| strokeWidth  | Stroke (line) width for the Pie chart and its section | number | no  | all | yes
| strokeColor | Stroke (line) color | ColorValue | no  | all | yes
| backgroundColor | Background color of the container that contains the Pie chart  | ColorValue | no  | all | yes
| showText  | When set to true, displays text on the Pie sections | boolean | no  | all | yes
| textColor  | Color of the label texts | ColorValue  | no  | all | yes
| textSize  | Size of the label texts (max allowed: radius / 5) | number | no  | all | yes
| fontStyle | Style of the text - 'normal', 'italic' or 'oblique'| string| no  | all | yes
| fontWeight | Weight of the text - 'bold', 'bolder', 'lighter', '100', '200' etc | string | no  | all | yes
| font  | Font family of the text - 'Arial', 'Cursive', 'Comic Sans MS' etc | string | no  | all | yes
| showTextBackground | When set to true, displays background for text on the Pie sections | boolean | no  | all | yes
| textBackgroundColor | Background color for the label texts  | ColorValue | no  | all | yes
| textBackgroundRadius | Radius for the background of the text labels   | number | no  | all | yes
| showValuesAsLabels  | When set to true, the values of the Pie sections are displayed as labels   | boolean  | no  | all | yes
| centerLabelComponent | Component to be rendered at the center of the Pie chart  | Function | no  | all | yes
| semiCircle  | When set to true, renders the Pie Chart in a semi-circle. donut semiCircle charts look like a speed-meter  | boolean  | no  | all | yes
| labelsPosition  | Tells where inside the Pie sections should the labels be shown- 'onBorder', 'outward', 'inward' or 'mid' | string | no  | all | yes
| pieInnerComponent | Svg element to be rendered inside each Pie like a label (position controlled by 'labelsPosition' )  | () => svg element       | no  | all | yes
| paddingHorizontal | horizontal padding in the chart svg component (useful to accomodate _"onBorder"_ labels) | number | no  | all | yes
| paddingVertical  | vertical padding in the chart svg component (useful to accomodate _"onBorder"_ labels) | number | no  | all | yes
| isAnimated | To show animates PieProChart. Animation occurs onLoad and on value change | boolean  | no  | all | yes
| animationDuration  | Duration of the animations, only fro PieProChart  | number| no  | all | yes
| curvedStartEdges  | Bend start edge, only fro PieProChart  | boolean | no  | all | yes
| curvedEndEdges  | Bend end edge, only fro PieProChart  | boolean | no  | all | yes
| edgesRadius  | Bend radius, only fro PieProChart | number | no  | all | yes

**Item description (pieDataItem)**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| value   | Value of the item, representing a section of the Pie chart | number  | no  | all | yes
| shiftX  | Translates (shifts) the particular section horizontally by given value  | number | no  | all | yes
| shiftY | Translates (shifts) the particular section vertically by given value | number | no  | all | yes
| shiftTextX | Translates (shifts) the position of label text horizontally          | number  | no  | all | yes
| shiftTextY  | Translates (shifts) the position of label text vertically | number | no  | all | yes
| shiftTextBackgroundX | Shifts the background of label text horizontally (default value is shiftTextX) | number  | no  | all | yes
| shiftTextBackgroundY | Shifts the background of label text vertically (default value is shiftTextY) | number | no  | all | yes
| color | Color (background color) of the section | ColorValue  | no  | all | yes
| text  | Label text for the sections | string  | no  | all | yes
| textColor  | Color of the text (label) inside the section | ColorValue   | no  | all | yes
| textSize  | Size of the text (label) inside the section | number   | no  | all | yes
| fontStyle | Style of the text - 'normal', 'italic' or 'oblique' | string | no  | all | yes
| fontWeight  | Weight of the text - 'bold', 'bolder', 'lighter', '100', '200' etc | string   | no  | all | yes
| font | Font family of the text - 'Arial', 'Cursive', 'Comic Sans MS' etc | string | no  | all | yes
| textBackgroundColor | Background color for the label text | ColorValue  | no  | all | yes
| textBackgroundRadius  | Radius for the background of the text label| number   | no  | all | yes
| labelPosition | Tells where inside the Pie sections should the labels be shown- 'onBorder', 'outward', 'inward' or 'mid'  | string  | no  | all | yes
| onPress  | Callback function called on press of Pie sections (takes item and index as parameter) | Function  | no  | all | yes
| onLabelPress | Callback function called on press of a Label (takes item and index as parameter)         | Function | no  | all | yes
| strokeWidth | Stroke (line) width for the Pie chart and its section       | number  | no  | all | yes
| strokeColor   | Stroke (line) color  | ColorValue | no  | all | yes
| focused  | When set to true, the section for that item is focused, sectionAutoFocus must be set true in order to use this property | boolean  | no  | all | yes
| pieInnerComponent  | Svg element to be rendered inside the Pie like a label (position controlled by 'labelsPosition' )    | () => svg element  | no  | all | yes

**Donut chart related props**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| donut | When set to true, renders a Donut chart (makes an inner ring) | boolean | no  | all | yes
| innerRadius   | Radius of the inner ring | number | no  | all | yes
| innerCircleColor | Color of the inner ring | ColorValue| no  | all | yes
| innerCircleBorderWidth | Stroke (border) width of the inner ring | number  | no  | all | yes
| innerCircleBorderColor | Stroke (border) color of the inner ring | ColorValue  | no  | all | yes
| shiftInnerCenterX   | Shifts the inner ring horizontally to enhance the 3D effect | number   | no  | all | yes 
| shiftInnerCenterY  | Shifts the inner ring vertically to enhance the 3D effect  | number  | no  | all | yes

### Population Pyramid

**base props**

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| height  | height of chart body (excluding x-axis labels)  | number | no  | all | yes
| width | width of chart body   | number   | no  | all | yes
| data | array of objects, each object is described by **popnPyramidDataItem**  | Array<popnPyramidDataItem>  | no  | all | yes
| hideRules  | when set to true, hides horizontal rules (which are displayed in the background of the charts)  | boolean     | no  | all | yes
| rulesThickness | thickness of the horizontal rules | number  | no  | all | yes    
| rulesColor | color of the horizontal rules | ColorValue   | no  | all | yes
| rulesType| type of the horizontal rules - SOLID or DASHED/DOTTED | RuleTypes   | no  | all | yes
| dashWidth | width of each dash in the horizontal rules | number  | no  | all | yes
| dashGap | gap between each dash in the horizontal rules | number | no | all | yes
| stepHeight| height of each step/horizontal section in the chart body | number   | no  | all | yes
| verticalMarginBetweenBars| self explanatory | number    | no  | all | yes
| hideYAxisText | hide Y axis labels, when not set to true, a gap will be left to the left of the chart | boolean   | no  | all | yes
| yAxisLabelWidth | self explanatory  | number     | no  | all | yes
| yAxisColor  | self explanatory  | ColorValue  | no  | all | yes
| yAxisThickness | self explanatory  | number    | no  | all | yes
| yAxisStrokeDashArray | used to render a dashed or dotted Y axis line ([dashWidth,dashGap]) | Array<number>    | no  | all | yes
| xAxisColor | self explanatory  | ColorValue   | no  | all | yes
| xAxisThickness | self explanatory  | number   | no  | all | yes
| xAxisType | type of X-axis- SOLID, DASHED or DOTTED  | RuleTypes  | no  | all | yes
| xAxisNoOfSections | number of sections in X-axis (in both left and right parts)  | number     | no  | all | yes
| showXAxisIndices | when set to true, shows small lines (indices) at each section of x-axis | boolean    | no  | all | yes
| xAxisIndicesWidth | width of x axis indices | number   | no  | all | yes
| xAxisIndicesHeight | height of x axis indices | number   | no  | all | yes
| xAxisIndicesColor | color of of x axis indices | ColorValue  | no  | all | yes
| xAxisIndicesShiftY | used to shift x axis indices downwards or upwards | number   | no  | all | yes
| showXAxisLabelTexts | self explanatory | boolean      | no  | all | yes
| xAxisLabelFontSize | self explanatory | number    | no  | all | yes
| xAxisLabelColor | self explanatory  | ColorValue      | no  | all | yes
| xAxisLabelFontStyle | self explanatory | FontStyle  | no  | all | yes
| xAxisLabelFontWeight | self explanatory  | FontWeight  | no  | all | yes
| xAxisLabelFontFamily | self explanatory  | string   | no  | all | yes
| xAxisLabelShiftX  | horizontally shifts the x axis labels by given value | number | no  | all | yes
| xAxisLabelShiftY | vertically shifts the x axis labels by given value | number  | no  | all | yes
| xAxisRoundToDigits | number of decimal places upto which x axis labels will be displayed   | number | no  | all | yes
| xAxisLabelPrefix  | The String prepended to the x axis label text (for example- '$') | string | no  | all | yes
| xAxisLabelSuffix  | The String appended to the x axis label text | string  | no  | all | yes
| formatXAxisLabels | a callback function that takes the label generated by the library and modifies it | (label: string) => string   | no  | all | yes
| showVerticalLines | show vertical lines (similar to horiz rules) in background of the chart | boolean  | no  | all | yes
| verticalLinesColor | Color of the vertical lines  | ColorValue  | no  | all | yes
| verticalLinesThickness | Thickness of the vertical lines | number  | no  | all | yes
| verticalLinesStrokeDashArray | used to render dashed or dotted vertical lines ([dashWidth,dashGap]) | Array<number> | no  | all | yes
| noOfSections | Number of sections (and horiz rules) in the Y axis | number | no  | all | yes
| barsMapToYAxisSections | this prop tells whether the number of sections in the Y axis is equal to the length of data array      | boolean  | no  | all | yes
| showYAxisIndices | when set to true, shows small lines (indices) at each section of y-axis  | boolean   | no  | all | yes
| yAxisIndicesWidth | width of y axis indices | number  | no  | all | yes
| yAxisIndicesHeight | height of y axis indices          | number   | no  | all | yes
| yAxisIndicesColor | color of of x axis indices | ColorValue   | no  | all | yes
| yAxisLabelColor | color of of x axis label text | ColorValue   | no  | all | yes
| yAxisLabelFontSize | font size of of of x axis label text =| number   | no  | all | yes
| yAxisLabelTextMarginRight | space left between the y axis labels and the y axis line | number | no  | all | yes
| yAxisLabelTexts | An array of string labels to be rendered as Y axis labels (top to bottom) | Array<string>    | no  | all | yes
| yAxisLabelFontStyle | self explanatory | FontStyle    | no  | all | yes
| yAxisLabelFontWeight | self explanatory | FontWeight   | no  | all | yes
| yAxisLabelFontFamily   | self explanatory  | string    | no  | all | yes
| showValuesAsBarLabels | when set to true, displays the left and right values as labels beside the respective bars | boolean | no  | all | yes
| showMidAxis  | when set to true, displays an axis in the mid - between the left and right halves of the pyramid | boolean   | no  | all | yes
| midAxisThickness  | thickness of the mid axis lines | number    | no  | all | yes
| midAxisLabelWidth | width of the mid axis | number    | no  | all | yes
| midAxisColor  | color of the mid axis lines | ColorValue    | no  | all | yes
| midAxisLeftColor | color of the left mid axis line | ColorValue    | no  | all | yes
| midAxisRightColor  | color of the right mid axis line | ColorValue    | no  | all | yes
| midAxisStrokeDashArray | used to render dashed or dotted mid axis lines ([dashWidth,dashGap])  | Array<number>   | no  | all | yes
| midAxisLabelFontSize   | self explanatory | number    | no  | all | yes
| midAxisLabelColor | self explanatory  | ColorValue     | no  | all | yes
| midAxisLabelFontStyle  | self explanatory | FontStyle    | no  | all | yes
| midAxisLabelFontWeight  | self explanatory | FontWeight    | no  | all | yes
| midAxisLabelFontFamily | self explanatory | string    | no  | all | yes
| barLabelWidth  | width of the labels displayed behind the bars (both left and right bars) | number    | no  | all | yes
| barLabelFontSize  | font size of the labels displayed behind the bars (both left and right bars) | number    | no  | all | yes
| barLabelColor | color of the of the labels displayed behind the bars (both left and right bars) | ColorValue    | no  | all | yes
| barLabelFontStyle  | font style of the labels displayed behind the bars (both left and right bars) | FontStyle    | no  | all | yes
| barLabelFontWeight  | font weight of the labels displayed behind the bars (both left and right bars) | FontWeight   | no  | all | yes
| barLabelFontFamily | font family of the labels displayed behind the bars (both left and right bars) | string    | no  | all | yes
| leftBarLabelWidth  | width of the labels displayed behind the left bars  | number    | no  | all | yes
| leftBarLabelFontSize   | font size of the labels displayed behind the left bars | number    | no  | all | yes
| leftBarLabelColor | color of the labels displayed behind the left bars | ColorValue    | no  | all | yes
| leftBarLabelFontStyle | font style of the labels displayed behind the left bars | FontStyle     | no  | all | yes
| leftBarLabelFontWeight  | font weight of the labels displayed behind the left bars  | FontWeight    | no  | all | yes
| leftBarLabelFontFamily | font family of the labels displayed behind the left bars | string    | no  | all | yes
| leftBarLabelShift | value by which the left bar labels should be shifted horizontally (kind of margin b/w label and bar) | number | no  | all | yes
| leftBarLabelPrefix | The String prepended to the left bar label text (for example- '$')  | string     | no  | all | yes
| leftBarLabelSuffix | The String appended to the left bar label text | string     | no  | all | yes
| rightBarLabelWidth | width of the labels displayed behind the right bars | number    | no  | all | yes
| rightBarLabelFontSize | font size of the labels displayed behind the right bars | number    | no  | all | yes
| rightBarLabelColor | color of the labels displayed behind the right bars  | ColorValue    | no  | all | yes
| rightBarLabelFontStyle  | font style of the labels displayed behind the right bars | FontStyle    | no  | all | yes
| rightBarLabelFontWeight | font weight of the labels displayed behind the right bars | FontWeight    | no  | all | yes
| rightBarLabelFontFamily | font family of the labels displayed behind the right bars | string    | no  | all | yes
| rightBarLabelShift  | value by which the right bar labels should be shifted horizontally (kind of margin b/w label and bar) | number   | no  | all | yes
| rightBarLabelPrefix  | The String prepended to the right bar label text (for example- '$') | string    | no  | all | yes
| rightBarLabelSuffix | The String appended to the right bar label text | string    | no  | all | yes
| formatBarLabels  | a callback function that takes the label generated by the library and modifies it | (label: string) => string    | no  | all | yes
| leftBarColor | color of the bars displayed in the left half of the pyramid  | ColorValue    | no  | all | yes
| rightBarColor | color of the bars displayed in the right half of the pyramid  | ColorValue    | no  | all | yes
| leftBarBorderColor | border color of the bars displayed in the left half of the pyramid | ColorValue    | no  | all | yes
| rightBarBorderColor  | border color of the bars displayed in the right half of the pyramid | ColorValue   | no  | all | yes
| barBorderWidth | boder width of the bars (both left and right bars) | number     | no  | all | yes
| leftBarBorderWidth | boder width of the bars displayed in the left half of the pyramid  | number    | no  | all | yes
| rightBarBorderWidth | boder width of the bars displayed in the right half of the pyramid  | number   | no  | all | yes
| barBorderRadius  | boder radius of the bars | number    | no  | all | yes
| leftBarBorderRadius | boder width of the bars displayed in the left half of the pyramid | number     | no  | all | yes
| rightBarBorderRadius | boder width of the bars displayed in the right half of the pyramid| number    | no  | all | yes
| allCornersRounded | when set to true, border radius will apply to all the four corners of the bars, else applied only on outer edges | boolean   | no  | all | yes
| showSurplus  | shows surplus values on the edges in highlighted colors (extra width of the bigger bar is highlighted )  | boolean    | no  | all | yes
| showSurplusLeft  | shows surplus values on the left edges in highlighted colors (extra width of the bigger bar is highlighted )  | boolean    | no  | all | yes
| showSurplusRight | shows surplus values on the right edges in highlighted colors (extra width of the bigger bar is highlighted ) | boolean    | no  | all | yes
| leftSurplusColor | highlight color of the left surplus  | ColorValue | no  | all | yes
| leftSurplusBorderColor | border color of the left surplus | ColorValue   | no  | all | yes
| rightSurplusColor  | highlight color of the right surplus | ColorValue    | no  | all | yes
| rightSurplusBorderColor | border color of the right surplus | ColorValue    | no  | all | yes
| leftSurplusBorderWidth | border width of the left surplus | number    | no  | all | yes
| rightSurplusBorderWidth | border width of the right surplus | number    | no  | all | yes

## 遗留问题

- [ ] PieChart设置圆环设置为3D，中间圆环显示问题 [issue#7](https://github.com/react-native-oh-library/react-native-gifted-charts/issues/7)
- [ ] BarChart设置barBackgroundPattern显示问题 [issue#6](https://github.com/react-native-oh-library/react-native-gifted-charts/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Abhinandan-Kushwaha/react-native-gifted-charts/blob/master/LICENSE) ，请自由地享受和参与开源。
