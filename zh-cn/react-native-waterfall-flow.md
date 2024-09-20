> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-waterfall-flow</code> </h1>
</p>
<p align="center">
    <a href="https://www.npmjs.com/package/react-native-waterfall-flow">       
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/axerjs/react-native-waterfall-flow/blob/HEAD/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

>[!TIP] [Github 地址](https://github.com/axerjs/react-native-waterfall-flow)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-waterfall-flow@1.1.5 --save
```

#### **yarn**

```bash
yarn add react-native-waterfall-flow@1.1.5 --save
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState, useRef } from 'react';
import { View, Text, StyleSheet, Button, RefreshControl, Alert } from 'react-native';
import WaterfallFlow from 'react-native-waterfall-flow';

const App = () => {
  const item = ['Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item', 'Item'].map((l, i) => ({ id: l, text: i + ` ${l}` }))
  const [data, setData] = useState(item);
  const [refreshing, setRefreshing] = useState(false);
  const waterfallRef = useRef(null);

  const renderItem = ({ item }) => {

    return (
      <View style={styles.item}>
        <Text>{item.text}</Text>
      </View>
    );
  }

  const onRefresh = () => {
    setRefreshing(true);
    setTimeout(() => {
      // 模拟刷新数据
      setData([...item]);
      setRefreshing(false);
    }, 2000);
  };

  const onEndReached = () => {
    // 模拟加载更多数据
    setData([...data, { id: `${data.length + 1}`, text: `${data.length + 1} Item` }, { id: `${data.length + 2}`, text: `${data.length + 2} Item` }]);
    // Alert.alert('滚动到底部')
  };

  return (
    <View style={styles.container}>
      <View style={{ flex: 1 }}>
        <WaterfallFlow
          ref={waterfallRef}
          renderItem={renderItem}
          data={data}
          numColumns={2}
          ListHeaderComponent={<Text style={styles.header}>Header Component</Text>}
          ListFooterComponent={<Text style={styles.footer}>Footer Component</Text>}
          ListEmptyComponent={<Text style={styles.empty}>No Data Available</Text>}
          onEndReached={onEndReached}
          onRefresh={onRefresh}
          refreshing={refreshing}
          style={styles.waterfall}
          contentContainerStyle={styles.contentContainer}
          refreshControl={<RefreshControl refreshing={refreshing} onRefresh={onRefresh} />}
        />
      </View>
      <View style={styles.buttonsContainer}>
        <Button
          title="Scroll to End"
          onPress={() => waterfallRef.current.scrollToEnd({ animated: true })}
        />
        <Button
          title="Scroll to Index"
          onPress={() => { data.length >= 20 ? waterfallRef.current.scrollToIndex({ animated: true, index: 20, viewPosition: 0 }) : false }}
        />
        <Button
          title="Scroll to Offset"
          onPress={() => waterfallRef.current.scrollToOffset({ offset: 0 })}
        />
      </View>
      <View style={styles.buttonDelete}>
        <Button
          title="Delete Data"
          onPress={() => { setData([]) }}
        />
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  waterfall: {
    flex: 1,
  },
  contentContainer: {
    padding: 10,
  },
  item: {
    backgroundColor: '#ccc',
    margin: 5,
    padding: 10,
    borderRadius: 5,
  },
  header: {
    padding: 10,
    fontSize: 18,
    textAlign: 'center',
  },
  footer: {
    padding: 10,
    fontSize: 16,
    textAlign: 'center',
  },
  empty: {
    padding: 10,
    fontSize: 16,
    textAlign: 'center',
  },
  buttonsContainer: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    padding: 10,
  },
  buttonDelete: {
    marginBottom: 20
  }
});

export default App;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.29; SDK：HarmonyOS NEXT Developer Beta6; IDE：DevEco Studio 5.0.3.706; ROM：NEXT.0.0.65; 



## 属性

>[!TIP] "Platform"列表示该属性在原三方库上支持的平台。

>[!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- | ----------------- |
| `renderItem` | 用于将当前`item`渲染到列表中 | function | Yes       | All      | yes               |
| `data`     | 瀑布流数据源，可以是任意内容的数组            | array | Yes       | All      | yes               |
| `numColumns` | 瀑布流的列数，默认为2，即两列                    | number | No   | All      | yes               |
| `ListHeaderComponent` | 头部组件。可以是 React Component 或 render 函数。                          | component`, `function | No       | All      | yes               |
| `ListFooterComponent` | 尾部组件。可以是 React Component 或 render 函数。 | component`, `function | No       | All      | yes               |
| `ListEmptyComponent` | 列表为空时渲染该组件。可以是 React Component 或 render 函数 | component`, `function | No       | All      | yes               |
| `onEndReached`   | 当列表滚动到底部是调用            | function | No       | All      | yes               |
| `onRefresh`   | 如果设置了此选项，则会在列表头部添加一个标准的[`RefreshControl`](https://www.react-native.cn/docs/refreshcontrol) 控件，以便实现“下拉刷新”的功能。同时你需要正确设置`refreshing`属性。 | function | No       | All      | yes               |
| `refreshing` | 在等待加载新数据时将此属性设为 true，列表就会显示出一个正在加载的符号。                   | boolean | No       | All      | yes               |
| `style`     | 用于设置瀑布流外层样式，默认会有`{ flex: 1 }`的样式，即高度充满父容器             | object | No       | All      | yes               |
| `contentContainerStyle` | 瀑布流内容容器样式                           | object | No   | All      | yes               |

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                       | Description                                                  | Type   | Required | Platform | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `scrollToEnd([params])`    | 滚动到瀑布流列表的底部                                       | object | No       | All      | yes               |
| `scrollToIndex([params])`  | 将位于指定位置的元素滚动到可视区的指定位置，当viewPosition 为 0 时将它滚动到屏幕顶部，为 1 时将它滚动到屏幕底部，为 0.5 时将它滚动到屏幕中央。 | object | Yes      | All      | yes               |
| `scrollToOffset([params])` | 滚动列表到指定的偏移（以像素为单位），等同于ScrollView的scrollTo方法。 | object | Yes      | All      | yes               |

## 遗留问题

 无

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/axerjs/react-native-waterfall-flow/blob/HEAD/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->