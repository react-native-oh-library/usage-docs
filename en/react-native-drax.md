> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-drax</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/nuclearpasta/react-native-drax">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/nuclearpasta/react-native-drax/blob/main/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-drax)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-drax Releases](https://github.com/react-native-oh-library/react-native-drax/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-drax@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-drax@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from 'react';
import { View, StyleSheet } from 'react-native';
import { GestureHandlerRootView } from 'react-native-gesture-handler';
import { DraxProvider, DraxView } from 'react-native-drax';


export const GestureHandleExample = () => {
  const viewPropsExtractor = (data: any) => {
    return {
      style: {
        backgroundColor: data.isDragging ? 'lightblue' : 'white',
      },
    };
  };
  return (
    <DraxProvider>
      <GestureHandlerRootView>
        <View style={styles.container}>
          <DraxView
            style={styles.draggable}
            onDragStart={() => {
              console.log('start drag');
            }}
            payload="world"
          />
          <DraxView
            style={styles.receiver}
            onReceiveDragEnter={({ dragged: { payload } }) => {
              console.log(`hello ${payload}`);
            }}
            onReceiveDragExit={({ dragged: { payload } }) => {
              console.log(`goodbye ${payload}`);
            }}
            onReceiveDragDrop={({ dragged: { payload } }) => {
              console.log(`received ${payload}`);
            }}
          />
        </View>
      </GestureHandlerRootView>
    </DraxProvider>
  );
};

