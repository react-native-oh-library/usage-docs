> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-snap-carousel</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-snap-carousel/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a> 
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-snap-carousel)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
$ npm install @react-native-oh-tpl/react-native-snap-carousel
```

```bash
$ yarn add @react-native-oh-tpl/react-native-snap-carousel
```

<!-- tabs:end -->

如果您使用的是 Typescript，您还应该安装类型定义：

```bash
$ npm install @types/react-native-snap-carousel
```

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from "react";
import { View, Text, Image } from "react-native";
import Carousel from "react-native-snap-carousel";

export default function SnapCarouselExample(): JSX.Element {
  const ENTRIES1 = [
    {
      title: "Beautiful and dramatic Antelope Canyon",
      subtitle: "Lorem ipsum dolor sit amet et nuncat mergitur",
      url: require("./img/UYiroysl.jpg"),
    },
    {
      title: "Earlier this morning, NYC",
      subtitle: "Lorem ipsum dolor sit amet",
      url: require("./img/UPrs1EWl.jpg"),
    },
    {
      title: "White Pocket Sunset",
      subtitle: "Lorem ipsum dolor sit amet et nuncat ",
      url: require("./img/MABUbpDl.jpg"),
    },
    {
      title: "Acrocorinth, Greece",
      subtitle: "Lorem ipsum dolor sit amet et nuncat mergitur",
      url: require("./img/KZsmUi2l.jpg"),
    },
    {
      title: "The lone tree, majestic landscape of New Zealand",
      subtitle: "Lorem ipsum dolor sit amet",
      url: require("./img/2nCt3Sbl.jpg"),
    },
    {
      title: "Middle Earth, Germany",
      subtitle: "Lorem ipsum dolor sit amet",
      url: require("./img/lceHsT6l.jpg"),
    },
  ];

  const _renderItem = ({ item, index }: any) => {
    return (
      <View>
        <Image source={item.url} style={styles.image} />
      </View>
    );
  };

  return (
    <View>
      <Carousel
        data={ENTRIES1}
        renderItem={_renderItem}
        sliderWidth={300}
        itemWidth={250}
        containerCustomStyle={styles.carouselContainer}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  carouselContainer: {
    height: 200,
    width: "100%",
    marginBottom: 20,
  },
});
```

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-snap-carousel Releases](https://github.com/react-native-oh-library/react-native-snap-carousel/releases)

## 属性

详情查看[react-native-snap-carousel 官方文档](https://github.com/meliorence/react-native-snap-carousel)

如下是已验证接口展示:

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type                       | Default                                               | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------- | ----------------------------------------------------- | -------- | ----------------- |
| `data`                        | Array of items to loop on                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Array                      | Required                                              | All      | yes               |
| `renderItem`                  | Takes an item from data and renders it into the list. The function receives one argument `{item, index}` (see [Usage](https://github.com/meliorence/react-native-snap-carousel#usage)) and must return a React element.                                                                                                                                                                                                                                                                    | Function                   | Required                                              | All      | yes               |
| `itemWidth`                   | Width in pixels of carousel's items, **must be the same for all of them**                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | Required for horizontal carousel                      | All      | yes               |
| `sliderWidth`                 | Width in pixels of the carousel itself                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Number                     | Required for horizontal carousel                      | All      | yes               |
| `itemHeight`                  | Height in pixels of carousel's items, **must be the same for all of them**                                                                                                                                                                                                                                                                                                                                                                                                                 | Number                     | Required for vertical carousel                        | All      | yes               |
| `sliderHeight`                | Height in pixels of the carousel itself                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Number                     | Required for vertical carousel                        | All      | yes               |
| `loop`                        | Enable infinite loop mode. **:warning: It won't work if `enableSnap` has been set to `false`.**                                                                                                                                                                                                                                                                                                                                                                                            | Boolean                    | `false`                                               | All      | yes               |
| `loopClonesPerSide`           | Number of clones to append to each side of the original items. **When swiping very quickly**, the user will eventually need to pause for a quick second before the scroll is repositioned (this occurs when the end of the set is reached). By increasing this number, the user will be able to scroll more slides before having to stop; but you'll also load more items in memory. This is a trade-off between optimal user experience and performance.                                  | Number                     | `3`                                                   | All      | yes               |
| `autoplay`                    | Trigger autoplay on mount. If you enable autoplay, we recommend you to set `enableMomentum` to `false` (default) and `lockScrollWhileSnapping` to `true`; this will enhance user experience a bit.                                                                                                                                                                                                                                                                                         | Boolean                    | `false`                                               | All      | yes               |
| `autoplayDelay`               | Delay before enabling autoplay on startup & after releasing the touch                                                                                                                                                                                                                                                                                                                                                                                                                      | Number                     | `1000`                                                | All      | yes               |
| `autoplayInterval`            | Delay in ms until navigating to the next item                                                                                                                                                                                                                                                                                                                                                                                                                                              | Number                     | `3000`                                                | All      | yes               |
| `layout`                      | Define the way items are rendered and animated. Possible values are `'default'`, `'stack'` and `'tinder'`. :warning: **Setting this prop to either `'stack'` or `'tinder'` will activate `useScrollView` [to prevent rendering bugs with `FlatList`](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#caveats). Therefore, those layouts won't be suited if you have a large data set since all items are going to be rendered upfront.** | String                     | `'default'`                                           | All      | yes               |
| `containerCustomStyle`        | Optional styles for Scrollview's global wrapper                                                                                                                                                                                                                                                                                                                                                                                                                                            | View Style Object          | `{}`                                                  | All      | yes               |
| `contentContainerCustomStyle` | Optional styles for Scrollview's items container                                                                                                                                                                                                                                                                                                                                                                                                                                           | View Style Object          | `{}`                                                  | All      | yes               |
| `inactiveSlideOpacity`        | Value of the opacity effect applied to inactive slides                                                                                                                                                                                                                                                                                                                                                                                                                                     | Number                     | `0.7`                                                 | All      | yes               |
| `inactiveSlideScale`          | Value of the 'scale' transform applied to inactive slides                                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | `0.9`                                                 | All      | yes               |
| `layoutCardOffset`            | Use to increase or decrease the default card offset in both 'stack' and 'tinder' layouts.                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | `18` for the 'stack' layout, `9` for the 'tinder' one | All      | yes               |
| `slideStyle`                  | Optional style for each item's container (the one whose scale and opacity are animated)                                                                                                                                                                                                                                                                                                                                                                                                    | Animated View Style Object | `{}`                                                  | All      | yes               |

### 回调

| Prop                             | Description                                                                        | Type     | Default     | latform | HarmonyOS Support |
| -------------------------------- | ---------------------------------------------------------------------------------- | -------- | ----------- | ------- | ----------------- |
| `onLayout(event)`                | Exposed `View` callback; invoked on mount and layout changes                       | Function | `undefined` | All     | yes               |
| `onScroll(event)`                | Exposed `ScrollView` callback; fired while scrolling                               | Function | `undefined` | All     | yes               |
| `onBeforeSnapToItem(slideIndex)` | Callback fired when the new active item has been determined, before snapping to it | Function | `undefined` | All     | yes               |
| `onSnapToItem(slideIndex)`       | Callback fired after snapping to an item                                           | Function | `undefined` | All     | yes               |

## 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2FShopify%2Fflash-list%2Fblob%2Fmain%2FLICENSE.md) ，请自由地享受和参与开源。
