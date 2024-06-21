<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-nested-scroll-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cesardeazevedo/react-native-nested-scroll-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cesardeazevedo/react-native-nested-scroll-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [! TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-nested-scroll-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-nested-scroll-view Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [! TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-nested-scroll-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-nested-scroll-view@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [! WARNING] 使用时 import 的库名不变。

```js
import {
  StyleSheet,
  Text,
  StatusBar,
  Button,
  View
} from 'react-native';
import React, {
  useRef
} from 'react';

import NestedScrollView from 'react-native-nested-scroll-view';

const NestedScrollViewDemo = () => {
  const scrollViewRef = useRef();

  const scrollToSpecificCoordinate = () => {
    scrollViewRef.current?.scrollTo({
      x: 300,
      y: 500,
      animated: true
    })
  };

  return ( <
    View style = {
      styles.container
    } >
    <
    NestedScrollView ref = {
      scrollViewRef
    }
    style = {
      styles.scrollView
    }
    contentContainerStyle = {
      {
        flexGrow: 1
      }
    } >
    <
    Text style = {
      styles.text
    } >
    A component that encapsulates the platform 's ScrollView, while also integrating a touch-locked "responder" system.
    Keep in mind that the ScrollView must have a definite height in order
    for it to work,
    because what it actually does is pack a series of sub - components of indeterminate height into a container with a definite height(via scrolling).To give a ScrollView a definite height, either set the height to it directly(not recommended), or make sure that all parent containers have a definite height.Generally speaking, we will set the ScrollView to automatically fill the empty space of the parent container, but only
    if all the parent containers themselves are also flex or have a height specified, otherwise it will not scroll properly,
    and you can use the Element Viewer to find out which layer is the correct height.flex: 1 Other responders inside ScrollView can 't yet prevent ScrollView from becoming a responder itself. < /
    Text > <
    /NestedScrollView> <
    View style = {
      {
        justifyContent: 'center',
        alignItems: 'center'
      }
    } >
    <
    Button title = "滚动到特定坐标"
    onPress = {
      scrollToSpecificCoordinate
    }
    /> < /
    View > <
    /View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: StatusBar.currentHeight,
    paddingBottom: 40
  },
  scrollView: {
    backgroundColor: 'pink',
    marginHorizontal: 20,
  },
  text: {
    fontSize: 42,
  },
});

export default NestedScrollViewDemo;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-nested-scroll-view Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases)

本文档内容基于以下版本验证通过：

RNOH: 0.72.23; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio: 5.0.3.27; ROM: 3.0.0.19; 

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

常用属性如下：

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| contentContainerStyle  | 设置滚动视图内容容器的样式.  | ViewStyleProp  | no       | Android/IOS  | yes                |
| disableIntervalMomentum  | 如果为 true，则无论手势有多快，滚动视图都会停止在下一个索引处（相对于释放时的滚动位置）| boolean | no | Android/IOS | yes  |
| decelerationRate  | 设置滚动减速速率。| ('fast' 或 'normal' 或 number)  | no | Android/IOS  | yes  |
| horizontal  | 指定滚动视图是否为水平方向，默认为垂直方向。 | boolean  | no   | Android/IOS  | yes                |
| invertStickyHeaders  | 粘性标题是否应粘在 ScrollView 的底部而不是顶部。| boolean  | no       | Android/IOS  | yes                |
| keyboardDismissMode  | 设置键盘消失模式，可选值为"none"、“interactive"和"on-drag” | string  | no       | Android/IOS  | yes                |
| keyboardShouldPersistTaps  | 设置点击输入框以外的区域时键盘是否消失，可选值为"never"、“always"和"handled”| ('always' 或 'never' 或 'handled' 或 true 或 false)  | no | Android/IOS  | yes |
| onMomentumScrollBegin  | 开始惯性滚动时触发的回调函数 | (event: ScrollEvent) => void  | no   | Android/IOS  | yes    |
| onMomentumScrollEnd  | 结束惯性滚动时触发的回调函数 | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onScroll  | 滚动时触发的回调函数   | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onScrollBeginDrag  | 开始拖拽滚动视图时触发的回调函数 | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onScrollEndDrag  | 结束拖拽滚动视图时触发的回调函数  | (event: ScrollEvent) => void  | no       | Android/IOS  | yes                |
| onContentSizeChange  | 当 ScrollView 的可滚动内容视图发生变化时调用，处理函数传递内容宽度和内容高度作为参数   | (contentWidth: number, contentHeight: number) => void  | no       | Android/IOS  | yes                |
| pagingEnabled  | 当值为 true 时，滚动条会停在滚动视图的尺寸的整数倍位置  | boolean  | no | Android/IOS | yes               |
| scrollEnabled  | 当值为 false 的时候，内容不能滚动，默认值为 true  | boolean | no | Android/IOS | yes               |
| showsVerticalScrollIndicator  | 当此属性为 true 的时候，显示一个垂直方向的滚动条 | boolean  | no | Android/IOS | yes               |
| stickyHeaderIndices  | 一个子视图下标的数组，用于决定哪些成员会在滚动之后固定在屏幕顶端   | $ReadOnlyArray<number>  | no | Android/IOS | yes               |
| snapToInterval  | 当设置了此属性时，会让滚动视图滚动停止后，停止在snapToInterval的倍数的位置   | number  | no | Android/IOS | yes               |
| snapToOffsets  | 会使滚动视图停止在定义的偏移处。这可用于对长度小于滚动视图的各种大小的子项进行分页  | $ReadOnlyArray<number>  | no | Android/IOS | yes               |
| snapToStart  | 与 snapToOffsets 结合使用。默认情况下，列表的开头算作捕捉偏移。   | boolean  | no | Android/IOS | yes               |
| snapToEnd  | 与 snapToOffsets 结合使用。默认情况下，列表末尾算作捕捉偏移         | boolean  | no | Android/IOS | yes               |
| removeClippedSubviews  | 当此属性为 true 时，屏幕之外的子视图（子视图的overflow样式需要设为hidden）会被移除         | boolean  | no | Android/IOS | yes               |
| refreshControl  | 用于为 ScrollView 提供下拉刷新功能。只能用于垂直视图，即horizontal不能为true | React. Element<any>  | no | Android/IOS | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scrollTo  | 该方法用于滚动到指定位置。可以通过x和y参数指定滚动的偏移量，animated参数用于指定是否使用动画效果。| function  | no       | Android/IOS  | yes        |
| scrollToEnd  | 该方法用于滚动到内容的末尾。可以通过animated参数指定是否使用动画效果。| function  | no       | Android/IOS  | yes                |
| flashScrollIndicators  | 该方法用于显示滚动指示器，通常在需要提醒用户可以滚动时使用。| function  | no       | Android/IOS  | yes                |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/cesardeazevedo/react-native-nested-scroll-view/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->