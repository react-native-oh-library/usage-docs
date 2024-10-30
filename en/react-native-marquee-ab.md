> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-marquee-ab</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/6.x/packages/stack">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://choosealicense.com/licenses/mit/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/ZhangTaoK/react-native-marquee-ab)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install --save react-native-marquee-ab@1.2.6
```

#### **yarn**

```bash
yarn add react-native-marquee-ab@1.2.6
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import React, { Component } from "react";
import { View, Text, Image, Dimensions } from "react-native";
import { MarqueeHorizontal, MarqueeVertical } from "react-native-marquee-ab";
export default class TestPage extends Component {
  render() {
    let mWidth = Dimensions.get("window").width;
    return (
      <View style={{ flex: 1, backgroundColor: "#FFFFFF" }}>
        <View
          style={{ height: 50, backgroundColor: "#FFFFFF", width: "100%" }}
        />
        <MarqueeHorizontal
          textList={[
            {
              label: "1",
              value:
                "item1:Twinkle.twinkle little star,the sky is full of little stars",
            },
            { label: "2", value: "item2:Two tigers run fast" },
            {
              label: "3",
              value:
                "item3:White clouds float in the blue sky, and little fat sheep run under them",
            },
          ]}
          speed={60}
          width={mWidth}
          height={50}
          direction={"left"}
          reverse={false}
          bgContainerStyle={{ backgroundColor: "#FFFF00" }}
          textStyle={{ fontSize: 16, color: "#FF0000" }}
          onTextClick={(item) => {
            alert("" + JSON.stringify(item));
          }}
        />
      </View>
    );
  }
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.29; SDK: HarmonyOS NEXT Developer Beta6; IDE: DevEco Studio 5.0.3.706; ROM: NEXT.0.0.65;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**MarqueeHorizontal props**

| Name             | Description                                       | Type           | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------- | -------------- | -------- | ----------- | ----------------- |
| duration         | 执行完成整个动画所需要的时间(ms)不常用            | number         | yes      | iOS/Android | yes               |
| speed            | 平均的滚动速度，跑马灯使用这个属性（建议传入 60） | number         | no       | iOS/Android | yes               |
| textList         | 滚动的文字数组，具体数据格式请参照 textList.item  | array          | yes      | iOS/Android | yes               |
| width            | 宽度，不能使用 flex                               | number         | yes      | iOS/Android | yes               |
| height           | 高度，不能使用 flex                               | number         | yes      | iOS/Android | yes               |
| direction        | 动画方向(向左向右滚动)`left` or `right`           | string         | yes      | iOS/Android | yes               |
| reverse          | 是否将整个文本数据倒叙显示                        | boolean        | yes      | iOS/Android | yes               |
| separator        | 两个 item 之间的间隙                              | number         | yes      | iOS/Android | yes               |
| bgContainerStyle | 背景样式                                          | object         | no       | iOS/Android | yes               |
| textStyle        | 文本样式                                          | object         | no       | iOS/Android | yes               |
| onTextClick      | 点击事件回调                                      | (item) => void | yes      | iOS/Android | yes               |

**MarqueeVertical props**

| Name             | Description                                                                                          | Type           | Required | Platform    | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------- | -------------- | -------- | ----------- | ----------------- |
| duration         | 执行完成整个动画所需要的时间(ms)                                                                     | number         | yes      | iOS/Android | yes               |
| textList         | 滚动的文字数组，具体数据格式请参照 textList.item                                                     | array          | yes      | iOS/Android | yes               |
| width            | 宽度，不能使用 flex                                                                                  | number         | no       | iOS/Android | yes               |
| height           | 高度，不能使用 flex                                                                                  | number         | no       | iOS/Android | yes               |
| delay            | 文本停顿时间(ms)                                                                                     | number         | yes      | iOS/Android | yes               |
| direction        | 动画方向(向上向下滚动)`up` or `down`                                                                 | string         | yes      | iOS/Android | yes               |
| numberOfLines    | 同一个数据的文本行数                                                                                 | number         | yes      | iOS/Android | yes               |
| headViews        | 在文本最前面加上一个自定义 view，效果如图例所示，用法请参照事例用法，length 长度与 textList 必须一致 | array          | no       | iOS/Android | yes               |
| viewStyle        | 每一行文本的样式                                                                                     | object         | yes      | iOS/Android | yes               |
| bgContainerStyle | 背景样式                                                                                             | object         | no       | iOS/Android | yes               |
| textStyle        | 文本样式                                                                                             | object         | no       | iOS/Android | yes               |
| onTextClick      | 点击事件回调                                                                                         | (item) => void | yes      | iOS/Android | yes               |

**textList.item props**

| Name     | Description                      | Type     | Required | Platform    | HarmonyOS Support |
| -------- | -------------------------------- | -------- | -------- | ----------- | ----------------- |
| label    | 用作点击事件的回调               | string   | yes      | iOS/Android | yes               |
| value    | 文本显示                         | string   | yes      | iOS/Android | yes               |
| [object] | 可随意添加数据供自己特殊需求使用 | [object] | no       | iOS/Android | yes               |

## Known Issues

- [ ] MarqueeHorizontal 的 reverse 属性在 HarmonyOS 上只有第一次修改会触发生效，而原库在 iOS 上该属性已经失效。未实现 HarmonyOS 化 问题[issue#58](https://github.com/ZhangTaoK/react-native-marquee-ab/issues/58)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://choosealicense.com/licenses/mit/).
