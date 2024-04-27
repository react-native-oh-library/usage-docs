模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-sortable-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gitim/react-native-sortable-list">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-sortable-list)

## 安装与使用

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

> [!TIP] 原库最新的修改并未发布到 npm 仓，导致 npm 仓上最新的版本在新架构上无法使用。

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-sortable-list@file:#
// 若要运行 Android or iOS
npm install react-native-sortable-list@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-sortable-list@file:#
// 若要运行 Android or iOS
yarn add react-native-sortable-list@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
/**
 * Sample React Native App
 * https://github.com/facebook/react-native
 *
 * @format
 */

import React, {useCallback, useEffect, useMemo, useRef} from 'react';
import {
  Animated,
  Image,
  StyleSheet,
  Text,
  Platform,
  Easing,
  View,
  Dimensions,
} from 'react-native';
import SortableList from 'react-native-sortable-list';

const window = Dimensions.get('window');

const data = {
  0: {
    image: 'https://placekitten.com/200/240',
    text: 'Chloe',
  },
  1: {
    image: 'https://placekitten.com/200/201',
    text: 'Jasper',
  },
  2: {
    image: 'https://placekitten.com/200/202',
    text: 'Pepper',
  },
  3: {
    image: 'https://placekitten.com/200/203',
    text: 'Oscar',
  },
  4: {
    image: 'https://placekitten.com/200/204',
    text: 'Dusty',
  },
  5: {
    image: 'https://placekitten.com/200/205',
    text: 'Spooky',
  },
  6: {
    image: 'https://placekitten.com/200/210',
    text: 'Kiki',
  },
  7: {
    image: 'https://placekitten.com/200/215',
    text: 'Smokey',
  },
  8: {
    image: 'https://placekitten.com/200/220',
    text: 'Gizmo',
  },
  9: {
    image: 'https://placekitten.com/220/239',
    text: 'Kitty',
  },
};

function Row(props) {
  const {active, data} = props;

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
    [],
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
      <Image source={{uri: data.image}} style={[styles.image]} />
      <Text style={styles.text}>{data.text}</Text>
    </Animated.View>
  );
}

const App = () => {
  const renderRow = useCallback(({data, active}) => {
    return <Row data={data} active={active} />;
  }, []);

  return (
    <View style={styles.container}>
      <Text style={styles.title}>React Native Sortable List</Text>
      <SortableList
        style={styles.list}
        contentContainerStyle={styles.contentContainer}
        data={data}
        renderRow={renderRow}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#eee',
    ...Platform.select({
      ios: {
        paddingTop: 20,
      },
      harmony: {
        paddingTop: 20,
      },
    }),
  },
  title: {
    fontSize: 20,
    paddingVertical: 20,
    color: '#999999',
  },
  list: {
    flex: 1,
  },
  contentContainer: {
    width: window.width,
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
    flexDirection: 'row',
    alignItems: 'center',
    backgroundColor: '#fff',
    padding: 16,
    height: 80,
    flex: 1,
    marginTop: 7,
    marginBottom: 12,
    borderRadius: 4,
    ...Platform.select({
      ios: {
        width: window.width - 30 * 2,
        shadowColor: 'rgba(0,0,0,0.2)',
        shadowOpacity: 1,
        shadowOffset: {height: 2, width: 2},
        shadowRadius: 2,
      },
      android: {
        width: window.width - 30 * 2,
        elevation: 0,
        marginHorizontal: 30,
      },
      harmony: {
        width: window.width - 30 * 2,
        elevation: 0,
        marginHorizontal: 30,
        shadowColor: 'rgba(0,0,0,0.2)',
        shadowOpacity: 1,
        shadowOffset: {height: 2, width: 2},
        shadowRadius: 2,
      },
    }),
  },
  image: {
    width: 50,
    height: 50,
    marginRight: 30,
    borderRadius: 25,
  },
  text: {
    fontSize: 24,
    color: '#222222',
  },
});

