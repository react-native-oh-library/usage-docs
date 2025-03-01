> 模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-stickyheader/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-stickyheader Releases](https://github.com/react-native-oh-library/react-native-stickyheader/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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
          stickyHeaderY={60} // 滑动到多少悬浮
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

## 约束与限制

#### 兼容性

在下述版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

此组件有以下属性:

| Property      | Type   | Required | Description       | Platform         | HarmonyOS <br/>Support |
| ------------- | ------ | -------- | ----------------- | ---------------- | ---------------------- |
| StickyHeaderY | number | NO       | 滑动到多少悬浮    | Android <br/>IOS | YES                    |
| StickyScrollY | any    | Yes      | 动画的ScrollY回调 | Android <br/>IOS | YES                    |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jiasongs/react-native-stickyheader/blob/master/LICENSE) ，请自由地享受和参与开源。


