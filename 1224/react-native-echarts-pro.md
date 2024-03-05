模板版本：v1.9.1

<p align="center">
  <h1 align="center"> <code>react-native-echarts-pro</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-echarts-pro">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-echarts-pro)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-library/react-native-echarts-pro> Releases](https://github.com/react-native-oh-library/react-native-echarts-pro/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-echarts-pro@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-echarts-pro@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

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

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档的 Link 章节](/zh-cn/react-native-webview.md)进行引入

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.1.6.6;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-echarts-pro](https://github.com/supervons/react-native-echarts-pro/tree/master)

### Properties for all react-native-echarts-pro components:

| Name                      | Description                                                  | **Type** | Platform    | Required | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------ | -------- | ----------- | -------- | ----------------- |
| height                    | Chart area height                                            | Number   | All         | Y        | Yes               |
| width                     | Chart area auto                                              | Number   | All         | N        | Yes               |
| option                    | Chart configuration, see more：[Apache ECharts - options](https://echarts.apache.org/en/option.html#title) | Object   | All         | Y        | Yes               |
| backgroundColor           | Chart background color                                       | String   | All         | N        | Yes               |
| themeName                 | There are only six officially available themes:<br/>`vintage` `dark` `macarons` `infographic` `shine` `roma` | String   | All         | N        | Yes               |
| webViewSettings           | Customize WebView container properties                       | Object   | All         | N        | Yes               |
| formatterVariable         | If option’formatter function need variable,can use this.     | Object   | All         | N        | Yes               |
| extension                 | Dynamic support for tripartite expansion, such as word cloud, water polo map, etc. example. | object   | All         | N        | Yes               |
| customMapData             | For custom maps, null is a world map. See the following usage examples | Object   | All         | N        | Yes               |
| eventActions              | Custom charts events.                                        | Object   | All         | N        | Yes               |
| fontFamilies              | Custom font families.                                        | Array    | Android/ios | N        | No                |
| enableParseStringFunction | If enabled, function are parse as strings                    | Boolean  | All         | N        | Yes               |

## 遗留问题

1、由于事件传递依托于 react-native-webview 的postMessage 方法，而该方法暂未鸿蒙化，所以该三方库的方法暂时无法使用[issues/17](https://github.com/react-native-oh-library/react-native-webview/issues/17)

2、base64形式的自定义字体在 react-native-webview 中无法使用，导致该三方库也无法使用自定义字体[issues/20](https://github.com/react-native-oh-library/react-native-webview/issues/20)

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/oblador/react-native-progress/blob/master/LICENSE) ，请自由地享受和参与开源。