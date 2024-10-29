> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-drax)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-drax Releases](https://github.com/react-native-oh-library/react-native-drax/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-gesture-handler. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-gesture-handler](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-gesture-handler.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-drax Releases](https://github.com/react-native-oh-library/react-native-drax/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### DraxView

|               Name                |                         Description                          |     Type      | Required |  Platform   | HarmonyOS Support |
| :-------------------------------: | :----------------------------------------------------------: | :-----------: | :------: | :---------: | :---------------: |
|            onDragStart            |          Callback function at the start of dragging          |   function    |    no    | iOS/Android |        Yes        |
|              onDrag               |              Callback function during dragging               |   function    |    no    | iOS/Android |        Yes        |
|            onDragEnter            |           Callback function when a drag is entered           |   function    |    no    | iOS/Android |        Yes        |
|            onDragOver             |       Callback function when dragging the floating top       |   function    |    no    | iOS/Android |        Yes        |
|            onDragExit             |            Callback function when the drag exits             |   function    |    no    | iOS/Android |        Yes        |
|             onDragEnd             |           Callback function at the end of dragging           |   function    |    no    | iOS/Android |        Yes        |
|            onDragDrop             |        Callback function when dragging and releasing         |   function    |    no    | iOS/Android |        Yes        |
|           onSnapbackEnd           |    Callback function at the end of the rebound animation     |   function    |    no    | iOS/Android |        Yes        |
|        onReceiveDragEnter         |           Callback function when a drag is entered           |   function    |    no    | iOS/Android |        Yes        |
|         onReceiveDragOver         |         Callback function when dragging and hovering         |   function    |    no    | iOS/Android |        Yes        |
|         onReceiveDragExit         |            Callback function when the drag exits             |   function    |    no    | iOS/Android |        Yes        |
|         onReceiveDragDrop         |        Callback function when dragging and releasing         |   function    |    no    | iOS/Android |        Yes        |
|        onMonitorDragStart         |    Callback function when the start of a drag is detected    |   function    |    no    | iOS/Android |        Yes        |
|        onMonitorDragEnter         |       Callback function when a drag entry is detected        |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragOver         |         Callback function when dragging is detected          |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragExit         |        Callback function when a drag exit is detected        |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragEnd          |    Callback function when the end of dragging is detected    |   function    |    no    | iOS/Android |        Yes        |
|         onMonitorDragDrop         |      Callback function after a drag release is detected      |   function    |    no    | iOS/Android |        Yes        |
|          animateSnapback          | Whether to animate hovering view snapshots after drag release |    boolean    |    no    | iOS/Android |        Yes        |
|              payload              |                  Data passed when dragging                   |      any      |    no    | iOS/Android |        Yes        |
|            dragPayload            |              Data transferred by the drag party              |      any      |    no    | iOS/Android |        Yes        |
|          receiverPayload          |               Data transferred by the receiver               |      any      |    no    | iOS/Android |        Yes        |
|         dragInactiveStyle         |            Style of the drag side before the drag            |    object     |    no    | iOS/Android |        Yes        |
|           draggingStyle           |      The style applied to the drag side during the drag      |    object     |    no    | iOS/Android |        Yes        |
|     draggingWithReceiverStyle     | The style applied to the drag side when the drag side is directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
|   draggingWithoutReceiverStyle    | The style applied to the drag side when the drag side is not directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
|         dragReleasedStyle         | The style applied to the drag side when the drag side is released |    object     |    no    | iOS/Android |        Yes        |
|            hoverStyle             | Drag sideDrag sideThe style applied to the drag side snapshot when the snapshot is hovered |    object     |    no    | iOS/Android |        Yes        |
|        hoverDraggingStyle         | Drag side The style applied to the drag side snapshot when dragging |    object     |    no    | iOS/Android |        Yes        |
|  hoverDraggingWithReceiverStyle   | The style applied to the snapshot of the drager when the drager is directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
| hoverDraggingWithoutReceiverStyle | The style applied to the drag side snapshot when the drag side is not directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
|      hoverDragReleasedStyle       | Drag side The style applied to the drag side snapshot when the drag stops |    object     |    no    | iOS/Android |        Yes        |
|       receiverInactiveStyle       |  The style applied to the recipient before the drag starts   |    object     |    no    | iOS/Android |        Yes        |
|          receivingStyle           | The style applied to the recipient when the drag is directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
|        otherDraggingStyle         |      Styles applied to the drag side during other drags      |    object     |    no    | iOS/Android |        Yes        |
|  otherDraggingWithReceiverStyle   | The style applied to the drag side when the other drag side is directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
| otherDraggingWithoutReceiverStyle | The style applied to the drag party when the other drag party is not directly above the recipient |    object     |    no    | iOS/Android |        Yes        |
|           renderContent           | Renders the content of the internal subnodes of the drag-and-drop component |   function    |    no    | iOS/Android |        Yes        |
|        renderHoverContent         | Used to render the content of the internal subnodes of the drag-and-drop copy component |   function    |    no    | iOS/Android |        Yes        |
|           registration            | Callback function, which can receive data transferred within the component |   function    |    no    | iOS/Android |        Yes        |
|             onMeasure             | Callback function, which can receive data transferred within the component |   function    |    no    | iOS/Android |        Yes        |
|         lockDragXPosition         | Indicates whether to lock the drag in the horizontal direction (x axis) |    boolean    |    no    | iOS/Android |        Yes        |
|         lockDragYPosition         | Indicates whether to lock the drag in the vertical direction (y axis) |    boolean    |    no    | iOS/Android |        Yes        |
|             children              | Renders the content of the internal subnodes of the drag-and-drop component. This parameter is valid only when the renderContent rendering method does not exist | React Element |    no    | iOS/Android |        Yes        |
|              noHover              |   Sets whether to disable the drag-and-drop copy function    |    boolean    |    no    | iOS/Android |        Yes        |
|          longPressDelay           | Sets the minimum time (in milliseconds) for the view to recognize touch and hold gestures |    number     |    no    | iOS/Android |        Yes        |
|             draggable             | Indicates whether dragging is allowed. The default value is true |    boolean    |    no    | iOS/Android |        Yes        |

###  DraxScrollView

|   Name   |          Description          |     Type      | Required |  Platform   | HarmonyOS Support |
| :------: | :---------------------------: | :-----------: | :------: | :---------: | :---------------: |
| children | Component React Node subnode  | React Element |    no    | iOS/Android |        Yes        |
| onScroll | Sliding event callback method |   function    |    no    | iOS/Android |        Yes        |

### DraxList

|           Name           |                         Description                          |   Type   | Required |  Platform   | HarmonyOS Support |
| :----------------------: | :----------------------------------------------------------: | :------: | :------: | :---------: | :---------------: |
|           data           |            Data source of the DraxList component             |  array   |    no    | iOS/Android |        Yes        |
|      flatListStyle       |      Sets the style of the internal FlatList component       |  object  |    no    | iOS/Android |        Yes        |
|        itemStyles        | Sets the style of an item in the internal FlatList component |  object  |    no    | iOS/Android |        Yes        |
|    renderItemContent     |  Method for Rendering Item Items in the DraxList Component   | function |    no    | iOS/Android |        Yes        |
|  renderItemHoverContent  | Method of Rendering Item Snapshots in the DraxList Component | function |    no    | iOS/Android |        Yes        |
|     onItemDragStart      | Callback is executed when an item in the DraxList component starts to be dragged | function |    no    | iOS/Android |        Yes        |
| onItemDragPositionChange | Callback is executed when the position of an item in the DraxList component changes | function |    no    | iOS/Android |        Yes        |
|      onItemDragEnd       | Callback when the drag of an item in the DraxList component ends | function |    no    | iOS/Android |        Yes        |
|      onItemReorder       | Callback for recording the moving index position of an item  | function |    no    | iOS/Android |        Yes        |
|       reorderable        |           Sets whether to enable automatic sorting           | boolean  |    no    | iOS/Android |        Yes        |
|    viewPropsExtractor    |     Props can be returned based on the data of each item     | function |    no    | iOS/Android |        Yes        |
|         onScroll         |                Sliding event callback method                 | function |    no    | iOS/Android |        Yes        |
|      itemsDraggable      | Indicates whether items in the FlatList component can be dragged | boolean  |    no    | iOS/Android |        Yes        |
| lockItemDragsToMainAxis  | Indicates whether to lock the drag direction of items in the FlatList component to the main axis direction | boolean  |    no    | iOS/Android |        Yes        |

## Known Issues

- [ ] DraxList和DraxScrollView组件存在拖拽不流畅的情况，[issue#1](https://github.com/react-native-oh-library/react-native-drax/issues/1)

## Others

## License

This project is licensed under [The MIT License(MIT)](https://github.com/nuclearpasta/react-native-drax/blob/main/LICENSE.md).
