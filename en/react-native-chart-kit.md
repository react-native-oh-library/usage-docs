> Template version: v0.2.1  

  <p align="center">  
  <h1 align="center"> <code>react-native-chart-kit</code> </h1>  
  </p >  
  <p align="center">
      <a>
       <a href="https://github.com/indiespirit/react-native-chart-kit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
     <a>
        <a href="https://github.com/indiespirit/react-native-chart-kit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p> 




> [!TIP] 
>
> [GitHub address](https://github.com/indiespirit/react-native-chart-kit)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

**npm**

```bash
npm install react-native-chart-kit@^6.12.0
```

**yarn**

```bash
yarn add react-native-chart-kit@^6.12.0
```



<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.


```js
import React from 'react';
import { View, Dimensions, StyleSheet } from 'react-native';
import { LineChart } from 'react-native-chart-kit';

const data = {
  labels: ['January', 'February', 'March', 'April', 'May', 'June'],
  datasets: [{
    data: [20, 45, 28, 80, 99, 43]
  }]
};

const MyChart = () => {
  const screenWidth = Dimensions.get('window').width;

  return (
    <View style={styles.container}>
      <LineChart
        data={data}
        width={screenWidth - 20} // Adjust width to fit the screen with some margin
        height={220}
        yAxisLabel={'$'}
        chartConfig={{
          backgroundColor: '#e26a00',
          backgroundGradientFrom: '#fb8c00',
          backgroundGradientTo: '#ffa726',
          decimalPlaces: 2, // Adjust decimal places to 2
          color: (opacity = 1) => `rgba(255, 255, 255, ${opacity})`,
          labelColor: (opacity = 1) => `rgba(255, 255, 255, ${opacity})`,
          style: {
            borderRadius: 16
          },
          propsForDots: {
            r: '6',
            strokeWidth: '2',
            stroke: '#ffa726'
          }
        }}
        bezier
        style={styles.chart}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF'
  },
  chart: {
    marginVertical: 8,
    borderRadius: 16
  }
});

export default MyChart;
```


## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg documentation Link chapter](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg-capi.md#link) to add it to your project.

## Constraints

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.300SP1; ROM：3.0.0.18;

## Properties (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### Chart style 

| Name                            | Description                                                  | Type               | Required | Platform | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------ | ------------------ | -------- | -------- | ----------------- |
| `backgroundGradientFrom`        | Defines the first color in the linear gradient of a chart's background | String             | No       | All      | Yes               |
| `backgroundGradientFromOpacity` | Defines the first color opacity in the linear gradient of a chart's background | Number             | No       | All      | Yes               |
| `backgroundGradientTo`          | Defines the second color in the linear gradient of a chart's background | String             | No       | All      | Yes               |
| `backgroundGradientToOpacity`   | Defines the second color opacity in the linear gradient of a chart's background | Number             | No       | All      | Yes               |
| `fillShadowGradientFrom`        | Defines the first color in the linear gradient of the area under data | String             | No       | All      | Yes               |
| `fillShadowGradientFromOpacity` | Defines the first color opacity in the linear gradient of the area under data | Number             | No       | All      | Yes               |
| `fillShadowGradientFromOffset`  | Defines the first color offset (0-1) in the linear gradient of the area under data | Number             | No       | All      | Yes               |
| `fillShadowGradientTo`          | Defines the second color in the linear gradient of the area under data | String             | No       | All      | Yes               |
| `fillShadowGradientToOpacity`   | Defines the second color opacity in the linear gradient of the area under data | Number             | No       | All      | Yes               |
| `fillShadowGradientToOffset`    | Defines the second color offset (0-1) in the linear gradient of the area under data | Number             | No       | All      | Yes               |
| `useShadowColorFromDataset`     | Defines the option to use color from dataset to each chart data. Default is false | Boolean            | No       | All      | Yes               |
| `color`                         | Defines the base color function that is used to calculate colors of labels and sectors used in a chart | Function => String | No       | All      | Yes               |
| `strokeWidth`                   | Defines the base stroke width in a chart                     | Number             | No       | All      | Yes               |
| `barPercentage`                 | Defines the percent (0-1) of the available width each bar width in a chart | Number             | No       | All      | Yes               |
| `barRadius`                     | Defines the radius of each bar                               | Number             | No       | All      | Yes               |
| `propsForBackgroundLines`       | Override styles of the background lines, refer to react-native-svg's Line documentation | Props              | No       | All      | Yes               |
| `propsForLabels`                | Override styles of the labels, refer to react-native-svg's Text documentation | Props              | No       | All      | Yes               |
| `propsForVerticalLabels`        | Override styles of vertical labels, refer to react-native-svg's Text documentation | Props              | No       | All      | Yes               |
| `propsForHorizontalLabels`      | Override styles of horizontal labels, refer to react-native-svg's Text documentation | Props              | No       | All      | Yes               |

### Line Chart

| Name                    | Description                                                  | Type                    | Required | Platform | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------ | ----------------------- | -------- | -------- | ----------------- |
| data                    | Data for the chart - see example above                       | Object                  | No       | All      | Yes               |
| width                   | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive | Number                  | No       | All      | Yes               |
| height                  | Height of the chart                                          | Number                  | No       | All      | Yes               |
| withDots                | Show dots on the line - default: True                        | boolean                 | No       | All      | Yes               |
| withShadow              | Show shadow for line - default: True                         | boolean                 | No       | All      | Yes               |
| withInnerLines          | Show inner dashed lines - default: True                      | boolean                 | No       | All      | Yes               |
| withOuterLines          | Show outer dashed lines - default: True                      | boolean                 | No       | All      | Yes               |
| withVerticalLines       | Show vertical lines - default: True                          | boolean                 | No       | All      | Yes               |
| withHorizontalLines     | Show horizontal lines - default: True                        | boolean                 | No       | All      | Yes               |
| withVerticalLabels      | Show vertical labels - default: True                         | boolean                 | No       | All      | Yes               |
| withHorizontalLabels    | Show horizontal labels - default: True                       | boolean                 | No       | All      | Yes               |
| fromZero                | Render charts from 0 not from the minimum value. - default: False | boolean                 | No       | All      | Yes               |
| yAxisLabel              | Prepend text to horizontal labels -- default: ''             | string                  | No       | All      | Yes               |
| yAxisSuffix             | Append text to horizontal labels -- default: ''              | string                  | No       | All      | Yes               |
| xAxisLabel              | Prepend text to vertical labels -- default: ''               | string                  | No       | All      | Yes               |
| yAxisInterval           | Display y axis line every {x} input. -- default: 1           | string                  | No       | All      | Yes               |
| chartConfig             | Configuration object for the chart, see example config object above | Object                  | No       | All      | Yes               |
| decorator               | This function takes a whole bunch of stuff and can render extra elements, such as data point info or additional markup. | Function                | No       | All      | Yes               |
| onDataPointClick        | Callback that takes {value, dataset, getColor}               | Function                | No       | All      | Yes               |
| horizontalLabelRotation | Rotation angle of the horizontal labels - default 0          | number (degree)         | No       | All      | Yes               |
| verticalLabelRotation   | Rotation angle of the vertical labels - default 0            | number (degree)         | No       | All      | Yes               |
| getDotColor             | Defines the dot color function that is used to calculate colors of dots in a line chart and takes (dataPoint, dataPointIndex) | function => string      | No       | All      | Yes               |
| renderDotContent        | Render additional content for the dot. Takes ({x, y, index, indexData}) as arguments. | Function                | No       | All      | Yes               |
| yLabelsOffset           | Offset for Y axis labels                                     | number                  | No       | All      | Yes               |
| xLabelsOffset           | Offset for X axis labels                                     | number                  | No       | All      | Yes               |
| hidePointsAtIndex       | Indices of the data points you don't want to display         | number[]                | No       | All      | Yes               |
| formatYLabel            | This function change the format of the display value of the Y label. Takes the Y value as argument and should return the desirable string. | Function                | No       | All      | Yes               |
| formatXLabel            | This function change the format of the display value of the X label. Takes the X value as argument and should return the desirable string. | Function                | No       | All      | Yes               |
| getDotProps             | This is an alternative to chartConfig's propsForDots         | (value, index) => props | No       | All      | Yes               |
| segments                | The amount of horizontal lines - default 4                   | number                  | No       | All      | Yes               |

### Bezier Line Chart

|      |                                        |        |          |          |                   |
| ---- | -------------------------------------- | ------ | -------- | -------- | ----------------- |
| Name | Description                            | Type   | Required | Platform | HarmonyOS Support |
| data | Data for the chart - see example above | Object | No       | All      | Yes               |

### Progress Ring

| Property    | Type    | Description                                                  | Required | Platform | HarmonyOS Support |
| ----------- | ------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| data        | Object  | Data for the chart - see example above                       | No       | ALL      | YES               |
| width       | Number  | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive | No       | ALL      | YES               |
| height      | Number  | Height of the chart                                          | No       | ALL      | YES               |
| strokeWidth | Number  | Width of the stroke of the chart - default: 16               | No       | ALL      | YES               |
| radius      | Number  | Inner radius of the chart - default: 32                      | No       | ALL      | YES               |
| chartConfig | Object  | Configuration object for the chart, see example config in the beginning of this file | No       | ALL      | YES               |
| hideLegend  | Boolean | Switch to hide chart legend (defaults to false)              | No       | ALL      | YES               |

### Bar chart

| Property                | Type    | Description                                                  | Required | Platform | HarmonyOS Support |
| ----------------------- | ------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| data                    | Object  | Data for the chart - see example above                       | No       | ALL      | YES               |
| width                   | Number  | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive | No       | ALL      | YES               |
| height                  | Number  | Height of the chart                                          | No       | ALL      | YES               |
| withVerticalLabels      | boolean | Show vertical labels - default: True                         | No       | ALL      | YES               |
| withHorizontalLabels    | boolean | Show horizontal labels - default: True                       | No       | ALL      | YES               |
| fromZero                | boolean | Render charts from 0 not from the minimum value. - default: False | No       | ALL      | YES               |
| withInnerLines          | boolean | Show inner dashed lines - default: True                      | No       | ALL      | YES               |
| yAxisLabel              | string  | Prepend text to horizontal labels -- default: ''             | No       | ALL      | YES               |
| yAxisSuffix             | string  | Append text to horizontal labels -- default: ''              | No       | ALL      | YES               |
| chartConfig             | Object  | Configuration object for the chart, see example config in the beginning of this file | No       | ALL      | YES               |
| horizontalLabelRotation | number  | Rotation angle of the horizontal labels - default 0          | No       | ALL      | YES               |
| verticalLabelRotation   | number  | Rotation angle of the vertical labels - default 0            | No       | ALL      | YES               |
| showBarTops             | boolean | Show bar tops                                                | No       | ALL      | YES               |
| showValuesOnTopOfBars   | boolean | Show value above bars                                        | No       | ALL      | YES               |

### StackedBar chart

| Property             | Type    | Description                                                  | Required | Platform | HarmonyOS Support |
| -------------------- | ------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| data                 | Object  | Data for the chart - see example above                       | No       | ALL      | YES               |
| width                | Number  | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive | No       | ALL      | YES               |
| height               | Number  | Height of the chart                                          | No       | ALL      | YES               |
| withVerticalLabels   | boolean | Show vertical labels - default: True                         | No       | ALL      | YES               |
| withHorizontalLabels | boolean | Show horizontal labels - default: True                       | No       | ALL      | YES               |
| chartConfig          | Object  | Configuration object for the chart, see example config in the beginning of this file | No       | ALL      | YES               |
| barPercentage        | Number  | Defines the percent (0-1) of the available width each bar width in a chart | No       | ALL      | YES               |
| showLegend           | boolean | Show legend - default: True                                  | No       | ALL      | YES               |

### Pie chart

| Property       | Type    | Description                                                  | Required | Platform | HarmonyOS Support |
| -------------- | ------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| data           | Object  | Data for the chart - see example above                       | No       | ALL      | YES               |
| width          | Number  | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive | No       | ALL      | YES               |
| height         | Number  | Height of the chart                                          | No       | ALL      | YES               |
| chartConfig    | Object  | Configuration object for the chart, see example config in the beginning of this file | No       | ALL      | YES               |
| accessor       | string  | Property in the data object from which the number values are taken | No       | ALL      | YES               |
| bgColor        | string  | Background color - if you want to set transparent, input transparent or none. | No       | ALL      | YES               |
| paddingLeft    | string  | Left padding of the pie chart                                | No       | ALL      | YES               |
| center         | array   | Offset x and y coordinates to position the chart             | No       | ALL      | YES               |
| absolute       | boolean | Shows the values as absolute numbers                         | No       | ALL      | YES               |
| hasLegend      | boolean | Defaults to true, set it to false to remove the legend       | No       | ALL      | YES               |
| avoidFalseZero | boolean | Defaults to false, set it to true to display a "<1%" instead of a rounded value equal to "0%" | No       | ALL      | YES               |

### Contribution graph (heatmap)

| Property           | Type     | Description                                                  | Required | Platform | HarmonyOS Support |
| ------------------ | -------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| data               | Object   | Data for the chart - see example above                       | No       | ALL      | YES               |
| width              | Number   | Width of the chart, use 'Dimensions' library to get the width of your screen for responsive | No       | ALL      | YES               |
| height             | Number   | Height of the chart                                          | No       | ALL      | YES               |
| gutterSize         | Number   | Size of the gutters between the squares in the chart         | No       | ALL      | YES               |
| squareSize         | Number   | Size of the squares in the chart                             | No       | ALL      | YES               |
| horizontal         | boolean  | Should graph be laid out horizontally? Defaults to true      | No       | ALL      | YES               |
| showMonthLabels    | boolean  | Should graph include labels for the months? Defaults to true | No       | ALL      | YES               |
| showOutOfRangeDays | boolean  | Should graph be filled with squares, including days outside the range? Defaults to false | No       | ALL      | YES               |
| chartConfig        | Object   | Configuration object for the chart, see example config in the beginning of this file | No       | ALL      | YES               |
| accessor           | string   | Property in the data object from which the number values are taken; defaults to count | No       | ALL      | YES               |
| getMonthLabel      | function | Function which returns the label for each month, taking month index (0 - 11) as argument | No       | ALL      | YES               |
| onDayPress         | function | Callback invoked when the user clicks a day square on the chart; takes a value-item object | No       | ALL      | YES               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/indiespirit/react-native-chart-kit/blob/master/LICENSE).