export default App;
```

## 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情见[react-native-sortable-list ReadMe](https://github.com/gitim/react-native-sortable-list/tree/master)

### Props:

| Name                           | Description                                                                                                                                                                    | **Type**      | Platform | Required | HarmonyOS Support |
| ------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------- | -------- | -------- | ----------------- |
| data                           | data source                                                                                                                                                                    | Object        | All      | Y        | Yes               |
| order                          | an array of keys from data, the order of keys from the array will be used to initial rows order                                                                                | Array         | All      | N        | Yes               |
| style                          | View style                                                                                                                                                                     | Object, Array | All      | N        | Yes               |
| contentContainerStyle          | these styles will be applied to the inner scroll view content container                                                                                                        | Object, Array | All      | N        | Yes               |
| innerContainerStyle            | these styles will be applied to the inner scroll view content container, excluding the header and footer                                                                       | Object, Array | All      | N        | Yes               |
| horizontal                     | when true, the SortableList's children are arranged horizontally in a row instead of vertically in a column. The default value is false.                                       | boolean       | All      | N        | Yes               |
| showsVerticalScrollIndicator   | when false, the vertical scroll indicator will not be visible. The default value is true.                                                                                      | boolean       | All      | Y        | Yes               |
| showsHorizontalScrollIndicator | when false, the horizontal scroll indicator will not be visible. The default value is true.                                                                                    | boolean       | All      | N        | Yes               |
| sortingEnabled                 | when false, rows are not sortable. The default value is true.                                                                                                                  | boolean       | All      | N        | Yes               |
| scrollEnabled                  | when false, the content does not scrollable. The default value is true.                                                                                                        | boolean       | All      | N        | Yes               |
| keyboardShouldPersistTaps      | Determines when the keyboard should stay visible after a tap. Default 'never'.                                                                                                 | string        | All      | N        | No                |
| manuallyActivateRows           | whether you intend to use the toggleRowActive method to activate a row or use the out of box solution.                                                                         | bool          | All      | N        | Yes               |
| autoscrollAreaSize             | determines the height for vertical list and the width for horizontal list of the area at the begining and the end of the list that will trigger autoscrolling. Defaults to 60. | number        | All      | N        | Yes               |
| rowActivationTime              | determines time delay in ms before pressed row becomes active. Defaults to 200 ms.                                                                                             | number        | All      | N        | Yes               |
| refreshControl                 | A RefreshControl that works the same way as a ScrollView's refreshControl.                                                                                                     | element       | All      | N        | Yes               |
| renderRow                      | Takes a row key, row index, data entry from the data source and its statuses disabled, active and should return a renderable component to be rendered as the row.              | function      | All      | Y        | Yes               |
| renderHeader                   | Renders returned component at the top of the list.                                                                                                                             | function      | All      | N        | Yes               |
| renderFooter                   | Renders returned component at the bottom of the list.                                                                                                                          | function      | All      | N        | Yes               |
| onChangeOrder                  | Called when rows were reordered, takes an array of rows keys of the next rows order.                                                                                           | bool          | All      | N        | Yes               |
| onActivateRow                  | Called when a row was activated (user long tapped).                                                                                                                            | function      | All      | N        | Yes               |
| onReleaseRow                   | Called when the active row was released. Returns the key and the new list order.                                                                                               | function      | All      | N        | Yes               |
| onPressRow                     | Called when a row was pressed.                                                                                                                                                 | function      | All      | N        | Yes               |

## 方法

### Methods

| Name           | Description                                                                 | **Type**       | Platform | Required | HarmonyOS Support |
| -------------- | --------------------------------------------------------------------------- | -------------- | -------- | -------- | ----------------- |
| scrollBy       | scrolls by a given y offset, either immediately or with a smooth animation. | dy?, animated? | All      | N        | Yes               |
| scrollTo       | scrolls to a given y offset, either immediately or with a smooth animation. | y?, animated?  | All      | N        | Yes               |
| scrollToRowKey | scrolls to a given row key, either immediately or with a smooth animation.  | key, animated? | All      | N        | Yes               |

## 遗留问题

- [ ] 上下拖拽的时候图片会偶现闪烁

## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/oblador/react-native-progress/blob/master/LICENSE) ，请自由地享受和参与开源。
