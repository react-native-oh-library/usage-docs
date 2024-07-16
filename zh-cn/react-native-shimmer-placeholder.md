> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shimmer-placeholder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tomzaku/react-native-shimmer-placeholder">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tomzaku/react-native-shimmer-placeholder/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/tomzaku/react-native-shimmer-placeholder)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-shimmer-placeholder@2.0.9
```

#### **yarn**

```bash
yarn add react-native-shimmer-placeholder@2.0.9
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { createShimmerPlaceholder } from "react-native-shimmer-placeholder";
import LinearGradient from "react-native-linear-gradient";

const ShimmerPlaceholder = createShimmerPlaceholder(LinearGradient);
const FacebookContent = () => {
  // Handle animation
  const avatarRef = React.createRef();
  const firstLineRef = React.createRef();
  const secondLineRef = React.createRef();
  const thirdLineRef = React.createRef();

  React.useEffect(() => {
    const facebookAnimated = Animated.stagger(400, [
      avatarRef.current.getAnimated(),
      Animated.parallel([
        firstLineRef.current.getAnimated(),
        secondLineRef.current.getAnimated(),
        thirdLineRef.current.getAnimated(),
      ]),
    ]);
    Animated.loop(facebookAnimated).start();
  }, []);

  return (
    <View>
      <View style={{ flexDirection: "row" }}>
        <ShimmerPlaceholder ref={avatarRef} stopAutoRun />
        <View style={{ justifyContent: "space-between" }}>
          <ShimmerPlaceholder ref={firstLineRef} stopAutoRun />
          <ShimmerPlaceholder ref={secondLineRef} stopAutoRun />
          <ShimmerPlaceholder ref={thirdLineRef} stopAutoRun />
        </View>
      </View>
    </View>
  );
};
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                                                                                            | Required | Type      | Platform | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------------------------------------------------ | -------- | --------- | -------- | ----------------- |
| **LinearGradient**         | Linear Gradient components ('react-native-linear-gradient' or 'expo-linear-gradient')                  | no       | Component | ALL      | yes               |
| **visible**                | Visible child components                                                                               | no       | boolean   | ALL      | yes               |
| **style**                  | Container Style                                                                                        | no       | Style     | ALL      | yes               |
| **shimmerStyle**           | Shimmer Style only                                                                                     | no       | Style     | ALL      | yes               |
| **contentStyle**           | Content Style when visible                                                                             | no       | Style     | ALL      | yes               |
| **location**               | Locations of shimmer                                                                                   | no       | number[]  | ALL      | yes               |
| **width**                  | Width of row                                                                                           | no       | number    | ALL      | yes               |
| **duration**               | Duration of shimmer over a row                                                                         | no       | number    | ALL      | yes               |
| **height**                 | Height of row                                                                                          | no       | number    | ALL      | yes               |
| **shimmerWidthPercent**    | Percent of shimmer width                                                                               | no       | number    | ALL      | yes               |
| **isReversed**             | Reverse direction of animation                                                                         | no       | boolean   | ALL      | yes               |
| **stopAutoRun**            | Stop running shimmer animation at beginning                                                            | no       | boolean   | ALL      | yes               |
| **isInteraction**          | Defines whether or not the shimmer animation creates an interaction handle on the `InteractionManager` | no       | boolean   | ALL      | yes               |
| **shimmerColors**          | Colors of the shimmer.                                                                                 | no       | string[]  | ALL      | yes               |
| **containerProps**         | Props passed to the outermost View                                                                     | no       | ViewProps | ALL      | yes               |
| **shimmerContainerProps**  | Props passed to the View which contains the loading animation                                          | no       | ViewProps | ALL      | yes               |
| **childrenContainerProps** | Props passed to the View which contains the children                                                   | no       | ViewProps | ALL      | yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Method          | Description                 | Type     | **Required** | Platform | HarmonyOS Support |
| --------------- | --------------------------- | -------- | ------------ | -------- | ----------------- |
| **getAnimated** | get Animated of Placeholder | Animated | no           | ALL      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/tomzaku/react-native-shimmer-placeholder/blob/master/LICENSE) ，请自由地享受和参与开源。
