> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/better-banner)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-better-banner Releases](https://github.com/react-native-oh-library/better-banner/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, View, Text } from "react-native";

import BetterBanner from "react-native-better-banner";

const App = () => {
  return (
    <View style={styles.container}>
      <BetterBanner
        bannerComponents={[
          <View
            style={{
              width: "100%",
              height: "100%",
              backgroundColor: "#1997fc",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            <Text style={{ fontSize: 35, color: "#fff", marginBottom: 10 }}>
              Page 01
            </Text>
            <Text style={{ fontSize: 15, color: "#fff" }}>
              Welcome! have a good time
            </Text>
          </View>,
          <View
            style={{
              width: "100%",
              height: "100%",
              backgroundColor: "#da578f",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            <Text style={{ fontSize: 35, color: "#fff", marginBottom: 10 }}>
              Page 02
            </Text>
            <Text style={{ fontSize: 15, color: "#fff" }}>
              Welcome! have a good time
            </Text>
          </View>,
          <View
            style={{
              width: "100%",
              height: "100%",
              backgroundColor: "#7c3fe4",
              alignItems: "center",
              justifyContent: "center",
            }}
          >
            <Text style={{ fontSize: 35, color: "#fff", marginBottom: 10 }}>
              Page 03
            </Text>
            <Text style={{ fontSize: 15, color: "#fff" }}>
              Welcome! have a good time
            </Text>
          </View>,
        ]}
        bannerTitles={[
          "Page 01 Page 01 Page 01 Page 01 Page 01 Page 01 Page 01 ",
          "Page 02",
          "Page 03",
        ]}
        onPress={(index) => alert("you pressed index is : " + index)}
        indicatorContainerBackgroundColor={"rgba(0,0,0,0.3)"}
        isSeamlessScroll={true}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
});

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-better-banner Releases](https://github.com/react-native-oh-library/better-banner/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                              | Description                                                                                                                                  | Type     | Default               | Platform | HarmonyOS Support |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------- | -------- | --------------------- | -------- | ----------------- |
| bannerImages                      | 用于展示轮播图片, 与`bannerComponents`二选一                                                                                                 | Array    | []                    | All      | Yes               |
| bannerComponents                  | 用于展示轮播自定义组件，与`bannerImages`二选一                                                                                               | Array    | []                    | All      | Yes               |
| bannerHeight                      | banner 的默认高度                                                                                                                            | Number   | 250                   | All      | Yes               |
| bannerTitles                      | 每张图片或组件对应的标题                                                                                                                     | Array    | []                    | All      | Yes               |
| bannerTitleTextColor              | 每张图片或组件对应的标题的文字颜色                                                                                                           | String   | #fff                  | All      | Yes               |
| bannerTitleTextSize               | 每张图片或组件对应的标题的文字大小                                                                                                           | Number   | 2000                  | All      | Yes               |
| isAutoScroll                      | 是否开启自动轮播                                                                                                                             | Boolean  | true                  | All      | Yes               |
| isSeamlessScroll                  | 是否开启无缝滚动(iOS 下正常，安卓某些机型可能出现滚动异常)                                                                                   | Boolean  | false                 | All      | Yes               |
| adaptSeamlessScrollValue          | 如果开启无缝滚动在某些机型滚动异常，可针对这些机型设置`true` 或 `false`, 此值实际上是设置是否显示`ScrollView`的`scrollTo`的滚动动画          | Boolean  | false                 | All      | Yes               |
| indicatorWidth                    | 指示器宽度                                                                                                                                   | Number   | 10                    | All      | Yes               |
| indicatorHeight                   | 指示器高度                                                                                                                                   | Number   | 6                     | All      | Yes               |
| indicatorColor                    | 指示器颜色                                                                                                                                   | String   | rgba(255,255,255,0.6) | All      | Yes               |
| indicatorStyle                    | 指示器样式，您也可以直接使用此属性一次性设置指示器宽、高、颜色和圆角等，它会覆盖以上`indicatorWidth`,`indicatorHeight`，`indicatorColor`属性 | Object   | {}                    | All      | Yes               |
| indicatorGap                      | 指示器之间的间隔                                                                                                                             | Number   | 6                     | All      | Yes               |
| activeIndicatorColor              | 活动指示器颜色                                                                                                                               | String   | #fff                  | All      | Yes               |
| indicatorGroupPosition            | 指示器组的位置，可设置`left`,`center`,`right`。如果您设置了`bannerTitles`,则此属性只能是`right`                                              | String   | right                 | All      | Yes               |
| indicatorGroupSideOffset          | 指示器组的左右边距                                                                                                                           | Number   | 10                    | All      | Yes               |
| indicatorContainerHeight          | 指示器容器高度                                                                                                                               | Number   | 32                    | All      | Yes               |
| indicatorContainerBackgroundColor | 指示器容器背景色                                                                                                                             | String   | transparent           | All      | Yes               |
| onPress()                         | 点击轮播图后的回调函数，会传回 banner 的`index`                                                                                              | Function | ()=>{}                | All      | Yes               |
| onScrollEnd()                     | 滚动完每张轮播图的回调函数，等同于`ScrollView`的`onMomentumScrollEnd`                                                                        | Function | ()=>{}                | All      | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://www.isc.org/licenses/).
