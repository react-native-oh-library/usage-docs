<!-- {% raw %} -->

> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/shifeng1993/react-native-secharts)

## 安装与使用

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
              ? "这里显示被点击的值"
              : "被点击的值：" + this.state.value}
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

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-webview 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-webview 文档的 Link 章节](/zh-cn/react-native-webview.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.26; SDK：HarmonyOS NEXT Developer Beta1；IDE：DevEco Studio 5.0.3.300; ROM：3.0.0.24;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop              | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `option`          | echarts 配置项，option详情参见 https://echarts.apache.org/zh/option.html#title | object   | yes      | All      | yes               |
| `backgroundColor` | 图表画布背景色                                               | string   | no       | All      | yes               |
| `width`           | 画布宽度                                                     | number   | no       | All      | yes               |
| `height`          | 画布高度                                                     | number   | no       | All      | yes               |
| `renderLoading`   | loading 时遮罩，默认不支持自定义，如需自定义，请修改 react-native-secharts 依赖的源码 main/dist/index.js 中 startInLoadingState={true} | function | no       | All      | yes               |
| `onPress`         | 画布中数据点击事件                                           | function | no       | All      | yes               |

## 实例方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop        | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `setOption` | 该参数接收option对象，1.5.0 之后版本的 react-native-secharts 不建议使用此方法了，可以直接用 react 的组件内 state 进行绑定，如果需要变更，直接 setstate 新的 option 即可。） | function | no       | All      | yes               |
| `getImage`  | 返回函数的参数 base64，可结合 RNFS 写入相册                  | function | no       | All      | yes               |
| `clear`     | 清空 echarts 画布                                            | function | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/shifeng1993/react-native-secharts/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->

