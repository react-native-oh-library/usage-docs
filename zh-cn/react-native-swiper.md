> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-swiper</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/leecade/react-native-swiper/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/leecade/react-native-swiper/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/leecade/react-native-swiper)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm i react-native-swiper@1.6.0 --save
```

#### **yarn**

```bash
yarn add react-native-swiper@1.6.0
```

<!-- tabs:end -->

快速使用：

```js
import React, { Component } from "react";
import { AppRegistry, StyleSheet, Text, View } from "react-native";

import Swiper from "react-native-swiper";

const styles = StyleSheet.create({
  wrapper: {},
  slide1: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#9DD6EB",
  },
  slide2: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#97CAE5",
  },
  slide3: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
    backgroundColor: "#92BBD9",
  },
  text: {
    color: "#fff",
    fontSize: 30,
    fontWeight: "bold",
  },
});

export default class SwiperComponent extends Component {
  render() {
    return (
      <Swiper style={styles.wrapper} showsButtons={true}>
        <View style={styles.slide1}>
          <Text style={styles.text}>Hello Swiper</Text>
        </View>
        <View style={styles.slide2}>
          <Text style={styles.text}>Beautiful</Text>
        </View>
        <View style={styles.slide3}>
          <Text style={styles.text}>And simple</Text>
        </View>
      </Swiper>
    );
  }
}

