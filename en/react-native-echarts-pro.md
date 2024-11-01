> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-echarts-pro</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/supervons/react-native-echarts-pro/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/supervons/react-native-echarts-pro)

## Installation and Usage

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### npm

```bash
npm install react-native-echarts-pro@^1.9.1
```

#### yarn

```bash
yarn add react-native-echarts-pro@^1.9.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React from "react";
import { View } from "react-native";
import RNEChartsPro from "react-native-echarts-pro";

export default function RNEPDemo() {
  const pieOption = {
    series: [
      {
        name: "Source",
        type: "pie",
        legendHoverLink: true,
        hoverAnimation: true,
        avoidLabelOverlap: true,
        startAngle: 180,
        radius: "55%",
        center: ["50%", "35%"],
        data: [
          { value: 105.2, name: "android" },
          { value: 310, name: "iOS" },
          { value: 234, name: "web" },
          { value: 134, name: "harmony" },
        ],
        label: {
          normal: {
            show: true,
            textStyle: {
              fontSize: 12,
              color: "#23273C",
            },
          },
        },
      },
    ],
  };
  return (
    <View style={{ height: 300, paddingTop: 25 }}>
      <RNEChartsPro height={250} option={pieOption} />
    </View>
  );
}
```

## Link

The HarmonyOS implementation of this library relies on the native code of @react-native-oh-tpl/react-native-webview，If the library has already been introduced in the HarmonyOS project, there is no need to introduce it again. You can skip the steps in this chapter and use it directly.

If not introduced, please refer to the Link section of the document[@react-native-oh-tpl/react-native-webview ](react-native-webview.md)for introduction.

## Constraints

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-echarts-pro](https://github.com/supervons/react-native-echarts-pro/tree/master)

### Properties for all react-native-echarts-pro components:

| Name                      | Description                                                                                                  | **Type** | Platform    | Required | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------------------------------------ | -------- | ----------- | -------- | ----------------- |
| height                    | Chart area height                                                                                            | Number   | All         | Y        | Yes               |
| width                     | Chart area auto                                                                                              | Number   | All         | N        | Yes               |
| option                    | Chart configuration, see more：[Apache ECharts - options](https://echarts.apache.org/en/option.html#title)   | Object   | All         | Y        | Yes               |
| backgroundColor           | Chart background color                                                                                       | String   | All         | N        | Yes               |
| themeName                 | There are only six officially available themes:<br/>`vintage` `dark` `macarons` `infographic` `shine` `roma` | String   | All         | N        | Yes               |
| webViewSettings           | Customize WebView container properties                                                                       | Object   | All         | N        | Yes               |
| formatterVariable         | If option’formatter function need variable,can use this.                                                     | Object   | All         | N        | Yes               |
| extension                 | Dynamic support for tripartite expansion, such as word cloud, water polo map, etc. example.                  | object   | All         | N        | Yes               |
| customMapData             | For custom maps, null is a world map. See the following usage examples                                       | Object   | All         | N        | Yes               |
| eventActions              | Custom charts events.                                                                                        | Object   | All         | N        | Yes               |
| fontFamilies              | Custom font families.                                                                                        | Array    | Android/ios | N        | No                |
| enableParseStringFunction | If enabled, function are parse as strings                                                                    | Boolean  | All         | N        | Yes               |

## Known Issues

- [ ] fontFamilies自定义字体属性未生效，该属性需要将字体文件转为base64字符串，拼接在html中的style标签中使用，经验证，这种用法在react-native-webview的最小化demo也不生效，一旦有base64字体加载，就会白屏并无法触发loadEnd，而原生 HarmonyOS webview上显示正常 [issues#20](https://github.com/react-native-oh-library/react-native-webview/issues/20)

## Others

## License

This project is licensed under [MIT License](https://github.com/oblador/react-native-progress/blob/master/LICENSE).
