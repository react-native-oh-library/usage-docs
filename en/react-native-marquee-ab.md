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
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**MarqueeHorizontal props**

| Name             | Description                                       | Type           | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------- | -------------- | -------- | ----------- | ----------------- |
| duration         | Time (ms) required to complete the entire animation. It is not commonly used.           | number         | yes      | iOS/Android | yes               |
| speed            | Average scrolling speed. This property is used for marquee (**60** is recommended).| number         | no       | iOS/Android | yes               |
| textList         | Scrolling text array. For details about the data format, see textList.item. | array          | yes      | iOS/Android | yes               |
| width            | Width. Flex is not allowed.                              | number         | yes      | iOS/Android | yes               |
| height           | Height. Flex is not allowed.                              | number         | yes      | iOS/Android | yes               |
| direction        | Animation scrolling direction, `left` or `right`.          | string         | yes      | iOS/Android | yes               |
| reverse          | Whether to display the entire text data in reverse order.                       | boolean        | yes      | iOS/Android | yes               |
| separator        | Separator between two items.                             | number         | yes      | iOS/Android | yes               |
| bgContainerStyle | Background style.                                         | object         | no       | iOS/Android | yes               |
| textStyle        | Text style.                                         | object         | no       | iOS/Android | yes               |
| onTextClick      | Callback for the click event.                                     | (item) => void | yes      | iOS/Android | yes               |

**MarqueeVertical props**

| Name             | Description                                                  | Type           | Required | Platform    | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------------- | -------- | ----------- | ----------------- |
| duration         | Time required to complete the entire animation (ms).                            | number         | yes      | iOS/Android | yes               |
| textList         | Scrolling text array. For details about the data format, see textList.item.            | array          | yes      | iOS/Android | yes               |
| width            | Width. Flex is not allowed.                                         | number         | no       | iOS/Android | yes               |
| height           | Height. Flex is not allowed.                                         | number         | no       | iOS/Android | yes               |
| delay            | Text delay (ms).                                            | number         | yes      | iOS/Android | yes               |
| direction        | Animation scrolling direction, `up` or `down`.                        | string         | yes      | iOS/Android | yes               |
| numberOfLines    | Number of text lines of the same data.                                        | number         | yes      | iOS/Android | yes               |
| headViews        | Adds a custom view at the beginning of the text. The effect and usage are shown in the example. The length must be the same as that of textList.| array          | no       | iOS/Android | yes               |
| viewStyle        | Style of each line of text.                                            | object         | yes      | iOS/Android | yes               |
| bgContainerStyle | Background style.                                                    | object         | no       | iOS/Android | yes               |
| textStyle        | Text style.                                                    | object         | no       | iOS/Android | yes               |
| onTextClick      | Callback for the click event.                                                | (item) => void | yes      | iOS/Android | yes               |

**textList.item props**

| Name     | Description                      | Type     | Required | Platform    | HarmonyOS Support |
| -------- | -------------------------------- | -------- | -------- | ----------- | ----------------- |
| label    | Callback for the click event.              | string   | yes      | iOS/Android | yes               |
| value    | Text display.                        | string   | yes      | iOS/Android | yes               |
| [object] | Data can be added for special use.| [object] | no       | iOS/Android | yes               |

## Known Issues

- [ ] The reverse property of MarqueeHorizontal takes effect only when it is modified for the first time in HarmonyOS. However, this property in the original third-party library is invalid in iOS and not compatible. [issue#58](https://github.com/ZhangTaoK/react-native-marquee-ab/issues/58).

## Others

## License

This project is licensed under [The MIT License (MIT)](https://choosealicense.com/licenses/mit/).
