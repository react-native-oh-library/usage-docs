> Template version: v0.2.2

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-nested-scroll-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-nested-scroll-view Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases)

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

### Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-nested-scroll-view Releases](https://github.com/react-native-oh-library/react-native-nested-scroll-view/releases)

## Properties 

Android的ScrollView并不支持像iOS的ScrollView那样的嵌套滚动，在React Native中直接使用原生的ScrollView实现嵌套滚动时，会出现一些滚动上的问题，例如嵌套滚动不流畅或无法正确响应滚动事件等，因此Android使用react-native-nested-scroll-view来解决嵌套滚动的问题；而iOS使用的是React Native中的ScrollView来实现嵌套滚动，HarmonyOS与iOS保持一致，接受所有[React Native ScrollView](https://reactnative.dev/docs/scrollview#props) 组件的Props

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| scrollTo  | 该方法用于滚动到指定位置。可以通过x和y参数指定滚动的偏移量，animated参数用于指定是否使用动画效果。| function  | no       | Android/IOS  | yes        |
| scrollToEnd  | 该方法用于滚动到内容的末尾。可以通过animated参数指定是否使用动画效果。| function  | no       | Android/IOS  | yes                |
| flashScrollIndicators  | 该方法用于显示滚动指示器，通常在需要提醒用户可以滚动时使用。| function  | no       | Android/IOS  | yes                |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/cesardeazevedo/react-native-nested-scroll-view/blob/master/LICENSE).
