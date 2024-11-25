> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-snap-carousel</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/meliorence/react-native-snap-carousel">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20||%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/meliorence/react-native-snap-carousel/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-snap-carousel)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-snap-carousel Releases](https://github.com/react-native-oh-library/react-native-snap-carousel/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-snap-carousel
```
#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-snap-carousel
```
<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text, Image, StyleSheet } from "react-native";
import Carousel from "react-native-snap-carousel";

export default function SnapCarouselExample(): JSX.Element {
  const ENTRIES1 = [
    {
      title: "Beautiful and dramatic Antelope Canyon",
      subtitle: "Lorem ipsum dolor sit amet et nuncat mergitur",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-1.png?la=zh",
    },
    {
      title: "Earlier this morning, NYC",
      subtitle: "Lorem ipsum dolor sit amet",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-2.jpg?la=zh",
    },
    {
      title: "White Pocket Sunset",
      subtitle: "Lorem ipsum dolor sit amet et nuncat ",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-1.png?la=zh",
    },
    {
      title: "Acrocorinth, Greece",
      subtitle: "Lorem ipsum dolor sit amet et nuncat mergitur",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-2.jpg?la=zh",
    },
    {
      title: "The lone tree, majestic landscape of New Zealand",
      subtitle: "Lorem ipsum dolor sit amet",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-1.png?la=zh",
    },
    {
      title: "Middle Earth, Germany",
      subtitle: "Lorem ipsum dolor sit amet",
      url: "https://www-file.huawei.com/-/media/corp2020/images/tech4all/cases1/12/white-headed-langur-en-2.jpg?la=zh",
    },
  ];

  const _renderItem = ({ item, index }: any) => {
    return (
      <View>
        <Image source={{ uri: item.url }} style={styles.image} />
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
  image: {
    resizeMode: 'cover',
    borderTopLeftRadius: 8,
    borderTopRightRadius: 8,
    width: 250,
    height: 300
  }
});
```
## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-snap-carousel Releases](https://github.com/react-native-oh-library/react-native-snap-carousel/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                          | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | Type                       | Required                                               | Platform | HarmonyOS Support |
| ----------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------- | ----------------------------------------------------- | -------- | ----------------- |
| `data`                        | Array of items to loop on                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Array                      | yes                                              | iOS/Android      | yes               |
| `renderItem`                  | Takes an item from data and renders it into the list. The function receives one argument `{item, index}` (see [Usage](https://github.com/meliorence/react-native-snap-carousel#usage)) and must return a React element.                                                                                                                                                                                                                                                                    | Function                   | yes                                              | iOS/Android      | yes               |
| `itemWidth`                   | Width in pixels of carousel's items, **must be the same for all of them**                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | yes                      | iOS/Android      | yes               |
| `sliderWidth`                 | Width in pixels of the carousel itself                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Number                     | yes                      | iOS/Android      | yes               |
| `itemHeight`                  | Height in pixels of carousel's items, **must be the same for all of them**                                                                                                                                                                                                                                                                                                                                                                                                                 | Number                     | yes                       | iOS/Android      | yes               |
| `sliderHeight`                | Height in pixels of the carousel itself                                                                                                                                                                                                                                                                                                                                                                                                                                                    | Number                     |  yes                        | iOS/Android      | yes               |
| `loop`                        | Enable infinite loop mode. **:warning: It won't work if `enableSnap` has been set to `false`.**                                                                                                                                                                                                                                                                                                                                                                                            | Boolean                    | no                                               | iOS/Android      | yes               |
| `loopClonesPerSide`           | Number of clones to append to each side of the original items. **When swiping very quickly**, the user will eventually need to pause for a quick second before the scroll is repositioned (this occurs when the end of the set is reached). By increasing this number, the user will be able to scroll more slides before having to stop; but you'll also load more items in memory. This is a trade-off between optimal user experience and performance.                                  | Number                     | no                                                   | iOS/Android      | yes               |
| `autoplay`                    | Trigger autoplay on mount. If you enable autoplay, we recommend you to set `enableMomentum` to `false` (default) and `lockScrollWhileSnapping` to `true`; this will enhance user experience a bit.                                                                                                                                                                                                                                                                                         | Boolean                    | no                                               | iOS/Android      | yes               |
| `autoplayDelay`               | Delay before enabling autoplay on startup & after releasing the touch                                                                                                                                                                                                                                                                                                                                                                                                                      | Number                     | no                                                | iOS/Android      | yes               |
| `autoplayInterval`            | Delay in ms until navigating to the next item                                                                                                                                                                                                                                                                                                                                                                                                                                              | Number                     | no                                                | iOS/Android      | yes               |
| `layout`                      | Define the way items are rendered and animated. Possible values are `'default'`, `'stack'` and `'tinder'`. :warning: **Setting this prop to either `'stack'` or `'tinder'` will activate `useScrollView` [to prevent rendering bugs with `FlatList`](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#caveats). Therefore, those layouts won't be suited if you have a large data set since all items are going to be rendered upfront.** | String                     | no                                           | iOS/Android      | yes               |
| `containerCustomStyle`        | Optional styles for Scrollview's global wrapper                                                                                                                                                                                                                                                                                                                                                                                                                                            | View Style Object          | no                                                 | iOS/Android      | yes               |
| `contentContainerCustomStyle` | Optional styles for Scrollview's items container                                                                                                                                                                                                                                                                                                                                                                                                                                           | View Style Object          | no                                               | iOS/Android      | yes               |
| `inactiveSlideOpacity`        | Value of the opacity effect applied to inactive slides                                                                                                                                                                                                                                                                                                                                                                                                                                     | Number                     | no                                                 | iOS/Android      | yes               |
| `inactiveSlideScale`          | Value of the 'scale' transform applied to inactive slides                                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | no                                                 | iOS/Android      | yes               |
| `inactiveSlideShift`                        | Value of the 'translate' transform applied to inactive slides (see #204 or the "custom interpolations" doc for an example usage). This prop will have no effect with layouts others than the default one. on                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | Number                      | no                                           | iOS/Android      | yes               |
| `layoutCardOffset`            | Use to increase or decrease the default card offset in both 'stack' and 'tinder' layouts.                                                                                                                                                                                                                                                                                                                                                                                                  | Number                     | no | iOS/Android      | yes               |
| `slideStyle`                  | Optional style for each item's container (the one whose scale and opacity are animated)                                                                                                                                                                                                                                                                                                                                                                                                    | Animated View Style Object | no                                               | iOS/Android      | yes               |
| `scrollInterpolator`                  | Used to define custom interpolations. See [the dedicated doc](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#summary).                                                                                                                                                                                                                                                                                                                                                                                                   | Function | no                                                  | iOS/Android      | yes              |
| `slideInterpolatedStyle`                  | Used to define custom interpolations. See [the dedicated doc](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/CUSTOM_INTERPOLATIONS.md#summary).                                                                                                                                                                                                                                                                                                                                                                                                   | Function | no                                                 | iOS/Android      | yes          |
| `activeAnimationOptions`                  | Custom animation options. Note that `useNativeDriver` will be enabled by default and that opacity's easing will always be kept linear. **Setting this prop to something other than `null` will trigger custom animations and will completely change the way items are animated:** rather than having their opacity and scale interpolated based the scroll value (default behavior), they will now play the custom animation you provide as soon as they become active. **This means you cannot use props `layout`, `scrollInterpolator` or `slideInterpolatedStyle` in conjunction with `activeAnimationOptions`.**                                                                                                                                                                                                                                                                                                                                                                                          | Object | no                                                  | iOS/Android      | yes               |
| `activeAnimationType`                  | Custom [animation type:](https://reactnative.dev/docs/animated.html#configuring-animations) either `'decay'`, `'spring'` or `'timing'`. Note that it will only be applied to the scale animation since opacity's animation type will always be set to `timing` (no one wants the opacity to 'bounce' around).                                                                                                                                                                                 ``````````````                                                                                                                                                                                                            | String | no                                                  | iOS/Android      | yes               |
| `activeSlideAlignment`                  | Determine active slide's alignment relative to the carousel. Possible values are: `'start'`, `'center'` and `'end'`. **It is not recommended to use this prop in conjunction with the `layout` one.**                                                                                                                                                                                                                                                                                                                                                                                             | String | no                                                 | iOS/Android      | yes               |
| `activeSlideOffset`                  | From slider's center, minimum slide distance to be scrolled before being set to active.                                                                                                                                                                                                                                                                                                                                                                                       | Number | no                                               | iOS/Android      | yes               |
| `apparitionDelay`                  | `FlatList`'s init is a real mess, with lots of unneeded flickers and slides movement. This prop controls the delay during which the carousel will be hidden when mounted. **WARNING: on Android, using it may lead to [rendering issues](https://github.com/meliorence/react-native-snap-carousel/issues/236) (i.e. images not showing up).** Make sure to test thoroughly if you decide on using it.                                                                                                                                                                                                                                                                                                                                                                                       | Number | no                                                | iOS/Android      | yes               |
| `callbackOffsetMargin`                  | Scroll events might not be triggered often enough to get a precise measure and, therefore, to provide a reliable callback. This usually is an Android issue, which might be linked to the version of React Native you're using (see ["Unreliable callbacks"](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/KNOWN_ISSUES.md#unreliable-callbacks)). To work around this, you can define a small margin that will increase the "sweet spot"'s width. The default value should cover most cases, but **you will want to increase it if you experience missed callbacks.**                                                                                                                                                                                                                                                                                                                                                                                      | Number | no                                               | iOS/Android      | yes               |
| `enableMomentum`                  | See [momentum](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/TIPS_AND_TRICKS.md#momentum)                                                                                                                                                                                                                                                                                                                                                                             | Boolean | no                                                  | iOS/Android      | yes              |
| `enableSnap`                  | If enabled, releasing the touch will scroll to the center of the nearest/active item                                                                                                                                                                                                                                                                                                                                                                             | Boolean | no                                               | iOS/Android      | yes               |
| `firstItem`                  | Index of the first item to display. ⚠️ **Make sure to use inherited props `[getItemLayout](https://reactnative.dev/docs/flatlist#getitemlayout)` & `[initialScrollIndex](https://reactnative.dev/docs/flatlist#initialscrollindex)` if the prop doesn't seem to work.**                                                                                                                                                                                                                                                                                                                                                     | Number | no                                              | iOS/Android      | yes               |
| `hasParallaxImages`                  | Whether the carousel contains <ParallaxImage /> components or not. Required for specific data to be passed to children.                                                                                                                                                                                                                                                                                                                                                   | Boolean | no                                                 | iOS/Android      | yes               |
| `lockScrollTimeoutDuration`                  | This prop works in conjunction with `lockScrollWhileSnapping`. When scroll is locked, a timer is created in order to release the scroll if something goes wrong with the regular callback handling. **Normally, you shouldn't have to use this prop.**                                                                                                                                                                                                                                                                                                                                                | Number | no                                                 | iOS/Android      | yes               |
| `lockScrollWhileSnapping`                  | Prevent the user from swiping again while the carousel is snapping to a position. This prevents miscellaneous minor issues (inadvertently tapping an item while scrolling, stopping the scrolling animation if the carousel is tapped in the middle of a snap, clunky behavior on Android when short snapping quickly in opposite directions). The only drawback is that enabling the prop hinders the ability to swipe quickly between items as a little pause between swipes is needed. **Note that the prop won't have any effect if `enableMomentum` is set to `true`, since it would otherwise impede the natural and expected behavior.**                                                                                                                                                                                                                                                                                                                                           | Boolean | no                                               | iOS/Android      | yes               |
| `scrollEnabled`                  | When `false`, the view cannot be scrolled via touch interaction ([inherited prop](https://github.com/meliorence/react-native-snap-carousel/blob/master/doc/PROPS_METHODS_AND_GETTERS.md#inherited-props))                                                                                                                                                                                                                                                                                                                                         | Boolean | no                                                | iOS/Android      | yes               |
| `shouldOptimizeUpdates`                  | Whether to implement a `shouldComponentUpdate` strategy to minimize updates                                                                                                                                                                                                                                                                                                                                      | Boolean | no                                                 | iOS/Android      | yes               |
| `swipeThreshold`                  | Delta x when swiping to trigger the snap                                                                                                                                                                                                                                                                                                                                     | Number | no                                             | iOS/Android      | yes               |
| `useScrollView`                  | Whether to use a `ScrollView` component instead of the default `FlatList` one. The advantages are to avoid rendering issues that can arise with `FlatList` and to provide compatibility with React Native pre- `0.43`. The major drawbacks are that you won't benefit from any of `FlatList`'s advanced optimizations and that you won't be able to use either VirtualizedList or FlatList's specific props. **We recommend activating it only with a small set of slides and to test performance thoroughly in production mode**. Since version `3.7.6`, this prop also accepts a custom scroll component (see #498 for more info).                                                                                                                                                                                                                                                                                                                                    | Boolean | no                                                | iOS/Android      | yes               |
| `vertical`                  | Layout slides vertically instead of horizontally                                                                                                                                                                                                                                                                                                                                   | Boolean | no                                             | iOS/Android      | yes               |


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Prop                             | Description                                                                        | Type     | Required     | Platform | HarmonyOS Support |
| -------------------------------- | ---------------------------------------------------------------------------------- | -------- | ----------- | ------- | ----------------- |
| `onLayout(event)`                | Exposed `View` callback; invoked on mount and layout changes                       | Function | `no` | All     | yes               |
| `onScroll(event)`                | Exposed `ScrollView` callback; fired while scrolling                               | Function | `no` | All     | yes               |
| `onBeforeSnapToItem(slideIndex)` | Callback fired when the new active item has been determined, before snapping to it | Function | `no` | All     | yes               |
| `onSnapToItem(slideIndex)`       | Callback fired after snapping to an item                                           | Function | `no` | All     | yes               |

## 遗留问题
- [ ] enableMomentum属性在ios设备上效果不明显，Harmony上效果使用正常: [issue#1](https://github.com/react-native-oh-library/react-native-snap-carousel/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-snap-carousel/blob/sig/LICENSE) ，请自由地享受和参与开源。