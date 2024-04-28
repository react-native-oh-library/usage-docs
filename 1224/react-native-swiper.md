> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-swiper</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/leecade/react-native-swiper/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!tip] [Github 地址](https://github.com/leecade/react-native-swiper)

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
import React, { Component } from 'react'
import { AppRegistry, StyleSheet, Text, View } from 'react-native'

import Swiper from 'react-native-swiper'

const styles = StyleSheet.create({
  wrapper: {},
  slide1: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#9DD6EB'
  },
  slide2: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#97CAE5'
  },
  slide3: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#92BBD9'
  },
  text: {
    color: '#fff',
    fontSize: 30,
    fontWeight: 'bold'
  }
})

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
    )
  }
}

AppRegistry.registerComponent('myproject', () => SwiperComponent)
```

### 兼容性

在下述版本验证通过:
RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

### 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### basics

| Prop           |     Default     |   Type   | Description                                                  | platform | HarmonyOS Support | remark |
| :------------- | :-------------: | :------: | :----------------------------------------------------------- | -------- | ----------------- | ------ |
| horizontal     |      true       |  `bool`  | If `true`, the scroll view's children are arranged horizontally in a row instead of vertically in a column. | All      | YES               | --     |
| loop           |      true       |  `bool`  | Set to `false` to disable continuous loop mode.              | All      | YES               | --     |
| index          |        0        | `number` | Index number of initial slide.                               | All      | YES               | --     |
| showsButtons   |      false      |  `bool`  | Set to `true` make control buttons visible.                  | All      | YES               | --     |
| autoplay       |      false      |  `bool`  | Set to `true` enable auto play mode.                         | All      | YES               | --     |
| onIndexChanged | (index) => null |  `func`  | Called with the new index when the user swiped               | All      | YES               | --     |

#### Custom basic style & content

| Prop              |         Default         |   Type    | Description                                                  | platform | HarmonyOS Support | remark |
| :---------------- | :---------------------: | :-------: | :----------------------------------------------------------- | -------- | ----------------- | ------ |
| width             |            -            | `number`  | If no specify default enable fullscreen mode by `flex: 1`.   | All      | YES               | --     |
| height            |            -            | `number`  | If no specify default fullscreen mode by `flex: 1`.          | All      | YES               | --     |
| style             |          {...}          |  `style`  | See default style in source.                                 | All      | YES               | --     |
| containerStyle    |          {...}          |  `style`  | See default container style in source.                       | All      | YES               | --     |
| loadMinimal       |          false          |  `bool`   | Only load current index slide , `loadMinimalSize` slides before and after. | All      | YES               | --     |
| loadMinimalSize   |            1            | `number`  | see `loadMinimal`                                            | All      | YES               | --     |
| loadMinimalLoader | `<ActivityIndicator />` | `element` | Custom loader to display when slides aren't loaded           | All      | YES               | --     |

#### Pagination

| Prop             |                           Default                            |    Type    | Description                                                  | platform | HarmonyOS Support | remark |
| :--------------- | :----------------------------------------------------------: | :--------: | :----------------------------------------------------------- | -------- | ----------------- | ------ |
| showsPagination  |                             true                             |   `bool`   | Set to `true` make pagination visible.                       | All      | YES               | --     |
| paginationStyle  |                            {...}                             |  `style`   | Custom styles will merge with the default styles.            | All      | YES               | --     |
| renderPagination |                              -                               | `function` | Complete control how to render pagination with three params (`index`, `total`, `context`) ref to `this.state.index` / `this.state.total` / `this`, For example: show numbers instead of dots. | All      | YES               | --     |
| dot              | `<View style={{backgroundColor:'rgba(0,0,0,.2)', width: 8, height: 8,borderRadius: 4, marginLeft: 3, marginRight: 3, marginTop: 3, marginBottom: 3,}} />` | `element`  | Allow custom the dot element.                                | All      | YES               | --     |
| activeDot        | `<View style={{backgroundColor: '#007aff', width: 8, height: 8, borderRadius: 4, marginLeft: 3, marginRight: 3, marginTop: 3, marginBottom: 3,}} />` | `element`  | Allow custom the active-dot element.                         | All      | YES               | --     |
| dotStyle         |                              -                               |  `object`  | Allow custom the dot element.                                | All      | YES               | --     |
| dotColor         |                              -                               |  `string`  | Allow custom the dot element.                                | All      | YES               | --     |
| activeDotColor   |                              -                               |  `string`  | Allow custom the active-dot element.                         | All      | YES               | --     |
| activeDotStyle   |                              -                               |  `object`  | Allow custom the active-dot element.                         | All      | YES               | --     |

#### Autoplay

| Prop              | Default |   Type   | Description                                      | platform | HarmonyOS Support | remark |
| :---------------- | :-----: | :------: | :----------------------------------------------- | -------- | ----------------- | ------ |
| autoplay          |  true   |  `bool`  | Set to `true` enable auto play mode.             | All      | YES               | --     |
| autoplayTimeout   |   2.5   | `number` | Delay between auto play transitions (in second). | All      | YES               | --     |
| autoplayDirection |  true   |  `bool`  | Cycle direction control.                         | All      | YES               | --     |

#### Control buttons

| Prop               |                           Default                            |   Type    | Description                                 | platform | HarmonyOS Support | remark |
| :----------------- | :----------------------------------------------------------: | :-------: | :------------------------------------------ | -------- | ----------------- | ------ |
| showsButtons       |                             true                             |  `bool`   | Set to `true` make control buttons visible. | All      | YES               | --     |
| buttonWrapperStyle | `{backgroundColor: 'transparent', flexDirection: 'row', position: 'absolute', top: 0, left: 0, flex: 1, paddingHorizontal: 10, paddingVertical: 10, justifyContent: 'space-between', alignItems: 'center'}` |  `style`  | Custom styles.                              | All      | YES               | --     |
| nextButton         |          `<Text style={styles.buttonText}>›</Text>`          | `element` | Allow custom the next button.               | All      | YES               | --     |
| prevButton         |          `<Text style={styles.buttonText}>‹</Text>`          | `element` | Allow custom the prev button.               | All      | YES               | --     |

#### Props of Children

| Prop  |               Default                |   Type    | Description                                                  | platform | HarmonyOS Support | remark |
| :---- | :----------------------------------: | :-------: | :----------------------------------------------------------- | -------- | ----------------- | ------ |
| style |                {...}                 |  `style`  | Custom styles will merge with the default styles.            | All      | YES               | --     |
| title | {<Text numberOfLines={1}>...</Text>} | `element` | If this parameter is not specified, will not render the title. | All      | YES               | --     |

#### Basic props of `<ScrollView />`

| Prop                             | Default |  Type  | Description                                                  | platform | HarmonyOS Support | remark |
| :------------------------------- | :-----: | :----: | :----------------------------------------------------------- | -------- | ----------------- | ----------------- |
| horizontal                       |  true   | `bool` | If `true`, the scroll view's children are arranged horizontally in a row instead of vertically in a column. | All      | YES               | --          |
| pagingEnabled                    |  true   | `bool` | If true, the scroll view stops on multiples of the scroll view's size when scrolling. This can be used for horizontal pagination. | All      | YES               | --          |
| showsHorizontalScrollIndicator   |  false  | `bool` | Set to `true` if you want to show horizontal scroll bar.     | All      | YES               | --          |
| showsVerticalScrollIndicator     |  false  | `bool` | Set to `true` if you want to show vertical scroll bar.       | All      | YES               | --          |
| bounces                          |  false  | `bool` | If `true`, the scroll view bounces when it reaches the end of the content if the content is larger then the scroll view along the axis of the scroll direction. If `false`, it disables all bouncing even if the alwaysBounce\* props are true. | All      | YES               | --          |
| scrollsToTop                     |  false  | `bool` | If true, the scroll view scrolls to top when the status bar is tapped. | All      | NO             | 组件属性继承RNOH scrollview,当前RNOH中的scrollsToTop暂时不支持 |
| removeClippedSubviews            |  true   | `bool` | If true, offscreen child views (whose overflow value is hidden) are removed from their native backing superview when offscreen. This canimprove scrolling performance on long lists. | All      | NO             | 组件属性继承RNOH scrollview,当前RNOH中的removeClippedSubviews暂时不支持 |
| automaticallyAdjustContentInsets |  false  | `bool` | Set to `true` if you need adjust content insets automation.  | All      | NO             | 组件属性继承RNOH scrollview,当前RNOH中的automaticallyAdjustContentInsets暂时不支持 |
| scrollEnabled                    |  true   | `bool` | Enables/Disables swiping                                     | All      | YES               | --      |

> @see: http://facebook.github.io/react-native/docs/scrollview.html

#### Supported ScrollResponder

| Prop                |          Params           |    Type    | Description                                                 | platform | HarmonyOS Support | remark |
| :------------------ | :-----------------------: | :--------: | :---------------------------------------------------------- | -------- | ----------------- | ------ |
| onScrollBeginDrag   | `e` / `state` / `context` | `function` | When animation begins after letting up                      | All      | YES               | --     |
| onMomentumScrollEnd | `e` / `state` / `context` | `function` | Makes no sense why this occurs first during bounce          | All      | YES               | --     |
| onTouchStartCapture | `e` / `state` / `context` | `function` | Immediately after `onMomentumScrollEnd`                     | All      | YES               | --     |
| onTouchStart        | `e` / `state` / `context` | `function` | Same, but bubble phase                                      | All      | YES               | --     |
| onTouchEnd          | `e` / `state` / `context` | `function` | You could hold the touch start for a long time              | All      | YES               | --     |
| onResponderRelease  | `e` / `state` / `context` | `function` | When lifting up - you could pause forever before \* lifting | All      | YES               | --     |

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

> More ScrollResponder info, see: https://github.com/facebook/react-native/blob/master/Libraries/Components/ScrollResponder.js

### 方法

#### scrollBy(index, animated)

| Name     |   Type   |   default   | Description  | platform | HarmonyOS Support | remark |
| :------- | :------: | :---------: | :----------- | -------- | ----------------- | ------ |
| index    | `number` | `undefined` | offset index | All      | YES               | --     |
| animated |  `bool`  |   `true`    | offset index | All      | YES               | --     |

### 遗留问题

- [ ]    组件属性继承RNOH scrollview,当前RNOH中的scrollsToTop暂时不支持
- [ ] 组件属性继承RNOH scrollview,当前RNOH中的removeClippedSubviews暂时不支持
- [ ]   组件属性继承RNOH scrollview,当前RNOH中的automaticallyAdjustContentInsets暂时不支持

### 其他

### 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/leecade/react-native-swiper/blob/master/LICENSE) ，请自由地享受和参与开源。
