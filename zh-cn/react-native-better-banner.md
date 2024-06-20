> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-better-banner</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/better-banner">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.isc.org/licenses/>">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/better-banner)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-better-banner Releases](https://github.com/react-native-oh-library/better-banner/releases)，并下载适用版本的 tgz 包。


进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-better-banner@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-better-banner@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```js
import React from 'react';
import {
    StyleSheet,
    View,
    Text,
} from 'react-native';

import BetterBanner from 'react-native-better-banner';

const App = () => {
    return (
        <View style={styles.container}>
            <BetterBanner
                bannerComponents={[
                    <View style={{
                        width: '100%',
                        height: '100%',
                        backgroundColor: '#1997fc',
                        alignItems: 'center',
                        justifyContent: 'center'
                    }}>
                        <Text style={{fontSize: 35, color: '#fff', marginBottom: 10}}>Page 01</Text>
                        <Text style={{fontSize: 15, color: '#fff'}}>Welcome! have a good time</Text>
                    </View>,
                    <View style={{
                        width: '100%',
                        height: '100%',
                        backgroundColor: '#da578f',
                        alignItems: 'center',
                        justifyContent: 'center'
                    }}>
                        <Text style={{fontSize: 35, color: '#fff', marginBottom: 10}}>Page 02</Text>
                        <Text style={{fontSize: 15, color: '#fff'}}>Welcome! have a good time</Text>
                    </View>,
                    <View style={{
                        width: '100%',
                        height: '100%',
                        backgroundColor: '#7c3fe4',
                        alignItems: 'center',
                        justifyContent: 'center'
                    }}>
                        <Text style={{fontSize: 35, color: '#fff', marginBottom: 10}}>Page 03</Text>
                        <Text style={{fontSize: 15, color: '#fff'}}>Welcome! have a good time</Text>
                    </View>,
                ]}
                bannerTitles={["Page 01 Page 01 Page 01 Page 01 Page 01 Page 01 Page 01 ", "Page 02", "Page 03"]}
                onPress={(index) => alert('you pressed index is : ' + index)}
                indicatorContainerBackgroundColor={'rgba(0,0,0,0.3)'}
                isSeamlessScroll={true}
            />
        </View>
    );
};

const styles = StyleSheet.create({
   container: {
       flex: 1
   }

});

export default App;
```
<!-- {% endraw %} -->

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[Releases](https://github.com/react-native-oh-library/better-banner/releases)

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                              | Description                                                  | Type     | Default               | Platform | HarmonyOS Support |
| --------------------------------- | ------------------------------------------------------------ | -------- | --------------------- | -------- | ----------------- |
| bannerImages                      | 用于展示轮播图片, 与`bannerComponents`二选一                 | Array    | []                    | All      | Yes               |
| bannerComponents                  | 用于展示轮播自定义组件，与`bannerImages`二选一               | Array    | []                    | All      | Yes               |
| bannerHeight                      | banner的默认高度                                             | Number   | 250                   | All      | Yes               |
| bannerTitles                      | 每张图片或组件对应的标题                                     | Array    | []                    | All      | Yes               |
| bannerTitleTextColor              | 每张图片或组件对应的标题的文字颜色                           | String   | #fff                  | All      | Yes               |
| bannerTitleTextSize               | 每张图片或组件对应的标题的文字大小                           | Number   | 2000                  | All      | Yes               |
| isAutoScroll                      | 是否开启自动轮播                                             | Boolean  | true                  | All      | Yes               |
| isSeamlessScroll                  | 是否开启无缝滚动(iOS下正常，安卓某些机型可能出现滚动异常)    | Boolean  | false                 | All      | Yes               |
| adaptSeamlessScrollValue          | 如果开启无缝滚动在某些机型滚动异常，可针对这些机型设置`true` 或 `false`, 此值实际上是设置是否显示`ScrollView`的`scrollTo`的滚动动画 | Boolean  | false                 | All      | Yes               |
| indicatorWidth                    | 指示器宽度                                                   | Number   | 10                    | All      | Yes               |
| indicatorHeight                   | 指示器高度                                                   | Number   | 6                     | All      | Yes               |
| indicatorColor                    | 指示器颜色                                                   | String   | rgba(255,255,255,0.6) | All      | Yes               |
| indicatorStyle                    | 指示器样式，您也可以直接使用此属性一次性设置指示器宽、高、颜色和圆角等，它会覆盖以上`indicatorWidth`,`indicatorHeight`，`indicatorColor`属性 | Object   | {}                    | All      | Yes               |
| indicatorGap                      | 指示器之间的间隔                                             | Number   | 6                     | All      | Yes               |
| activeIndicatorColor              | 活动指示器颜色                                               | String   | #fff                  | All      | Yes               |
| indicatorGroupPosition            | 指示器组的位置，可设置`left`,`center`,`right`。如果您设置了`bannerTitles`,则此属性只能是`right` | String   | right                 | All      | Yes               |
| indicatorGroupSideOffset          | 指示器组的左右边距                                           | Number   | 10                    | All      | Yes               |
| indicatorContainerHeight          | 指示器容器高度                                               | Number   | 32                    | All      | Yes               |
| indicatorContainerBackgroundColor | 指示器容器背景色                                             | String   | transparent           | All      | Yes               |
| onPress()                         | 点击轮播图后的回调函数，会传回banner的`index`                | Function | ()=>{}                | All      | Yes               |
| onScrollEnd()                     | 滚动完每张轮播图的回调函数，等同于`ScrollView`的`onMomentumScrollEnd` | Function | ()=>{}                | All      | Yes               |

## 遗留问题


## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://www.isc.org/licenses/) ，请自由地享受和参与开源。
