<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-intersection-observer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-intersection-observer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-intersection-observer/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-intersection-observer/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-library/react-native-intersection-observer> Releases](https://github.com/react-native-oh-library/react-native-intersection-observer/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-library/react-native-intersection-observer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-library/react-native-intersection-observer@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useRef } from "react";
import { Text } from "react-native";
import {
  IOScrollView,
  IOScrollViewController,
  InView,
} from "react-native-intersection-observer";

function App() {
  const scrollViewRef = useRef<IOScrollViewController>(null);
  return (
    <IOScrollView ref={scrollViewRef}>
      <Text
        onPress={() => {
          scrollViewRef.current?.scrollToEnd();
        }}
      >
        Scroll to bottom
      </Text>
      <InView onChange={(inView: boolean) => console.log("Inview:", inView)}>
        <Text>
          Plain children are always rendered. Use onChange to monitor state.
        </Text>
      </InView>
    </IOScrollView>
  );
}

export default App;
```

## 约束与限制

#### 兼容性

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

#### 组件及属性

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[react-native-intersection-observer](https://github.com/zhbhun/react-native-intersection-observer/blob/master/README.md)

如下是已经 HarmonyOS 化的属性：

> [!tip] " HarmonyOS 支持"列为 yes 的属性表示支持 HarmonyOS 平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

#### **IOScrollView** **组件**

#### 此组件有以下属性:

Props: Inherits [ScrollView Props](https://reactnative.dev/docs/scrollview#props)

| Name       | Description   | Type                                                         | Required | HarmonyOS Support |
| ---------- | ------------- | ------------------------------------------------------------ | -------- | ----------------- |
| rootMargin | `root margin` | { top: number; left: number; right: number; bottom: number } | false    | yes               |

Methods: Inherits [ScrollView Methods](https://reactnative.dev/docs/scrollview#methods)

#### **IOFlatList** **组件**

#### 此组件有以下属性:

Props: Inherits [FlatList Props](https://reactnative.dev/docs/flatlist#props)

| Name       | Description   | Type                                                         | Required | HarmonyOS Support |
| ---------- | ------------- | ------------------------------------------------------------ | -------- | ----------------- |
| rootMargin | `root margin` | { top: number; left: number; right: number; bottom: number } | false    | yes               |

Methods: Inherits [FlatList Methods](https://reactnative.dev/docs/flatlist#methods)

#### **InView** **组件**

#### 此组件有以下属性:

| Name        | Description                                                  | Type                        | Required | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | --------------------------- | -------- | ----------------- |
| as          | `Render the wrapping element as this element. Defaults to `View`.` | `ComponentType`             | false    | yes               |
| children    | Children expects a plain child, to have the `<InView />` deal with the wrapping element. | ReactNode                   | true     | yes               |
| triggerOnce | Only trigger this method once.                               | boolean                     | false    | yes               |
| onChange    | Call this function whenever the in view state changes. It will receive the `inView` boolean, alongside the current `IntersectionObserverEntry`. | `(inView: boolean) => void` | false    | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/react-native-oh-library/react-native-intersection-observer/blob/sig/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->