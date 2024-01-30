> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>< react-native-drag-sort ></code> </h1>
</p>
<p align="center">
    <a href="https://github.com/<原库源码仓地址>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|<如原库还支持其他平台，添加在此处>|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/<原库源码仓LICENSE的路径（如有）>">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!tip] [Github 地址](https://github.com/mochixuan/react-native-drag-sort)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-drag-sort
```

#### **npm**

```bash
npm i react-native-drag-sort --save 

export { DragSortableView, AutoDragSortableView, AnySizeDragSortableView }
```

下面的代码展示了这个库的基本使用场景：

```js
import React, { useState } from "react";
import { View, Text, StyleSheet, SafeAreaView } from 'react-native';
import { DragSortableView } from 'react-native-drag-sort';

const Dragsort = () => {
  const [data, setData] = useState([
    {
      id: 1,
      title: "固定任务 1",
    },
    {
      id: 2,
      title: "固定任务 2",
    },
    {
      id: 3,
      title: "任务 3",
    },
    {
      id: 4,
      title: "任务 4",
    },
    {
      id: 5,
      title: "任务 5",
    },
    {
      id: 6,
      title: "任务 6",
    },
    {
      id: 7,
      title: "任务 7",
    },
    {
      id: 8,
      title: "任务 8",
    },
  ]);

  return (
    <SafeAreaView style={{ flex: 1 }}>
      <View style={styles.header}>
            <Text style={styles.header_title}>DragSortableView</Text>
      </View>
      <DragSortableView
        dataSource={data}
        parentWidth={400}
        childrenWidth={100}
        childrenHeight={50}
        marginChildrenTop={5}
        marginChildrenBottom={5}
        marginChildrenLeft={5}
        marginChildrenRight={5}
        // onDataChange={setData}
        keyExtractor={(item, index) => item.id}
        onClickItem={(data, item, index) => {
          console.log("点击了第", index, "个元素");
        }}
        onDragStart={() => console.log('Drag started')}
        onDragEnd={() => console.log('Drag end')}
        onDataChange={() => {
          console.log("数据发生变化");
        }}
        fixedItems={[0, 1]}
        delayLongPress={100}
        isDragFreely={true}
        maxScale={1.2}
        minOpacity={0.7}
        renderItem={(item, index) => {
          return (
            <View
              key={item.id}
              style={styles.box}
            >
              <Text style={styles.text}>{item.title}</Text>
            </View>
          );
        }}
        sortable={true}

      />
    </SafeAreaView>
  );
};

const styles = StyleSheet.create({
  box: {
    // position:'relative',
    // flexDirection: "column",
    justifyContent: "center",
    alignContent: "center",
    borderRadius: 5,
    margin: 20,
    backgroundColor: '#4e71f2',
    height: 50,
    width: 100,
  },
  text: {
    fontSize: 18,
    color: '#fff',
    textAlign: 'center'
  },
  header: {
    height: 48,
    justifyContent: 'center',
    alignItems: 'center',
    borderBottomColor: '#2ecc71',
    borderBottomWidth: 2,
  },
  header_title: {
    color: '#333',
    fontSize: 24,
    fontWeight: 'bold',
  }
})
export default Dragsort;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio(构建版本：4.1.3.500) 和 手机 ROM(HarmonyOS NEXT)。

### 权限要求（如有）

## API（AutoDragSortableView、DragSortableView）

**isRequired if there is a * in the name field**

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> 详情见 [react-native-drag-sort 源库地址](https://github.com/mochixuan/react-native-drag-sort)

|           Name           |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :----------------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|     **dataSource** *     |                                                              |  array   |   Yes    | iOS/Android |        Yes        |
|     **parentWidth**      |                         parent width                         |  number  |    No    | iOS/Android |        Yes        |
|   **childrenHeight** *   |                       Each item height                       |  number  |   Yes    | iOS/Android |        Yes        |
|   **childrenWidth** *    |                       Each item width                        |  number  |   Yes    | iOS/Android |        Yes        |
|  **marginChildrenTop**   | So the item's outermost view adds margin, you can only use this method. |  number  |    No    | iOS/Android |        Yes        |
| **marginChildrenBottom** |                                                              |  number  |    No    | iOS/Android |        Yes        |
|  **marginChildrenLeft**  |                                                              |  number  |    No    | iOS/Android |        Yes        |
| **marginChildrenRight**  |                                                              |  number  |    No    | iOS/Android |        Yes        |
|       **sortable**       |                    Do not allow dragging                     |   bool   |    No    | iOS/Android |        Yes        |
|     **onClickItem**      |                            click                             | function |    No    | iOS/Android |        Yes        |
|     **onDragStart**      |                                                              | function |    No    | iOS/Android |        Yes        |
|      **onDragEnd**       |                                                              | function |    No    | iOS/Android |        Yes        |
|     **onDataChange**     |      This method is called every time the data changes.      | function |    No    | iOS/Android |        Yes        |
|     **renderItem** *     |                       render item view                       | function |   Yes    | iOS/Android |        Yes        |
|      **fixedItems**      |                          no remove                           |  array   |    No    | iOS/Android |        Yes        |
|     **keyExtractor**     |                     (item,index) => key                      | function |    No    | iOS/Android |        Yes        |
|    **delayLongPress**    |                                                              |  number  |    No    | iOS/Android |        Yes        |
|     **isDragFreely**     |               Whether to limit the drag space                |   bool   |    No    | iOS/Android |        Yes        |
|      **onDragging**      |                                                              | function |    No    | iOS/Android |        Yes        |
|       **maxScale**       |                                                              |  number  |    No    | iOS/Android |        Yes        |
|      **minOpacity**      |                                                              |  number  |    No    | iOS/Android |        Yes        |

#### The following attributes belong only to AutoDragSortableView

|           Name            | Description |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :---------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **scaleDuration**     |             |                          number                          |    No    | iOS/Android |        Yes        |
|     **slideDuration**     |             |                          number                          |    No    | iOS/Android |        Yes        |
|     **autoThrottle**      |             |                          number                          |    No    | iOS/Android |        Yes        |
| **autoThrottleDuration**  |             |                          number                          |    No    | iOS/Android |        Yes        |
|   **renderHeaderView**    |             |                         element                          |    No    | iOS/Android |        Yes        |
|   **headerViewHeight**    |             |                          number                          |    No    | iOS/Android |        Yes        |
| **scrollIndicatorInsets** |             | ({top:number, left:number, bottom:number, right:number}) |    No    | iOS/Android |        Yes        |
|   **renderBottomView**    |             |                         element                          |    No    | iOS/Android |        Yes        |
|   **bottomViewHeight**    |             |                          number                          |    No    | iOS/Android |        Yes        |
|   **onScrollListener**    |             |          (event: NativeSyntheticEvent) => void           |    No    | iOS/Android |        Yes        |
|      **onScrollRef**      |             |                    (ref: any) => void                    |    No    | iOS/Android |        Yes        |

## **API（AnySizeDragSortableView）**

|           Name            |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
| :-----------------------: | :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **renderItem** *      |                 render item view                  |                         function                         |   Yes    | iOS/Android |        Yes        |
|     **onDataChange**      | This method is called every time the data changes |                         function                         |    No    | iOS/Android |        Yes        |
|   **renderHeaderView**    |                                                   |                         element                          |    No    | iOS/Android |        Yes        |
|   **headerViewHeight**    |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
|   **bottomViewHeight**    |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
|     **autoThrottle**      |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
| **autoThrottleDuration**  |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
| **scrollIndicatorInsets** |                                                   | ({top:number, left:number, bottom:number, right:number}) |    No    | iOS/Android |        Yes        |
|   **onScrollListener**    |                                                   |          (event: NativeSyntheticEvent) => void           |    No    | iOS/Android |        Yes        |
|      **onScrollRef**      |                                                   |                    (ref: any) => void                    |    No    | iOS/Android |        Yes        |
|   **areaOverlapRatio**    |             Must be greater than 0.5              |                          number                          |    No    | iOS/Android |        Yes        |
|    **movedWrapStyle**     |                       style                       |                        StyleProp                         |    No    | iOS/Android |        Yes        |
|    **childMarginTop**     |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
|   **childMarginBottom**   |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
|    **childMarginLeft**    |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
|   **childMarginRight**    |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
| **autoThrottleDuration**  |                                                   |                          number                          |    No    | iOS/Android |        Yes        |
|       **onDragEnd**       |                                                   |                         function                         |    No    | iOS/Android |        Yes        |
|     **dataSource** *      |                                                   |                          array                           |   Yes    | iOS/Android |        Yes        |
|     **keyExtractor**      |                (item,index) => key                |                   function.isRequired                    |    No    | iOS/Android |        Yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The Apache License (Apache)](https://github.com/mochixuan/react-native-drag-sort/blob/master/LICENSE) ，请自由地享受和参与开源。