AppRegistry.registerComponent("myproject", () => SwiperComponent);
```

## 约束与限制

### 兼容性

在以下版本验证通过

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### basics

| Name           | Description                                                  |   Type   |     Default     | platform | HarmonyOS Support |
| :------------- | ------------------------------------------------------------ | :------: | :-------------: | -------- | ----------------- |
| horizontal     | If `true`, the scroll view's children are arranged horizontally in a row instead of vertically in a column. |  `bool`  |      true       | All      | YES               |
| loop           | Set to `false` to disable continuous loop mode.              |  `bool`  |      true       | All      | YES               |
| index          | Index number of initial slide.                               | `number` |        0        | All      | YES               |
| showsButtons   | Set to `true` make control buttons visible.                  |  `bool`  |      false      | All      | YES               |
| autoplay       | Set to `true` enable auto play mode.                         |  `bool`  |      false      | All      | YES               |
| onIndexChanged | Called with the new index when the user swiped               |  `func`  | (index) => null | All      | YES               |

#### Custom basic style & content

| Name              | Description                                                  |   Type    |         Default         | platform | HarmonyOS Support |
| :---------------- | :----------------------------------------------------------- | :-------: | :---------------------: | -------- | ----------------- |
| width             | If no specify default enable fullscreen mode by `flex: 1`.   | `number`  |            -            | All      | YES               |
| height            | If no specify default fullscreen mode by `flex: 1`.          | `number`  |            -            | All      | YES               |
| style             | See default style in source.                                 |  `style`  |          {...}          | All      | YES               |
| containerStyle    | See default container style in source.                       |  `style`  |          {...}          | All      | YES               |
| loadMinimal       | Only load current index slide , `loadMinimalSize` slides before and after. |  `bool`   |          false          | All      | YES               |
| loadMinimalSize   | see `loadMinimal`                                            | `number`  |            1            | All      | YES               |
| loadMinimalLoader | Custom loader to display when slides aren't loaded           | `element` | `<ActivityIndicator />` | All      | YES               |

#### Pagination

| Name             | Description                                                  |    Type    |                           Default                            | platform | HarmonyOS Support |
| :--------------- | :----------------------------------------------------------- | :--------: | :----------------------------------------------------------: | -------- | ----------------- |
| showsPagination  | Set to `true` make pagination visible.                       |   `bool`   |                             true                             | All      | YES               |
| paginationStyle  | Custom styles will merge with the default styles.            |  `style`   |                            {...}                             | All      | YES               |
| renderPagination | Complete control how to render pagination with three params (`index`, `total`, `context`) ref to `this.state.index` / `this.state.total` / `this`, For example: show numbers instead of dots. | `function` |                              -                               | All      | YES               |
| dot              | Allow custom the dot element.                                | `element`  | `<View style={{backgroundColor:'rgba(0,0,0,.2)', width: 8, height: 8,borderRadius: 4, marginLeft: 3, marginRight: 3, marginTop: 3, marginBottom: 3,}} />` | All      | YES               |
| activeDot        | Allow custom the active-dot element.                         | `element`  | `<View style={{backgroundColor: '#007aff', width: 8, height: 8, borderRadius: 4, marginLeft: 3, marginRight: 3, marginTop: 3, marginBottom: 3,}} />` | All      | YES               |
| dotStyle         | Allow custom the dot element.                                |  `object`  |                              -                               | All      | YES               |
| dotColor         | Allow custom the dot element.                                |  `string`  |                              -                               | All      | YES               |
| activeDotColor   | Allow custom the active-dot element.                         |  `string`  |                              -                               | All      | YES               |
| activeDotStyle   | Allow custom the active-dot element.                         |  `object`  |                              -                               | All      | YES               |

#### Autoplay

| Name              | Description                                      |   Type   | Default | platform | HarmonyOS Support |
| :---------------- | :----------------------------------------------- | :------: | :-----: | -------- | ----------------- |
| autoplay          | Set to `true` enable auto play mode.             |  `bool`  |  true   | All      | YES               |
| autoplayTimeout   | Delay between auto play transitions (in second). | `number` |   2.5   | All      | YES               |
| autoplayDirection | Cycle direction control.                         |  `bool`  |  true   | All      | YES               |

#### Control buttons

| Prop               |                                                                                                   Default                                                                                                   |   Type    | Description                                 | platform | HarmonyOS Support | remark |
| :----------------- | :---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-------: | :------------------------------------------ | -------- | ----------------- | ------ |
| showsButtons       |                                                                                                    true                                                                                                     |  `bool`   | Set to `true` make control buttons visible. | All      | YES               | --     |
| buttonWrapperStyle | `{backgroundColor: 'transparent', flexDirection: 'row', position: 'absolute', top: 0, left: 0, flex: 1, paddingHorizontal: 10, paddingVertical: 10, justifyContent: 'space-between', alignItems: 'center'}` |  `style`  | Custom styles.                              | All      | YES               | --     |
| nextButton         |                                                                                 `<Text style={styles.buttonText}>›</Text>`                                                                                  | `element` | Allow custom the next button.               | All      | YES               | --     |
| prevButton         |                                                                                 `<Text style={styles.buttonText}>‹</Text>`                                                                                  | `element` | Allow custom the prev button.               | All      | YES               | --     |

#### Props of Children

| Name  | Description                                                  |   Type    |               Default                | platform | HarmonyOS Support |
| :---- | :----------------------------------------------------------- | :-------: | :----------------------------------: | -------- | ----------------- |
| style | Custom styles will merge with the default styles.            |  `style`  |                {...}                 | All      | YES               |
| title | If this parameter is not specified, will not render the title. | `element` | {<Text numberOfLines={1}>...</Text>} | All      | YES               |

#### Basic props of `<ScrollView />`

| Name                             | Description                                                  |  Type  | Default | platform | HarmonyOS Support | remark                                                       |
| :------------------------------- | :----------------------------------------------------------- | :----: | :-----: | -------- | ----------------- | ------------------------------------------------------------ |
| horizontal                       | If `true`, the scroll view's children are arranged horizontally in a row instead of vertically in a column. | `bool` |  true   | All      | YES               | --                                                           |
| pagingEnabled                    | If true, the scroll view stops on multiples of the scroll view's size when scrolling. This can be used for horizontal pagination. | `bool` |  true   | All      | YES               | --                                                           |
| showsHorizontalScrollIndicator   | Set to `true` if you want to show horizontal scroll bar.     | `bool` |  false  | All      | YES               | --                                                           |
| showsVerticalScrollIndicator     | Set to `true` if you want to show vertical scroll bar.       | `bool` |  false  | All      | YES               | --                                                           |
| bounces                          | If `true`, the scroll view bounces when it reaches the end of the content if the content is larger then the scroll view along the axis of the scroll direction. If `false`, it disables all bouncing even if the alwaysBounce\* props are true. | `bool` |  false  | All      | YES               | --                                                           |
| scrollsToTop                     | If true, the scroll view scrolls to top when the status bar is tapped. | `bool` |  false  | All      | NO                | 组件属性继承RNOH scrollview,当前RNOH中的scrollsToTop暂时不支持 |
| removeClippedSubviews            | If true, offscreen child views (whose overflow value is hidden) are removed from their native backing superview when offscreen. This canimprove scrolling performance on long lists. | `bool` |  true   | All      | NO                | 组件属性继承RNOH scrollview,当前RNOH中的removeClippedSubviews暂时不支持 |
| automaticallyAdjustContentInsets | Set to `true` if you need adjust content insets automation.  | `bool` |  false  | All      | NO                | 组件属性继承RNOH scrollview,当前RNOH中的automaticallyAdjustContentInsets暂时不支持 |
| scrollEnabled                    | Enables/Disables swiping                                     | `bool` |  true   | All      | YES               | --                                                           |

> @see: http://facebook.github.io/react-native/docs/scrollview.html

#### Supported ScrollResponder

| Name                | Description                                                 |    Type    |          Params           | platform | HarmonyOS Support |
| :------------------ | :---------------------------------------------------------- | :--------: | :-----------------------: | -------- | ----------------- |
| onScrollBeginDrag   | When animation begins after letting up                      | `function` | `e` / `state` / `context` | All      | YES               |
| onMomentumScrollEnd | Makes no sense why this occurs first during bounce          | `function` | `e` / `state` / `context` | All      | YES               |
| onTouchStartCapture | Immediately after `onMomentumScrollEnd`                     | `function` | `e` / `state` / `context` | All      | YES               |
| onTouchStart        | Same, but bubble phase                                      | `function` | `e` / `state` / `context` | All      | YES               |
| onTouchEnd          | You could hold the touch start for a long time              | `function` | `e` / `state` / `context` | All      | YES               |
| onResponderRelease  | When lifting up - you could pause forever before \* lifting | `function` | `e` / `state` / `context` | All      | YES               |

> Note: each ScrollResponder be injected with two params: `state` and `context`, you can get `state` and `context`(ref to swiper's `this`) from params, for example:

```jsx
var swiper = React.createClass({
  _onMomentumScrollEnd: function (e, state, context) {
    console.log(state, context.state)
  },
  render: function() {
    return (
      <Swiper style={styles.wrapper}
      onMomentumScrollEnd ={this._onMomentumScrollEnd}
     ...
      </Swiper>
    )
  }
})
```

### 方法

#### scrollBy(index, animated)

| Name     | Description  |   Type   |   default   | platform | HarmonyOS Support |
| :------- | :----------- | :------: | :---------: | -------- | ----------------- |
| index    | offset index | `number` | `undefined` | All      | YES               |
| animated | offset index |  `bool`  |   `true`    | All      | YES               |

### 遗留问题

- [ ] 组件属性继承RNOH scrollview,当前RNOH中的scrollsToTop暂时不支持
- [ ] 组件属性继承RNOH scrollview,当前RNOH中的removeClippedSubviews暂时不支持
- [ ] 组件属性继承RNOH scrollview,当前RNOH中的automaticallyAdjustContentInsets暂时不支持
- [ ] 组件轮播图RNOH版本为0.72.13暂时有不居中问题，在RNOH版本为0.72.19上解决

### 其他

### 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/leecade/react-native-swiper/blob/master/LICENSE) ，请自由地享受和参与开源。