const styles = StyleSheet.create({
  box: {
    width: 100,
    height: 100,
    backgroundColor: 'blue',
    marginTop: 100,
    marginLeft: 100
  },
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    width: '100%',
    height: 800,
    paddingTop: 500
  },
  draggable: {
    width: 100,
    height: 100,
    backgroundColor: 'blue',
  },
  receiver: {
    width: 100,
    height: 100,
    backgroundColor: 'green',
  },
});
```

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-gesture-handler 的原生端代码，如已在鸿蒙工程中引入过这个库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-gesture-handler 文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-gesture-handler.md)  进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-drax Releases](https://github.com/react-native-oh-library/react-native-drax/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 Yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### DraxView

|               Name                |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :-------------------------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|            onDragStart            |     Called in the dragged view when a drag action begins     | function |    no    | iOS/Android |        Yes        |
|              onDrag               | Called in the dragged view repeatedly while dragged, not over any receiver | function |    no    | iOS/Android |        Yes        |
|            onDragEnter            | Called in the dragged view when initially dragged over a new receiver | function |    no    | iOS/Android |        Yes        |
|            onDragOver             | Called in the dragged view repeatedly while dragged over a receiver. | function |    no    | iOS/Android |        Yes        |
|            onDragExit             |  Called in the dragged view when dragged off of a receiver   | function |    no    | iOS/Android |        Yes        |
|             onDragEnd             | Called in the dragged view when drag ends not over any receiver or is cancelled | function |    no    | iOS/Android |        Yes        |
|            onDragDrop             |  Called in the dragged view when drag ends over a receiver   | function |    no    | iOS/Android |        Yes        |
|           onSnapbackEnd           |  Called in the dragged view when drag release snapback ends  | function |    no    | iOS/Android |        Yes        |
|        onReceiveDragEnter         | Called in the receiver view each time an item is initially dragged over it | function |    no    | iOS/Android |        Yes        |
|         onReceiveDragOver         | Called in the receiver view repeatedly while an item is dragged over it | function |    no    | iOS/Android |        Yes        |
|         onReceiveDragExit         | Called in the receiver view when item is dragged off of it or drag is cancelled | function |    no    | iOS/Android |        Yes        |
|         onReceiveDragDrop         |      Called in the receiver view when drag ends over it      | function |    no    | iOS/Android |        Yes        |
|        onMonitorDragStart         | Called in the monitor view when a drag action begins over it | function |    no    | iOS/Android |        Yes        |
|        onMonitorDragEnter         | Called in the monitor view each time an item is initially dragged over it | function |    no    | iOS/Android |        Yes        |
|         onMonitorDragOver         | Called in the monitor view repeatedly while an item is dragged over it | function |    no    | iOS/Android |        Yes        |
|         onMonitorDragExit         |  Called in the monitor view when item is dragged off of it   | function |    no    | iOS/Android |        Yes        |
|         onMonitorDragEnd          | Called in the monitor view when drag ends over it while not over any receiver or drag is cancelled | function |    no    | iOS/Android |        Yes        |
|         onMonitorDragDrop         | Called in the monitor view when drag ends over it while over a receiver | function |    no    | iOS/Android |        Yes        |
|          animateSnapback          | Whether or not to animate hover view snapback after drag release, defaults to true | boolean  |    no    | iOS/Android |        Yes        |
|              payload              | Convenience prop to provide one value for both `dragPayload` and `receiverPayload` |   any    |    no    | iOS/Android |        Yes        |
|            dragPayload            | Payload that will be delivered to receiver views when this view is dragged; overrides `payload` |   any    |    no    | iOS/Android |        Yes        |
|          receiverPayload          | Payload that will be delievered to dragged views when this view receives them; overrides `payload` |   any    |    no    | iOS/Android |        Yes        |
|         dragInactiveStyle         | Additional view style applied while this view is not being dragged or released |  object  |    no    | iOS/Android |        Yes        |
|           draggingStyle           | Additional view style applied while this view is being dragged |  object  |    no    | iOS/Android |        Yes        |
|     draggingWithReceiverStyle     | Additional view style applied while this view is being dragged over a receiver |  object  |    no    | iOS/Android |        Yes        |
|   draggingWithoutReceiverStyle    | Additional view style applied while this view is being dragged NOT over a receiver |  object  |    no    | iOS/Android |        Yes        |
|         dragReleasedStyle         | Additional view style applied while this view has just been released from a drag |  object  |    no    | iOS/Android |        Yes        |
|            hoverStyle             | Additional view style applied to the hovering copy of this view during drag/release |  object  |    no    | iOS/Android |        Yes        |
|        hoverDraggingStyle         | Additional view style applied to the hovering copy of this view while dragging |  object  |    no    | iOS/Android |        Yes        |
|  hoverDraggingWithReceiverStyle   | Additional view style applied to the hovering copy of this view while dragging over a receiver |  object  |    no    | iOS/Android |        Yes        |
| hoverDraggingWithoutReceiverStyle | Additional view style applied to the hovering copy of this view while dragging NOT over a receiver |  object  |    no    | iOS/Android |        Yes        |
|      hoverDragReleasedStyle       | Additional view style applied to the hovering copy of this view when just released |  object  |    no    | iOS/Android |        Yes        |
|       receiverInactiveStyle       | Additional view style applied while this view is not receiving a drag |  object  |    no    | iOS/Android |        Yes        |
|          receivingStyle           | Additional view style applied while this view is receiving a drag |  object  |    no    | iOS/Android |        Yes        |
|        otherDraggingStyle         | Additional view style applied to this view while any other view is being dragged |  object  |    no    | iOS/Android |        Yes        |
|  otherDraggingWithReceiverStyle   | Additional view style applied to this view while any other view is being dragged over a receiver |  object  |    no    | iOS/Android |        Yes        |
| otherDraggingWithoutReceiverStyle | Additional view style applied to this view while any other view is being dragged NOT over a receiver |  object  |    no    | iOS/Android |        Yes        |
|           renderContent           |       Custom render function for content of this view        |    /     |    no    | iOS/Android |        Yes        |
|        renderHoverContent         | Custom render function for content of hovering copy of this view, defaults to renderContent |    /     |    no    | iOS/Android |        Yes        |
|           registration            | For external registration of this view, to access internal methods, similar to a ref | function |    no    | iOS/Android |        Yes        |
|             onMeasure             |          For receiving view measurements externally          | function |    no    | iOS/Android |        Yes        |
|         lockDragXPosition         |               If true, lock drag's x-position                | boolean  |    no    | iOS/Android |        Yes        |
|         lockDragYPosition         |               If true, lock drag's y position                | boolean  |    no    | iOS/Android |        Yes        |
|             children              |                React children of the DraxView                |    /     |    no    | iOS/Android |        Yes        |
|              noHover              | If true, do not render hover view copies for this view when dragging | boolean  |    no    | iOS/Android |        Yes        |
|          longPressDelay           | Time in milliseconds view needs to be pressed before drag starts |  number  |    no    | iOS/Android |        Yes        |
|             draggable             |               Whether the view can be dragged                | boolean  |    no    | iOS/Android |        Yes        |

###  DraxScrollView

|   Name   |                  Description                   |   Type   | Required |  Platform   | HarmonyOS Support |
| :------: | :--------------------------------------------: | :------: | :------: | :---------: | :---------------: |
| children |         React children of the DraxView         |    /     |    no    | iOS/Android |        Yes        |
| onScroll | Callback generated when scrolling is triggered | function |    no    | iOS/Android |        Yes        |

### DraxList

|           Name           |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :----------------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|           data           |      Transforms the first character in a capital letter      | boolean  |    no    | iOS/Android |        Yes        |
|      flatListStyle       |            Style prop for the underlying FlatList            |  object  |    no    | iOS/Android |        Yes        |
|        itemStyles        |    Style props to apply to all DraxView items in the list    |  object  |    no    | iOS/Android |        Yes        |
|    renderItemContent     |      Render function for content of an item's DraxView       |    /     |    no    | iOS/Android |        Yes        |
|  renderItemHoverContent  | Render function for content of an item's hovering copy, defaults to renderItemContent |    /     |    no    | iOS/Android |        Yes        |
|     onItemDragStart      | Callback handler for when a list item reorder drag action begins | function |    no    | iOS/Android |        Yes        |
| onItemDragPositionChange | Callback handler for when a list item position (index) changes during a reorder drag | function |    no    | iOS/Android |        Yes        |
|      onItemDragEnd       | Callback handler for when a list item reorder drag action ends | function |    no    | iOS/Android |        Yes        |
|      onItemReorder       | Callback handler for when a list item is moved within the list, reordering the list | function |    no    | iOS/Android |        Yes        |
|       reorderable        | Can the list be reordered by dragging items? Defaults to true if onItemReorder is set | boolean  |    no    | iOS/Android |        Yes        |
|    viewPropsExtractor    | Function that receives an item and returns a list of DraxViewProps to apply to that item's DraxView | function |    no    | iOS/Android |        Yes        |
|         onScroll         |        Callback generated when scrolling is triggered        | function |    no    | iOS/Android |        Yes        |
|      itemsDraggable      |          Can the items be dragged? Defaults to true          | boolean  |    no    | iOS/Android |        Yes        |
| lockItemDragsToMainAxis  |       If true, lock item drags to the list's main axis       | boolean  |    no    | iOS/Android |        Yes        |

## 遗留问题

- [ ] DraxList和DraxScrollView组件存在拖拽不流畅的情况，[issue#1](https://github.com/react-native-oh-library/react-native-drax/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License(MIT)](https://github.com/nuclearpasta/react-native-drax/blob/main/LICENSE.md)，请自由地享受和参与开源。
