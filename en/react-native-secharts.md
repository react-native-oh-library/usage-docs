> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-secharts</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/shifeng1993/react-native-secharts">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/shifeng1993/react-native-secharts/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/shifeng1993/react-native-secharts)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-secharts@1.7.0
```

#### **yarn**

```bash
yarn add react-native-secharts@1.7.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { View, StyleSheet, Text } from "react-native";
import { Echarts, echarts } from "react-native-secharts";

export default class SechartsBar extends Component {
  constructor(props) {
    super(props);
    this.state = {
      image: "",
      value: null,
      option1:
        (option = option =
          {
            xAxis: {
              type: "category",
              data: ["Mon", "Tue", "Wed", "Thu", "Fri"],
            },
            yAxis: {
              type: "value",
            },
            series: [
              {
                data: [120, 200, 150, 80, 70],
                type: "bar",
              },
            ],
          }),
      flag: false, // 这个布尔值是为了测试option1在setstate操作后不会被重置成初始状态。
    };
    this.echart1 = React.createRef();
  }

  render() {
    return (
      <View style={styles.container}>
        <View>
          <Echarts
            ref={this.echart1}
            option={this.state.option1}
            onPress={this.onPress}
            height={600}
            width={300}
            backgroundColor={"#468B58"}
            renderLoading={() => (
              <View style={{ backgroundColor: "rgba(255,255,0,0)" }} />
            )}
          />
        </View>
        <View>
          <Text>
            {!this.state.value
              ? "The clicked value is displayed here."
              : "The clicked value：" + this.state.value}
          </Text>
        </View>
      </View>
    );
  }
  onPress = (e) => {
    this.setState({ value: e.value });
  };
}
const styles = StyleSheet.create({
  container: {
    // flex: 1,
    // justifyContent: 'center',
    // alignItems: 'center',
    backgroundColor: "#F5FCFF",
  },
  buttonContainer: {
    width: 300,
    marginTop: 5,
  },
});
```

## Link

> [!TIP] This library depends on @react-native-oh-tpl/react-native-webview 13.10.2-0.2.0

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-webview. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-webview](/en/react-native-webview.md) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `option`          | echarts 配置项，option 详情参见 https://echarts.apache.org/zh/option.html#title                                                        | object   | yes      | All      | yes               |
| `backgroundColor` | 图表画布背景色                                                                                                                         | string   | no       | All      | yes               |
| `width`           | 画布宽度                                                                                                                               | number   | no       | All      | yes               |
| `height`          | 画布高度                                                                                                                               | number   | no       | All      | yes               |
| `renderLoading`   | loading 时遮罩，默认不支持自定义，如需自定义，请修改 react-native-secharts 依赖的源码 main/dist/index.js 中 startInLoadingState={true} | function | no       | All      | yes               |
| `onPress`         | 画布中数据点击事件                                                                                                                     | function | no       | All      | yes               |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Prop        | Description                                                                                                                                                                   | Type     | Required | Platform | HarmonyOS Support |
| ----------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `setOption` | 该参数接收 option 对象，1.5.0 之后版本的 react-native-secharts 不建议使用此方法了，可以直接用 react 的组件内 state 进行绑定，如果需要变更，直接 setstate 新的 option 即可。） | function | no       | All      | yes               |
| `getImage`  | 返回函数的参数 base64，可结合 RNFS 写入相册                                                                                                                                   | function | no       | All      | yes               |
| `clear`     | 清空 echarts 画布                                                                                                                                                             | function | no       | All      | yes               |

## Known Issues

## Others

renderLoading 属性在 Android 和 iOS 设置之后不生效，HarmonyOS 与 Android,iOS 表现一致。 [issue#109](https://github.com/shifeng1993/react-native-secharts/issues/109)

原库使用了在线 CDN，Echarts 组件需在网络支持下才能正常展示，HarmonyOS 与 Android,iOS 表现一致。 [issue#79](https://github.com/shifeng1993/react-native-secharts/issues/79)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/shifeng1993/react-native-secharts/blob/master/LICENSE).
