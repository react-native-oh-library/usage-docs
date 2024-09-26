> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-awesome-gallery</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Flair-Dev/react-native-awesome-gallery">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/pavelbabenko/react-native-awesome-gallery/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/Flair-Dev/react-native-awesome-gallery)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-awesome-gallery@0.4.2
```

#### **yarn**

```bash
yarn add react-native-awesome-gallery@0.4.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```ts
import React from 'react';
import {View, SafeAreaView} from 'react-native';
import Gallery from 'react-native-awesome-gallery';

const getRandomSize = function () {
  const min = 400;
  const max = 800;
  return Math.floor(Math.random() * (max - min + 1)) + min;
};

const images = new Array(10)
  .fill(0)
  .map(() => `https://picsum.photos/${getRandomSize()}/${getRandomSize()}`);

export default function App() {
  return (
    <View style={{flex: 1}}>
      <SafeAreaView></SafeAreaView>
      <View style={{height: '100%', width: '100%'}}>
        <Gallery data={images} swipeEnabled={true} />
      </View>
    </View>
  );
}
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-gesture-handler、@react-native-oh-tpl/react-native-reanimated 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)、[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)进行引入

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.28; SDK: HarmonyOS-NEXT-DB5 5.0.0.60; IDE: DevEco Studio  5.0.3.655; ROM: 3.0.0.36;

2. RNOH: 0.72.29; SDK: HarmonyOS-NEXT-DB6 5.0.0.61; IDE: DevEco Studio  5.0.3.706; ROM: 5.0.0.60;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                     | Type           | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------- | -------------- | -------- | ----------- | ----------------- |
| data        | Array of items to render       | T[] | Yes       | iOS/Android | Yes               |
| renderItem       | Callback func which can be used to render custom image component, e.g FastImage. NOTE: You have to call setImageDimensions({width, height}) parameter after image is loaded         | (renderItemInfo: {item: T, index: number, setImageDimensions: Function}) => React.ReactElement | No       | iOS/Android | Yes               |
| keyExtractor | Callback func which provides unique keys for items  | (item: T, index: number) => string or number | No       | iOS/Android | Yes               |
| initialIndex     | The initial image index | number        | No       | iOS/Android | Yes               |
| onIndexChange     | Is called when index of active item is changed | boolean        | No       | iOS/Android | Yes               |
| numToRender     | Amount of items rendered in gallery simultaneously | number        | No       | iOS/Android | Yes               |
| emptySpaceWidth     | Width of empty space between items | number        | No       | iOS/Android | Yes               |
| doubleTapScale     | Image scale when double tap is fired | number        | No       | iOS/Android | No               |
| doubleTapInterval     | Time in milliseconds between single and double tap events | number        | No       | iOS/Android | No               |
| maxScale     | Maximum scale user can set with gesture | number        | No       | iOS/Android | Yes               |
| pinchEnabled     | Is pinch gesture enabled | boolean        | No       | iOS/Android | Yes               |
| swipeEnabled     | Is pan gesture enabled | boolean        | No       | iOS/Android | Yes               |
| doubleTapEnabled     | Is double tap enabled | boolean        | No       | iOS/Android | No               |
| disableTransitionOnScaledImage     | Disables transition to next/previous image when scale > 1 | boolean        | No       | iOS/Android | Yes               |
| hideAdjacentImagesOnScaledImage     | Hides next and previous images when scale > 1 | boolean        | No       | iOS/Android | Yes               |
| disableVerticalSwipe     | Disables vertical swipe when scale == 1 | boolean        | No       | iOS/Android | Yes               |
| disableSwipeUp     | Disables swipe up when scale == 1 | boolean        | No       | iOS/Android | Yes               |
| loop     | Allows user to swipe infinitely. Works when data.length > 1 | boolean        | No       | iOS/Android | Yes               |
| onScaleChange     | Is called when scale is changed | (scale: number) => void        | No       | iOS/Android | Yes               |
| onScaleChangeRange     | Shows range of scale in which onScaleChange is called | {start: number, end: number}        | No       | iOS/Android | Yes               |
| containerDimensions     | Dimensions object for the View that wraps gallery. | {width: number, height: number}        | No       | iOS/Android | Yes               |
| style     | Is double tap enabled | Style of container        | No       | iOS/Android | Yes               |

## 事件

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| onSwipeToClose()         | Fired when user swiped to top/bottom                                  | function         | No       | iOS/Android | Yes               |
| onTranslationYChange(translationY: number, shouldClose: boolean) | 'worklet'; Fired when user is swiping vertically to close the gallery                         | function         | No       | iOS/Android | No               |
| onTap()          | Fired when user tap on image                                | string or number | No       | iOS/Android | Yes               |
| onDoubleTap(toScale: number)        | Fired when user double tap on image                                 | function         | No       | iOS/Android | No               |
| onLongPress()              | Fired when long press is detected                                         | function           | No       | iOS/Android | Yes               |
| onScaleStart(scale: number)         | Fired when pinch gesture starts                             | function            | No       | iOS/Android | Yes               |
| onScaleEnd(scale: number) | Fired when pinch gesture ends. Use case: add haptic feedback when user finished gesture with scale > maxScale or scale < 1                    | function            | No       | iOS/Android | Yes               |
| onPanStart()           | Fired when pan gesture starts                                    | function            | No       | iOS/Android | Yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                        | Type             | Required | Platform    | HarmonyOS Support |
| ------------------ | -------------------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| setIndex        | Sets active index                                  | (newIndex: number, animated?: boolean) => void         | No       | iOS/Android | Yes               |
| reset | Resets scale, translation                         | (animated?: boolean) => void         | No       | iOS/Android | Yes               |

## 遗留问题
- [ ] onTranslationYChange事件设置后，拖动图片会发生异常，iOS 和 Android平台均有该问题: [issue#84](https://github.com/pavelbabenko/react-native-awesome-gallery/issues/84)
- [x] react-native-gesture-handler库Gesture.Tap()事件无法获取正确的当前坐标和手指数，导致doubleTapScale、doubleTapInterval、doubleTapEnabled、onDoubleTap不生效: [issue#21](https://github.com/react-native-oh-library/react-native-harmony-gesture-handler/issues/21)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/pavelbabenko/react-native-awesome-gallery/blob/main/LICENSE) ，请自由地享受和参与开源。