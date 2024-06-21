<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-image-header-scroll-view</code></h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-render-html">
        <img src="https://img.shields.io/badge/platforms-ios%20|%20android%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-render-html/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址(v0.10.3)](https://github.com/bamlab/react-native-image-header-scroll-view/tree/0.10.3)  
> 因 v1.0.0 中存在无法触发 TriggeringView 组件回调的问题，以下基于 v0.10.3 版本验证

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-image-header-scroll-view@0.10.3 --save
```

#### **yarn**

```bash
yarn add react-native-image-header-scroll-view@0.10.3
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import { View, TouchableOpacity, Text } from "react-native";
import React from "react";
import HeaderImageScrollView, {
  TriggeringView,
} from "react-native-image-header-scroll-view";

export function ImageHeaderPropertyTest() {
  return (
    <HeaderImageScrollView
      maxHeight={200}
      minHeight={88}
      headerImage={require("./assets/NZ.jpg")}
      renderForeground={() => (
        <View
          style={{
            height: 150,
            justifyContent: "center",
            alignItems: "center",
          }}
        >
          <TouchableOpacity onPress={() => console.log("tap!!")}>
            <Text>Tap Me!</Text>
          </TouchableOpacity>
        </View>
      )}
    >
      <View style={{ height: 800 }}>
        <TriggeringView onHide={() => console.log("text hidden")}>
          <Text>Scroll Me!</Text>
        </TriggeringView>
      </View>
    </HeaderImageScrollView>
  );
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息： [Releases](https://github.com/bamlab/react-native-image-header-scroll-view/releases/tag/0.10.3)

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。详情可查看[react-native-image-header-scroll-view](https://github.com/bamlab/react-native-image-header-scroll-view/blob/0.10.3/README.md#usage-api)

### Header

| Name                 | Description                                                                                                                                                                                    | Type     | Required | Platform       | HarmonyOS Support |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------------- | ----------------- |
| renderHeader         | Function which return the component to use as header. It can return background image for example.                                                                                              | function | no       | All            | yes               |
| headerImage          | Shortcut for renderHeader={() => <Image source={this.props.headerImage} style={{ height: this.props.maxHeight, width: Dimensions.get('window').width }} />}                                    | Image source Props (object or number)      | no       | All            | yes               |
| maxHeight            | Max height for the header                                                                                                                                                                      | number   | no       | All            | yes               |
| minHeight            | Min height for the header (in navbar mode)                                                                                                                                                     | number   | no       | All            | yes               |
| minOverlayOpacity    | Opacity of a black overlay on the header before any scroll                                                                                                                                     | number   | no       | All            | yes               |
| maxOverlayOpacity    | Opacity of a black overlay on the header when in navbar mode                                                                                                                                   | number   | no       | All            | yes               |
| overlayColor         | Color of the overlay on the header                                                                                                                                                             | string   | no       | All            | yes               |
| useNativeDriver      | Use native driver for the animation for performance improvement. A few props are unsupported at the moment if useNativeDriver=true (onScroll, ScrollComponent, renderTouchableFixedForeground) | boolean  | no       | All            | yes               |
| headerContainerStyle | Optional styles to be passed to the container of the header component                                                                                                                          | Object   | no       | All            | yes               |
| disableHeaderGrow    | Disable to grow effect on the header                                                                                                                                                           | boolean  | no       | ios、HarmonyOS | yes               |

### Foreground

| Name                           | Description                                                                                                                                                                          | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| renderForeground               | Function which return the component to use at foreground. The component is render in front of the header and scroll with the ScrollView. It can return a title for example.          | function | no       | All      | yes               |
| renderFixedForeground          | Function which return the component to use as fixed foreground. The component is displayed with the header but not affected by the overlay.                                          | function | no       | All      | yes               |
| foregroundExtrapolate          | Optional prop that allows override extrapolate mode for foreground. Use null to allow extrapolation, which is usefull for using foreground as bottom title                           | string   | no       | All      | yes               |
| foregroundParallaxRatio        | Ration for parallax effect of foreground when scrolling. If 2, the header goes up two times faster than the scroll                                                                   | number   | no       | All      | yes               |
| fadeOutForeground              | If set, add a fade out effect on the foreground when scroll up                                                                                                                       | boolean  | no       | All      | yes               |
| renderTouchableFixedForeground | Same as renderFixedForeground but allow to use touchable in it. [Can cause performances issues on Android](https://github.com/bamlab/react-native-image-header-scroll-view/issues/6) | function | no       | All      | yes               |
| fixedForegroundContainerStyles | Optional styles to be passed to the container of the fixed foreground component                                                                                                      | Object   | no       | All      | yes               |

### Mixed

| Name                      | Description                                                                                                                             | Type      | Required | Platform | HarmonyOS Support |
| ------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | -------- | ----------------- |
| ScrollViewComponent       | The component to be used for scrolling. Can be any component with an onScroll props (ie. ListView, FlatList, SectionList or ScrollView) | Component | no       | All      | yes               |
| scrollViewBackgroundColor | Background color of the scrollView content                                                                                              | string    | no       | All      | yes               |

### TriggeringView

| Name             | Description                                                                                          | Type     | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| onBeginHidden    | Called when the component start to be hidden at the top of the scroll view.                          | function | no       | All      | yes               |
| onHide           | Called when the component is not displayed any more after scroll up                                  | function | no       | All      | yes               |
| onBeginDisplayed | Called when the component begin to be displayed again after scroll down                              | function | no       | All      | yes               |
| onDisplay        | Called when the component finished to be displayed again.                                            | function | no       | All      | yes               |
| onTouchTop       | Called when the Top of the component touch the Top of the ScrollView. (onDisplay + onBeginHidden)    | function | no       | All      | yes               |
| onTouchBottom    | Called when the Bottom of the component touch the Top of the ScrollView. (onHide + onBeginDisplayed) | function | no       | All      | yes               |

## 其他

- 如何去除图片阴影蒙层？  
  可通过设置 maxOverlayOpacity、minOverlayOpacity 属性为 0，去除图片阴影蒙层。
- 如何禁止滑动回弹效果？
  - 方法 1：设置 disableHeaderGrow 属性为 true
  - 方法 2：设置 bounces 属性为 false

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/meliorence/react-native-render-html/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->