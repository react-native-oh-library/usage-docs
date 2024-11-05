> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-library/react-native-scroll-bottom-sheet Releases](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet/releases).

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

This repository depends on the following libraries, please refer to the corresponding documentation: 

- [@react-native-oh-tpl/react-native-gesture-handler](/en/react-native-gesture-handler.md)
- [@react-native-oh-tpl/react-native-reanimated](/en/react-native-reanimated.md)
- [@react-native-oh-tpl/bottom-sheet](/en/gorhom-bottom-sheet.md)

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-reanimated、@react-native-oh-tpl/react-native-gesture-handler. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-reanimated](/en/react-native-reanimated.md)、[@react-native-oh-tpl/react-native-gesture-handler](/en/react-native-gesture-handler.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-scroll-bottom-sheet Releases](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet/releases)

## Properties

For details, see [react-native-scroll-bottom-sheet](https://github.com/rgommezz/react-native-scroll-bottom-sheet)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Static Methods

| Name          | Description                                                                 | Type     | Required | Platform    | HarmonyOS Support |
| ------------- | --------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| snapTo(index) | bottomSheetRef refers to the ref passed to the ScrollBottomSheet component. | function | no       | iOS/Android | yes               |

## Known Issues

## Others

- 本库基于[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)实现，详见[issue#2](https://github.com/react-native-oh-library/react-native-scroll-bottom-sheet/pull/2)
- 若想实现完全可配置选项的高性能交互式 ScrollBottomSheet，建议优先使用[@gorhom/bottom-sheet](https://github.com/react-native-oh-library/react-native-bottom-sheet)。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/rgommezz/react-native-scroll-bottom-sheet/blob/master/LICENSE).
