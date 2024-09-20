> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sortable-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gitim/react-native-sortable-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/gitim/react-native-sortable-list/blob/master/LICENSE"/>
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sortable-list)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-sortabel-list Releases](https://github.com/react-native-oh-library/react-native-sortable-list/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sortable-list@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sortable-list@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 */

import React, {
  useCallback,
  useEffect,
  useMemo,
  useRef,
  useState,
} from "react";
import {
  Animated,
  Easing,
  StyleSheet,
  Text,
  Image,
  View,
  Dimensions,
  Platform,
  ScrollView,
  TextInput,
  Button,
} from "react-native";
import SortableList from "react-native-sortable-list";

const window = Dimensions.get("window");

const data = {
  0: {
    text: "Chloe （0）",
  },
  1: {
    text: "Jasper （1）",
  },
  2: {
    text: "Pepper （2）",
  },
  3: {
    text: "Oscar （3）",
  },
};

export default function SortDemo() {
  const renderRow = useCallback(({ data, active }) => {
    return <Row data={data} active={active} />;
  }, []);
  return (
    <View style={{ height: 600 }}>
      <SortableList style={styles.list} data={data} renderRow={renderRow} />
    </View>
  );
}

function Row(props) {
  const { active, data } = props;

  const activeAnim = useRef(new Animated.Value(0));
  const style = useMemo(
    () => ({
      ...Platform.select({
        ios: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          shadowRadius: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 10],
          }),
        },

        android: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          elevation: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 6],
          }),
        },
        harmony: {
          transform: [
            {
              scale: activeAnim.current.interpolate({
                inputRange: [0, 1],
                outputRange: [1, 1.07],
              }),
            },
          ],
          elevation: activeAnim.current.interpolate({
            inputRange: [0, 1],
            outputRange: [2, 6],
          }),
        },
      }),
    }),
    []
  );
  useEffect(() => {
    Animated.timing(activeAnim.current, {
      duration: 300,
      easing: Easing.bounce,
      toValue: Number(active),
      useNativeDriver: true,
    }).start();
  }, [active]);

  return (
    <Animated.View style={[styles.row, style]}>
      <Text style={styles.text}>{data.text}</Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  list: {
    flex: 1,
    backgroundColor: "#AAE",
  },
  contentContainer: {
    width: window.width - 100,
    ...Platform.select({
      ios: {
        paddingHorizontal: 30,
      },
      android: {
        paddingHorizontal: 0,
      },
      harmony: {
        paddingHorizontal: 0,
      },
    }),
  },
  row: {
    flexDirection: "row",
    alignItems: "center",
    backgroundColor: "#fff",
    padding: 16,
    height: 80,
    flex: 1,
    marginTop: 10,
    ...Platform.select({
      ios: {
        width: window.width - 60 * 2,
        shadowColor: "rgba(0,0,0,0.2)",
        shadowOpacity: 1,
        shadowOffset: { height: 2, width: 2 },
        shadowRadius: 2,
      },
      android: {
        width: window.width - 60 * 2,
        elevation: 0,
        marginHorizontal: 30,
      },
      harmony: {
        width: window.width - 60 * 2,
        elevation: 0,
        marginHorizontal: 30,
        shadowColor: "rgba(0,0,0,0.2)",
        shadowOpacity: 1,
        shadowOffset: { height: 2, width: 2 },
        shadowRadius: 2,
      },
    }),
  },
  text: {
    fontSize: 18,
    color: "#222222",
  },
});
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-sortabel-list Releases](https://github.com/react-native-oh-library/react-native-sortable-list/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                           | Description                                                                                                                                                                    | **Type**      | Required | Platform | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| data                           | data source                                                                                                                                                                    | Object        | yes      | All      | Yes               |
| order                          | an array of keys from data, the order of keys from the array will be used to initial rows order                                                                                | Array         | no       | All      | Yes               |
| style                          | View style                                                                                                                                                                     | Object, Array | no       | All      | Yes               |
| contentContainerStyle          | these styles will be applied to the inner scroll view content container                                                                                                        | Object, Array | no       | All      | Yes               |
| innerContainerStyle            | these styles will be applied to the inner scroll view content container, excluding the header and footer                                                                       | Object, Array | no       | All      | Yes               |
| horizontal                     | when true, the SortableList's children are arranged horizontally in a row instead of vertically in a column. The default value is false.                                       | boolean       | no       | All      | Yes               |
| showsVerticalScrollIndicator   | when false, the vertical scroll indicator will not be visible. The default value is true.                                                                                      | boolean       | no       | All      | Yes               |
| showsHorizontalScrollIndicator | when false, the horizontal scroll indicator will not be visible. The default value is true.                                                                                    | boolean       | no       | All      | Yes               |
| sortingEnabled                 | when false, rows are not sortable. The default value is true.                                                                                                                  | boolean       | no       | All      | Yes               |
| scrollEnabled                  | when false, the content does not scrollable. The default value is true.                                                                                                        | boolean       | no       | All      | Yes               |
| keyboardShouldPersistTaps      | Determines when the keyboard should stay visible after a tap. Default 'never'.                                                                                                 | string        | no       | All      | Yes               |
| manuallyActivateRows           | whether you intend to use the toggleRowActive method to activate a row or use the out of box solution.                                                                         | bool          | no       | All      | Yes               |
| autoscrollAreaSize             | determines the height for vertical list and the width for horizontal list of the area at the begining and the end of the list that will trigger autoscrolling. Defaults to 60. | number        | no       | All      | Yes               |
| rowActivationTime              | determines time delay in ms before pressed row becomes active. Defaults to 200 ms.                                                                                             | number        | no       | All      | Yes               |
| refreshControl                 | A RefreshControl that works the same way as a ScrollView's refreshControl.                                                                                                     | element       | no       | All      | Yes               |
| renderRow                      | Takes a row key, row index, data entry from the data source and its statuses disabled, active and should return a renderable component to be rendered as the row.              | function      | yes      | All      | Yes               |
| renderHeader                   | Renders returned component at the top of the list.                                                                                                                             | function      | no       | All      | Yes               |
| renderFooter                   | Renders returned component at the bottom of the list.                                                                                                                          | function      | no       | All      | Yes               |
| onChangeOrder                  | Called when rows were reordered, takes an array of rows keys of the next rows order.                                                                                           | bool          | no       | All      | Yes               |
| onActivateRow                  | Called when a row was activated (user long tapped).                                                                                                                            | function      | no       | All      | Yes               |
| onReleaseRow                   | Called when the active row was released. Returns the key and the new list order.                                                                                               | function      | no       | All      | Yes               |
| onPressRow                     | Called when a row was pressed.                                                                                                                                                 | function      | no       | All      | Yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name           | Description                                                                 | **Type**       | Required | Platform | HarmonyOS Support |
| -------------- | --------------------------------------------------------------------------- | -------------- | -------- | -------- | ----------------- |
| scrollBy       | scrolls by a given y offset, either immediately or with a smooth animation. | dy?, animated? | no       | All      | Yes               |
| scrollTo       | scrolls to a given y offset, either immediately or with a smooth animation. | y?, animated?  | no       | All      | Yes               |
| scrollToRowKey | scrolls to a given row key, either immediately or with a smooth animation.  | key, animated? | no       | All      | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/react-native-oh-library/react-native-sortable-list/blob/sig/LICENSE) ，请自由地享受和参与开源。
