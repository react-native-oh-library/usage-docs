> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-stickyheader</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jiasongs/react-native-stickyheader/blob/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jiasongs/react-native-stickyheader/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-stickyheader/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-stickyheader Releases](https://github.com/react-native-oh-library/react-native-stickyheader/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-stickyheader
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-stickyheader
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState, useCallback, useRef, useEffect } from "react";
import { StyleSheet, Text, View, FlatList, Animated } from "react-native";
import StickyHeader from "react-native-stickyheader";

function App() {
  const scrollY = useRef(new Animated.Value(0));
  const [data, setData] = useState([]);

  useEffect(() => {
    let array = [];
    for (let index = 0; index < 100; index++) {
      array.push(index);
    }
    setData(array);
  }, []);

  const renderItem = useCallback((info) => {
    return (
      <View style={{ height: 50, backgroundColor: "#ffffff" }}>
        <Text>{info.item}</Text>
      </View>
    );
  }, []);

  const keyExtractor = useCallback((item, index) => {
    return index + "";
  }, []);

  return (
    <View style={styles.container}>
      <View style={{ height: 64, backgroundColor: "#973444" }} />
      <Animated.ScrollView
        onScroll={Animated.event(
          [
            {
              nativeEvent: { contentOffset: { y: scrollY.current } },
            },
          ],
          { useNativeDriver: true },
        )}
        scrollEventThrottle={1}
      >
        <Text>文字</Text>
        <Text>文字</Text>
        <Text>文字</Text>
        <Text>文字</Text>
        <StickyHeader
          stickyHeaderY={60} 
          stickyScrollY={scrollY.current}
        >
          <View style={{ height: 60, backgroundColor: "#d22222" }} />
        </StickyHeader>
        <FlatList
          data={data}
          keyExtractor={keyExtractor}
          renderItem={renderItem}
        />
      </Animated.ScrollView>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: "#ffffff",
    justifyContent: "center",
  },
});

export default App;
```

## Constraints

#### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

此组件有以下属性:

| Property      | Type   | Required | Description       | Platform         | HarmonyOS <br/>Support |
| ------------- | ------ | -------- | ----------------- | ---------------- | ---------------------- |
| StickyHeaderY | number | NO       | 滑动到多少悬浮    | Android <br/>IOS | YES                    |
| StickyScrollY | any    | Yes      | 动画的ScrollY回调 | Android <br/>IOS | YES                    |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jiasongs/react-native-stickyheader/blob/master/LICENSE).


