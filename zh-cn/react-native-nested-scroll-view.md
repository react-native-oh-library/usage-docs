> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-nested-scroll-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-nested-scroll-view Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

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

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, ScrollView, Text, StyleSheet } from 'react-native';
import NestedScrollView from 'react-native-nested-scroll-view';

const NestedScrollViewExample = () => {
  return (
    <NestedScrollView style={{ flex: 1 }}>
      <ScrollView contentContainerStyle={styles.scrollViewContent}>
        {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map((item) => (
          <View key={item} style={styles.itemContainer}>
            <Text style={styles.itemTitle}>Item {item}</Text>
            <ScrollView horizontal showsHorizontalScrollIndicator={false}>
              {[1, 2, 3, 4, 5, 6, 7, 8, 9, 10].map((subItem) => (
                <View key={subItem} style={styles.subItem}>
                  <Text>content {subItem}</Text>
                </View>
              ))}
            </ScrollView>
          </View>
        ))}
      </ScrollView>
    </NestedScrollView>
  );
};

const styles = StyleSheet.create({
  scrollViewContent: {
    paddingVertical: 20,
    paddingHorizontal: 10,
  },
  itemContainer: {
    marginBottom: 20,
    padding: 10,
    backgroundColor: '#f0f0f0',
    borderRadius: 10,
  },
  itemTitle: {
    fontSize: 18,
    fontWeight: 'bold',
    marginBottom: 10,
  },
  subItem: {
    width: 100,
    height: 100,
    backgroundColor: '#b0e0e6',
    justifyContent: 'center',
    alignItems: 'center',
    marginHorizontal: 5,
  },
});

export default NestedScrollViewExample;
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-nested-scroll-view Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases)

## 属性

Android的ScrollView并不支持像iOS的ScrollView那样的嵌套滚动，在React Native中直接使用原生的ScrollView实现嵌套滚动时，会出现一些滚动上的问题，例如嵌套滚动不流畅或无法正确响应滚动事件等，因此Android使用react-native-nested-scroll-view来解决嵌套滚动的问题；而iOS使用的是React Native中的ScrollView来实现嵌套滚动，HarmonyOS与iOS保持一致，接受所有[React Native ScrollView](https://reactnative.dev/docs/scrollview#props) 组件的Props

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

Android的ScrollView并不支持像iOS的ScrollView那样的嵌套滚动，在React Native中直接使用原生的ScrollView实现嵌套滚动时，会出现一些滚动上的问题，例如嵌套滚动不流畅或无法正确响应滚动事件等，因此Android使用react-native-nested-scroll-view来解决嵌套滚动的问题；而iOS使用的是React Native中的ScrollView来实现嵌套滚动，HarmonyOS与iOS保持一致，接受所有[React Native ScrollView](https://reactnative.dev/docs/scrollview#methods) 组件的Methods

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
