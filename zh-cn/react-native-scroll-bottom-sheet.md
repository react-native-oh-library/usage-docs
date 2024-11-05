> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-scroll-bottom-sheet</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/rgommezz/react-native-scroll-bottom-sheet">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/rgommezz/react-native-scroll-bottom-sheet/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-scroll-bottom-sheet Releases](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-scroll-bottom-sheet@file:#
```

#### **yarn**

```bash
yarn add  @react-native-oh-tpl/react-native-scroll-bottom-sheet@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, { useCallback, useMemo, useRef } from "react";
import {
  View,
  Text,
  SafeAreaView,
  StyleSheet,
  Animated,
  Dimensions,
  StatusBar,
  Pressable,
  Alert,
} from "react-native";
import ScrollBottomSheet from "react-native-scroll-bottom-sheet";
const WINDOW_HEIGHT = Dimensions.get("window").height;
export default function App() {
  const onSettleCallback = (index: number) => {
    console.log("handleSheetChanges", index);
  };
  const scrollRef = React.useRef(null);
  const data = useMemo(
    () =>
      Array(50)
        .fill(0)
        .map((_, index) => `index-${index}`),
    []
  );
  return (
    <View style={styles.screenbox}>
      <ScrollBottomSheet
        componentType="FlatList"
        snapPoints={[128, "40%", "60%"]}
        initialSnapIndex={2}
        renderHandle={() => (
          <View style={styles.header}>
            <View style={styles.panelHandle} />
          </View>
        )}
        //FlatList
        data={data}
        keyExtractor={(i) => i}
        renderItem={({ item }) => (
          <View style={styles.item}>
            <Text>{`Item ${item}`}</Text>
          </View>
        )}
        onSettle={onSettleCallback}
        animationType={"spring"}
        animationConfig={{}}
        innerRef={scrollRef}
        enableOverScroll={false}
        containerStyle={styles.containerStyle}
        contentContainerStyle={styles.contentContainerStyle}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  screenbox: {
    height: "100%",
    backgroundColor: "papayawhip",
  },
  containerStyle: {
    fontSize: 18,
  },
  container: {
    flex: 1,
    padding: 24,
    backgroundColor: "grey",
  },
  header: {
    alignItems: "center",
    backgroundColor: "white",
    paddingVertical: 20,
    borderTopLeftRadius: 20,
    borderTopRightRadius: 20,
  },
  panelHandle: {
    width: 40,
    height: 2,
    backgroundColor: "rgba(0,0,0,0.3)",
    borderRadius: 4,
  },
  item: {
    padding: 20,
    justifyContent: "center",
    backgroundColor: "white",
    alignItems: "center",
    marginVertical: 10,
  },
  contentContainerStyle: {
    padding: 16,
    backgroundColor: "#F3F4F9",
  },
  contentContainer: {
    flex: 1,
    alignItems: "center",
  },
});
```

## Link

本库依赖以下三方库，请查看对应文档：

- [@react-native-oh-tpl/react-native-gesture-handler](/zh-cn/react-native-gesture-handler.md)
- [@react-native-oh-tpl/react-native-reanimated](/zh-cn/react-native-reanimated.md)
- [@react-native-oh-tpl/bottom-sheet](/zh-cn/gorhom-bottom-sheet.md)

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-reanimated、@react-native-oh-tpl/react-native-gesture-handler 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-reanimated 文档](/zh-cn/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-gesture-handler 文档](/zh-cn/react-native-gesture-handler.md)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-scroll-bottom-sheet Releases](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet/releases)

## 属性

详情见[react-native-scroll-bottom-sheet](https://github.com/rgommezz/react-native-scroll-bottom-sheet)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                                                                                                                                                                                                                                                                                                                                                                                              | Type                                                                                                                  | Required | Platform | HarmonyOS Support |
| ---------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| componentType    | 'FlatList', 'ScrollView', or 'SectionList'                                                                                                                                                                                                                                                                                                                                                                                               | string                                                                                                                | yes      | all      | yes               |
| snapPoints       | Array of numbers and/or percentages that indicate the different resting positions of the bottom sheet (in dp or %), starting from the top. If a percentage is used, that would translate to the relative amount of the total window height. If you want that percentage to be calculated based on the parent available space instead, for example to account for safe areas or navigation bars, use it in combination with topInset prop | Array\<string \| number\>                                                                                             | yes      | all      | yes               |
| initialSnapIndex | Index that references the initial resting position of the drawer, starting from the top.                                                                                                                                                                                                                                                                                                                                                 | number                                                                                                                | yes      | all      | yes               |
| renderHandle     | Render prop for the handle, should return a React Element                                                                                                                                                                                                                                                                                                                                                                                | () => React.ReactNode                                                                                                 | yes      | all      | yes               |
| onSettle         | Callback that is executed right after the bottom sheet settles in one of the snapping points. The new index is provided on the callback                                                                                                                                                                                                                                                                                                  | (index: number) => void                                                                                               | no       | all      | yes               |
| animationType    | timing (default) or spring                                                                                                                                                                                                                                                                                                                                                                                                               | string                                                                                                                | no       | all      | yes               |
| animationConfig  | Timing or Spring configuration for the animation. If animationType is timing, it uses by default a timing configuration with a duration of 250ms and easing fn Easing.inOut(Easing.linear). If animationType is spring, it uses this default spring configuration. You can partially override any parameter from the animation config as per your needs                                                                                  | [TimingConfig or SpringConfig](https://docs.swmansion.com/react-native-reanimated/docs/animations/withTiming/#easing) | no       | all      | yes               |
| animatedPosition | Animated value that tracks the position of the drawer                                                                                                                                                                                                                                                                                                                                                                                    | Animated.useSharedValue<number>                                                                                       | no       | all      | yes               |
| topInset         | This value is useful to provide an offset (in dp) when applying percentages for snapping points                                                                                                                                                                                                                                                                                                                                          | number                                                                                                                | no       | all      | yes               |
| innerRef         | Ref to the inner scrollable component (ScrollView, FlatList or SectionList), so that you can call its imperative methods. For instance, calling scrollTo on a ScrollView.                                                                                                                                                                                                                                                                | RefObject                                                                                                             | no       | all      | yes               |
| containerStyle   | Style to be applied to the container (Handle and Content)                                                                                                                                                                                                                                                                                                                                                                                | StyleProp\<ViewStyle\>                                                                                                | no       | all      | yes               |
| friction         | Friction is the damping coefficient (0 to 1). The closer the damping coefficient is to 1, the more obvious the sliding trend is when the finger continues to slide to the bottom node.                                                                                                                                                                                                                                                   | number                                                                                                                | no       | all      | yes               |
| enableOverScroll | Allow drawer to be dragged beyond lowest snap point                                                                                                                                                                                                                                                                                                                                                                                      | boolean                                                                                                               | no       | all      | yes               |

## Methods 方法

| Name          | Description                                                                 | Type     | Required | Platform    | HarmonyOS Support |
| ------------- | --------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| snapTo(index) | bottomSheetRef refers to the ref passed to the ScrollBottomSheet component. | function | no       | iOS/Android | yes                |

## 遗留问题

## 其他

- 本库基于[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)实现，详见[issue#2](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet/pull/2)
- 若想实现完全可配置选项的高性能交互式 ScrollBottomSheet，建议优先使用[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/rgommezz/react-native-scroll-bottom-sheet/blob/master/LICENSE) ，请自由地享受和参与开源。
