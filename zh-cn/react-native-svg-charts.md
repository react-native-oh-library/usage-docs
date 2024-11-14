> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-svg-charts</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/JesperLekland/react-native-svg-charts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/JesperLekland/react-native-svg-charts/blob/dev/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-svg-charts)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[https://github.com/react-native-oh-library/react-native-svg-charts Releases](https://github.com/react-native-oh-library/react-native-svg-charts/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-naitve-svg-charts
```

#### **yarn**

```bash
yarn add  @react-native-oh-tpl/react-naitve-svg-charts
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

areaChart：
```jsx
import React from 'react'
import { Path } from 'react-native-svg'
import { AreaChart, Grid } from 'react-native-svg-charts'
import * as shape from 'd3-shape'

class AreaChartExample extends React.PureComponent {

    render() {

        const data = [50, 10, 40, 95, -4, -24, 85, 91, 35, 53, -53, 24, 50, -20, -80]

        const Line = ({ line }) => (
            <Path
                key={'line'}
                d={line}
                stroke={'rgb(134, 65, 244)'}
                fillOpacity={0}
            />
        )

        return (
            <AreaChart
                style={{ height: 200 }}
                data={data}
                contentInset={{ top: 30, bottom: 30 }}
                curve={shape.curveNatural}
                svg={{ fill: 'rgba(134, 65, 244, 0.2)' }}
                animate={true}
                animationDuration={2000}
            >
                <Grid />
                <Line />
            </AreaChart>
        )
    }
}

export default AreaChartExample
```
barChart:
```jsx
import React from 'react'
import { BarChart, Grid } from 'react-native-svg-charts'

class GroupedBarChartExample extends React.PureComponent {

    render() {

        const data1 = [ 14, -1, 100, -95, -94, -24, -8, 85, -91, 35, -53, 53, -78, 66, 96, 33, -26, -32, 73, 8 ]
            .map((value) => ({ value }))
        const data2 = [ 24, 28, 93, 77, -42, -62, 52, -87, 21, 53, -78, -62, -72, -6, 89, -70, -94, 10, 86, 84 ]
            .map((value) => ({ value }))

        const barData = [
            {
                data: data1,
                svg: {
                    fill: 'rgb(134, 65, 244)',
                },
            },
            {
                data: data2,
            },
        ]

        return (
            <BarChart
                style={ { height: 200 } }
                data={ barData }
                yAccessor={({ item }) => item.value}
                svg={{
                    fill: 'green',
                }}
                contentInset={ { top: 30, bottom: 30 } }
                { ...this.props }
            >
                <Grid/>
            </BarChart>
        )
    }

}

export default GroupedBarChartExample
```

StackedBarChart：
```jsx
import React from 'react'
import { Grid, StackedBarChart } from 'react-native-svg-charts'

const colors = ['#33691E', '#689F38', '#9CCC65', '#DCEDC8']
const data = [
    {
        broccoli: {
            value: 3840,
            svg: {
                onPress: () => console.log('onPress => 0:broccoli:3840'),
            },
        },
        celery: {
            value: 1920,
            svg: {
                onPress: () => console.log('onPress => 0:celery:1920'),
            },
        },
        onions: {
            value: 960,
            svg: {
                onPress: () => console.log('onPress => 0:onions:960'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 0:tomato:400'),
            },
        },
    },
    {
        broccoli: {
            value: 1600,
            svg: {
                onPress: () => console.log('onPress => 1:broccoli:1600'),
            },
        },
        celery: {
            value: 1440,
            svg: {
                onPress: () => console.log('onPress => 1:celery:1440'),
            },
        },
        onions: {
            value: 960,
            svg: {
                onPress: () => console.log('onPress => 1:onions:960'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 1:tomato:400'),
            },
        },
    },
    {
        broccoli: {
            value: 640,
            svg: {
                onPress: () => console.log('onPress => 2:broccoli:640'),
            },
        },
        celery: {
            value: 960,
            svg: {
                onPress: () => console.log('onPress => 2:celery:960'),
            },
        },
        onions: {
            value: 3640,
            svg: {
                onPress: () => console.log('onPress => 2:onions:3640'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 2:tomato:400'),
            },
        },
    },
    {
        broccoli: {
            value: 3320,
            svg: {
                onPress: () => console.log('onPress => 3:broccoli:3320'),
            },
        },
        celery: {
            value: 480,
            svg: {
                onPress: () => console.log('onPress => 3:celery:480'),
            },
        },
        onions: {
            value: 640,
            svg: {
                onPress: () => console.log('onPress => 3:onions:640'),
            },
        },
        tomato: {
            value: 400,
            svg: {
                onPress: () => console.log('onPress => 3:tomato:400'),
            },
        },
    },
]

const keys = ['broccoli', 'celery', 'onions', 'tomato']

class StackedBarChartWithOnPressExample extends React.PureComponent {
    render() {
        return (
            <StackedBarChart
                style={{ height: 300 }}
                colors={colors}
                contentInset={{ top: 30, bottom: 30 }}
                data={data}
                keys={keys}
                valueAccessor={({ item, key }) => item[key].value}
            >
                <Grid />
            </StackedBarChart>
        )
    }
}

export default StackedBarChartWithOnPressExample
```

lineChart：
```jsx
import React from 'react'
import { LineChart, Path, Grid } from 'react-native-svg-charts'

class LineChartExample extends React.PureComponent {

    render() {

        const data = [50, 10, 40, 95, -4, -24, 85, 91, 35, 53, -53, 24, 50, -20, -80]

        const Shadow = ({ line }) => (
            <Path
                key={'shadow'}
                y={2}
                d={line}
                fill={'none'}
                fillOpacity={0}
                strokeWidth={4}
                stroke={'rgba(134, 65, 244, 0.2)'}
            />
        )

        return (
            <LineChart
                style={{ height: 200, position: 'relative', zIndex: 0 }}
                data={data}
                svg={{ stroke: 'rgb(134, 65, 244)', fillOpacity: 0 }}
                contentInset={{ top: 20, bottom: 20 }}
            >
                <Grid />
                <Shadow />
            </LineChart>
        )
    }

}

export default LineChartExample
```

StackedAreaChart：
```jsx
import React from 'react'
import { StackedAreaChart, YAxis, Grid } from 'react-native-svg-charts'
import * as shape from 'd3-shape'
import { View } from 'react-native'

class AreaStackWithAxisExample extends React.PureComponent {

    render() {

        const data = [
            {
                month: new Date(2015, 0, 1),
                apples: 3840,
                bananas: 1920,
                cherries: 960,
                dates: 400,
            },
            {
                month: new Date(2015, 1, 1),
                apples: 1600,
                bananas: 1440,
                cherries: 960,
                dates: 400,
            },
            {
                month: new Date(2015, 2, 1),
                apples: 640,
                bananas: 960,
                cherries: 3640,
                dates: 400,
            },
            {
                month: new Date(2015, 3, 1),
                apples: 3320,
                bananas: 480,
                cherries: 640,
                dates: 400,
            },
        ]

        const colors = ['rgba(138, 0, 230, 0.8)', 'rgba(173, 51, 255, 0.8)', 'rgba(194, 102, 255, 0.8)', 'rgba(214, 153, 255, 0.8)']
        const keys = ['apples', 'bananas', 'cherries', 'dates']

        return (
            <View style={{ flexDirection: 'row', height: 200 }}>
                <StackedAreaChart
                    style={{ flex: 1 }}
                    contentInset={{ top: 10, bottom: 10 }}
                    data={data}
                    keys={keys}
                    colors={colors}
                    curve={shape.curveNatural}
                >
                    <Grid />
                </StackedAreaChart>
                <YAxis
                    style={{ position: 'absolute', top: -10, bottom: 10, width: 40 }}
                    data={StackedAreaChart.extractDataPoints(data, keys)}
                    contentInset={{ top: 10, bottom: 10 }}
                    numberOfTicks={8}
                    svg={{
                        fontSize: 8,
                        fill: 'white',
                        stroke: 'black',
                        strokeWidth: 0.1,
                        alignmentBaseline: 'baseline',
                        baselineShift: '3'
                    }}
                />
            </View>
        )
    }
}

export default AreaStackWithAxisExample
```

ProgressCircle：
```jsx
import React from 'react'
import { ProgressCircle } from 'react-native-svg-charts'

class ProgressCircleExample extends React.PureComponent {

    render() {

        return (
            <ProgressCircle
                style={ { height: 200 } }
                progress={ 0.7 }
                progressColor={'rgb(134, 65, 244)'}
                startAngle={ -Math.PI * 0.8 }
                endAngle={ Math.PI * 0.8 }
            />
        )
    }

}

export default ProgressCircleExample
```

PieChart：
```jsx
import React from 'react'
import { PieChart } from 'react-native-svg-charts'
import { Circle, G, Line } from 'react-native-svg'

class PieChartWithLabelExample extends React.PureComponent {

    render() {

        const data = [ 50, 10, 40, 95, -4, -24, 85, 91 ]

        const randomColor = () => ('#' + (Math.random() * 0xFFFFFF << 0).toString(16) + '000000').slice(0, 7)

        const pieData = data
            .filter(value => value > 0)
            .map((value, index) => ({
                value,
                svg: { fill: randomColor() },
                key: `pie-${index}`,
            }))

        const Labels = ({ slices }) => {
            return slices.map((slice, index) => {
                const { labelCentroid, pieCentroid, data } = slice;
                return (
                    <G key={ index }>
                        <Line
                            x1={ labelCentroid[ 0 ] }
                            y1={ labelCentroid[ 1 ] }
                            x2={ pieCentroid[ 0 ] }
                            y2={ pieCentroid[ 1 ] }
                            stroke={ data.svg.fill }
                        />
                        <Circle
                            cx={ labelCentroid[ 0 ] }
                            cy={ labelCentroid[ 1 ] }
                            r={ 15 }
                            fill={ data.svg.fill }
                        />
                    </G>
                )
            })
        }

        return (
            <PieChart
                style={ { height: 200 } }
                data={ pieData }
                innerRadius={ 20 }
                outerRadius={ 55 }
                labelRadius={ 80 }
            >
                <Labels/>
            </PieChart>
        )
    }

}

export default PieChartWithLabelExample
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-svg-capi.md#link)进行引入

## 约束与限制

### 兼容性

在下述版本验证通过:

1. react-native-harmony: 0.72.26-CAPI; SDK：HarmonyOS NEXT Developer Cannary3 SP2; IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.22(Canary3);

## 属性

详情见[react-native-svg-charts](https://github.com/JesperLekland/react-native-svg-charts)

### 共有属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An array of arbitrary data - use prop xAccessor/yAccessorto tell the chart about the data structure         | array  | YES | ALL      | YES |
yAccessor | A function that takes each entry of data (named "item") as well as the index and returns the y-value of that entry |  function | YES | ALL | YES |
xAccessor | Same as yAccessor but returns the x-value of that entry | function | YES | ALL | YES |
yScale | A function that determines the scale of said axis (only tested with scaleLinear, scaleTime & scaleBand ) | d3Scale.scaleLinear | YES | ALL | YES |
xScale | Same as yScale but for the x axis | d3Scale.scaleLinear | YES | ALL | YES |
svg | an object containing all the props that should be passed down to the underlying react-native-svg component. See available props | object | YES | ALL | YES |
animate | PropTypes.bool | boolean |   YES | ALL | YES |
animationDuration | PropTypes.number | number |   YES | ALL | YES |
style | Supports all ViewStyleProps | ViewStyleProps |   YES | ALL | YES |
curve | A function like this | d3.curveLinear  |   YES | ALL | YES |
contentInset | An object that specifies how much fake "margin" to use inside of the SVG canvas. This is particularly helpful on Android where overflow: "visible" isn't supported and might cause clipping. Note: important to have same contentInset on axis's and chart | object |   YES | ALL | YES |
numberOfTicks | We use d3-array to evenly distribute the grid and dataPoints on the yAxis. This prop specifies how many "ticks" we should try to render. Note: important that this prop is the same on both the chart and on the yAxis | number/undefined |   YES | ALL | YES |
showGrid | Whether or not to show the grid lines  | boolean |   YES | ALL | YES |
yMin | Alter how the chart bounds are calculated  | number/undefined |   YES | ALL | YES |
yMax | Alter how the chart bounds are calculated  |  number/undefined |   YES | ALL | YES |
xMin | Alter how the chart bounds are calculated  |  number/undefined |   YES | ALL | YES |
xMax | Alter how the chart bounds are calculated  |  number/undefined |   YES | ALL | YES |
children | One or many react-native-svg components that will be used to enhance your chart |  ReactNode |   YES | ALL | YES |

### 属性children
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| x  | a function that normally accepts the index of a data point an returns its 'x' location on the canvas         |  nunmber/string  | YES | ALL      | YES |
| y  | a function that normally accepts the value of a data point an returns its 'y' location on the canvas        |  nunmber/string  | YES | ALL      | YES |
| width  | the width of the canvas in pixels        |  number/srting  | YES | ALL      | YES |
| height  | the height of the canvas in pixels        |   number/srting  | YES | ALL      | YES |
| data  | the same data array provided to the chart, use this to map over your data points if you want decorators on each point        |  array  | YES | ALL      | YES |
| ticks  | if numberOfTicks has been provided to the chart this array will include the calculated tick values (useful for grids)       |  array  | YES | ALL      | YES |

### 组件特有属性

#### Area
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| start  | The value of which the area should start (will always end on the data point)    |  number/undefined  | YES | ALL      | YES |

#### StackedAreaChart
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An array of the data entries    |  array  | YES | ALL      | YES |
| keys  | This array should contain the object keys of interest (see above example)    |  array  | YES | ALL      | YES |
| colors  | An array of equal size as keys with the color for each key    |  array  | YES | ALL      | YES |
| order  | The order in which to sort the areas    |  d3.stackOrderNone  | YES | ALL      | YES |
| offset  | A function to determine the offset of the areas    |  d3.stackOffsetNone  | YES | ALL  | YES |

#### BarChart
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | The data prop in a barChart can look exactly like in a Line- or AreaChart, i.e an array of just numbers or complex objects. It can however also be an array with several data sets. A data object can contain a svg property which allows you two override styles on that specific object.     |  array  | YES | ALL      | YES |
| horizontal  | Boolean whether or not the bars should be horizontal   |  boolean  | YES | ALL      | YES |
| svg  | Default svg props for all bars. Supports all svg props an svg path normally supports. This styles will be overriden if there are specific styles for a given data object   |  object  | YES | ALL      | YES |
| spacingInner  | Spacing between the bars (or groups of bars)    |  number/undefined   | YES | ALL      | YES |
| spacingOuter  | Spacing outside of the bars (or groups of bars). Percentage of one bars width    |  number/undefined   | YES | ALL      | YES |
| contentInset  | PropTypes.shape    |  object  | YES | ALL      | YES |
| children.bandwidth  | the width of a band (a.k.a bar)    |  number  | YES | ALL      | YES |

#### StackedBarChart
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An array of the data entries: each value can be a number or a complex object with custom svg props for example    |  array  | YES | ALL      | YES |
| keys  | This array should contain the object keys of interest (see above example)    |  array  | YES | ALL      | YES |
| colors  | An array of equal size as keys with the color for each key    |  array  | YES | ALL      | YES |
| valueAccessor  | Very similar to the yAccessor of the other charts, usually needed when using complex objects as values    |  function  | YES | ALL      | YES |
| horizontal  | Boolean whether or not the bars should be horizontal   |  boolean  | YES | ALL      | YES |
| order  | The order in which to sort the areas    |  d3.stackOrderNone  | YES | ALL      | YES |
| offset  | A function to determine the offset of the areas    |  d3.stackOffsetNone | YES | ALL  | YES |

#### PieChart
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | Very similar to the data prop of our other charts, the only exception is that the PieChart only accepts complex objects (not just numbers). An item can also contain the arc property which allows you two override settings on that specific arc    |  array  | YES | ALL      | YES |
| valueAccessor  | Very similar to the yAccessor of the other charts    |  function  | YES | ALL      | YES |
| outerRadius  | The outer radius, use this to tweak how close your pie is to the edge of it's container. Takes either percentages or absolute numbers (pixels)    |  number/string/undefined  | YES | ALL      | YES |
| innerRadius  | The inner radius, use this to create a donut. Takes either percentages or absolute numbers (pixels)    |  number/string/undefined  | YES | ALL      | YES |
| labelRadius  | The radius of the circle that will help you layout your labels. Takes either percentages or absolute numbers (pixels)    |  number/string/undefined  | YES | ALL      | YES |
| padAngle  | The angle between the slices    |  number/undefined  | YES | ALL      | YES |
| startAngle  | The start angle in radians of the entire pie    |  number/undefined  | YES | ALL      | YES |
| endAngle  | The end angle in radians of the entire pie    |  number/undefined  | YES | ALL      | YES |
| sort  | Like any normal sort function it expects either 0, a positive or negative return value. The arguments are each an object from the dataPoints array   |  function  | YES | ALL      | YES |
| children.slices  | an array of the pie chart slices. See source code and examples for what it includes    |  array  | YES | ALL      | YES |

#### ProgressCircle
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| progress  | PropTypes.number.isRequired    |  number  | YES | ALL  | YES |
| progressColor  | PPropTypes.any    |  string/undefined  | YES | ALL  | YES |
| backgroundColor  | PropTypes.any    |  string/undefined  | YES | ALL  | YES |
| startAngle  | PropTypes.number    |  number/undefined  | YES | ALL  | YES |
| endAngle  | PropTypes.number    |  number/undefined  | YES | ALL  | YES |
| strokeWidth  | PropTypes.number    |  number/undefined  | YES | ALL  | YES |
| cornerRadius  | PropTypes.number    |  number/undefined | YES | ALL  | YES |

#### YAxis
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scale  | Should be the same as passed into the charts yScale, or d3Scale.scaleBand if used in conjunction with a horizontal BarChart   |  d3Scale.scaleLinear  | YES | ALL  | YES |
| svg  | supports all svg props an svg text normally supports   |  object  | YES | ALL      | YES |
| spacingInner  | Spacing between the labels. Only applicable if scale=d3Scale.scaleBand and should then be equal to spacingInner prop on the actual BarChart   |  number/undefined   | YES | ALL      | YES |
| spacingOuter  | 	Spacing outside of the labels. Only applicable if scale=d3Scale.scaleBand and should then be equal to spacingOuter prop on the actual BarChart   |  number/undefined  | YES | ALL      | YES |
| formatLabel  | A utility function to format the text before it is displayed, e.g `value => "$" + value   |  function|undefined  | YES | ALL      | YES |
| contentInset  | Used to sync layout with chart (if same prop used there)   |  object  | YES | ALL      | YES |
| min  | Used to sync layout with chart (if gridMin is used there)  | number/undefined | YES | ALL      | YES |
| max  | Used to sync layout with chart (if gridMax is used there)  | number/undefined | YES | ALL      | YES |

#### XAxis
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| data  | An array of values or objects to render on the xAxis. Should preferably have the same length as the chart's dataPoints. If a complex object is used instead of a simple value, a xAccessor prop is required to calculate the axis' extent. A data object can contain a svg property which allows you to override styles on that specific object  |  array  | YES | ALL      | YES |
| scale  | Should be the same as passed into the charts xScale   |  d3Scale.scaleLinear  | YES | ALL  | YES |
| spacingInner  | Spacing between the labels. Only applicable if scale=d3Scale.scaleBand and should then be equal to spacingInner prop on the actual BarChart   |  number/undefined   | YES | ALL      | YES |
| spacingOuter  | 	Spacing between the labels. Only applicable if scale=d3Scale.scaleBand and should then be equal to spacingOuter prop on the actual BarChart   |  number/undefined  | YES | ALL      | YES |
| svg  | Default svg props for all labels. Supports all svg props an svg text normally supports. This styles will be overriden if there are specific styles for a given data object   |  object  | YES | ALL      | YES |
| formatLabel  | A utility function to format the text before it is displayed, e.g value => "day" + value. Passes back the value provided by the xAccessor   |  function  | YES | ALL      | YES |
| contentInset  | Used to sync layout with chart (if same prop used there)  |  object  | YES | ALL      | YES |


#### Grid
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| svg  | an object containing all the props that should be passed down to the underlying react-native-svg component.   |  object  | YES | ALL      | YES |
| direction  | The direction of the grid lines.  |  Grid.Direction  | YES | ALL      | YES |
| belowChart  | whether or not to render below the chart.  |  boolean  | YES | ALL      | YES |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/JesperLekland/react-native-svg-charts/blob/dev/LICENSE) ，请自由地享受和参与开源。
