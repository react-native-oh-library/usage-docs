<!-- {% raw %} -->
> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-swipe-list-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jemise111/react-native-swipe-list-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-swipe-list-view/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-swipe-list-view)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-swipe-list-view](https://github.com/react-native-oh-library/react-native-swipe-list-view/releases/)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install --save @react-native-oh-tpl/react-native-swipe-list-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-swipe-list-view@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import { SwipeListView } from 'react-native-swipe-list-view';

//... note: your data array objects MUST contain a key property
//          or you must pass a keyExtractor to the SwipeListView to ensure proper functionality
//          see: https://reactnative.dev/docs/flatlist#keyextractor

  this.state.listViewData = Array(20)
    .fill("")
    .map((_, i) => ({ key: `${i}`, text: `item #${i}` }));

//...
render() {
    return (
        <SwipeListView
            data={this.state.listViewData}
            renderItem={ (data, rowMap) => (
                <View style={styles.rowFront}>
                    <Text>I am {data.item.text} in a SwipeListView</Text>
                </View>
            )}
            renderHiddenItem={ (data, rowMap) => (
                <View style={styles.rowBack}>
                    <Text>Left</Text>
                    <Text>Right</Text>
                </View>
            )}
            leftOpenValue={75}
            rightOpenValue={-75}
        />
    )
}
```

完整使用案例如下：

```jsx
import React, { useState } from "react";
import {
  StyleSheet,
  Text,
  TouchableOpacity,
  TouchableHighlight,
  View,
} from "react-native";

import { SwipeListView } from "react-native-swipe-list-view";

export default function Basic() {
  const [listData, setListData] = useState(
    Array(20)
      .fill("")
      .map((_, i) => ({ key: `${i}`, text: `item #${i}` })),
  );

  const closeRow = (rowMap, rowKey) => {
    if (rowMap[rowKey]) {
      rowMap[rowKey].closeRow();
    }
  };

  const deleteRow = (rowMap, rowKey) => {
    closeRow(rowMap, rowKey);
    const newData = [...listData];
    const prevIndex = listData.findIndex((item) => item.key === rowKey);
    newData.splice(prevIndex, 1);
    setListData(newData);
  };

  const onRowDidOpen = (rowKey) => {
    console.log("This row opened", rowKey);
  };

  const renderItem = (data) => (
    <TouchableHighlight
      onPress={() => console.log("You touched me")}
      style={styles.rowFront}
      underlayColor={"#AAA"}
    >
      <View>
        <Text>I am {data.item.text} in a SwipeListView</Text>
      </View>
    </TouchableHighlight>
  );

  const renderHiddenItem = (data, rowMap) => (
    <View style={styles.rowBack}>
      <Text>Left</Text>
      <TouchableOpacity
        style={[styles.backRightBtn, styles.backRightBtnLeft]}
        onPress={() => closeRow(rowMap, data.item.key)}
      >
        <Text style={styles.backTextWhite}>Close</Text>
      </TouchableOpacity>
      <TouchableOpacity
        style={[styles.backRightBtn, styles.backRightBtnRight]}
        onPress={() => deleteRow(rowMap, data.item.key)}
      >
        <Text style={styles.backTextWhite}>Delete</Text>
      </TouchableOpacity>
    </View>
  );

  return (
    <View style={styles.container}>
      <SwipeListView
        data={listData}
        renderItem={renderItem}
        renderHiddenItem={renderHiddenItem}
        leftOpenValue={75}
        rightOpenValue={-150}
        previewRowKey={"0"}
        previewOpenValue={-40}
        previewOpenDelay={3000}
        onRowDidOpen={onRowDidOpen}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: "white",
    flex: 1,
  },
  backTextWhite: {
    color: "#FFF",
  },
  rowFront: {
    alignItems: "center",
    backgroundColor: "#CCC",
    borderBottomColor: "black",
    borderBottomWidth: 1,
    justifyContent: "center",
    height: 50,
  },
  rowBack: {
    alignItems: "center",
    backgroundColor: "#DDD",
    flex: 1,
    flexDirection: "row",
    justifyContent: "space-between",
    paddingLeft: 15,
  },
  backRightBtn: {
    alignItems: "center",
    bottom: 0,
    justifyContent: "center",
    position: "absolute",
    top: 0,
    width: 75,
  },
  backRightBtnLeft: {
    backgroundColor: "blue",
    right: 75,
  },
  backRightBtnRight: {
    backgroundColor: "red",
    right: 0,
  },
});
```

## 兼容性

在以下版本验证通过

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

## 属性

**SwipeListView**

| Name                                 | Description                                                                                                                                                                                                                                                                                                                                                                                      | Type     | Required | Platform      | HarmonyOS Support |
| ------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------- | -------- | ------------- | ----------------- |
| data                                 | List of objects to be passed into the `renderItem` and `renderHiddenItem` functions. Each item must include a unique `key` property or `keyExtractor` must be implemented to ensure full functionality.                                                                                                                                                                                          | array    | YES      | Android IOS   | YES               |
| useSectionList                       | Render list using React Native's `SectionList`                                                                                                                                                                                                                                                                                                                                                   | bool     | NO       | Android IOS   | YES               |
| renderItem                           | How to render a row in a FlatList. Should return a valid React Element.                                                                                                                                                                                                                                                                                                                          | func     | YES      | Android IOS   | YES               |
| renderHiddenItem                     | How to render a hidden row in a FlatList (renders behind the row). Should return a valid React Element. This is required unless `renderItem` returns a `<SwipeRow>` (see [Per Row Behavior](https://github.com/jemise111/react-native-swipe-list-view/blob/master/docs/per-row-behavior.md)).                                                                                                    | func     | YES      | Android IOS   | YES               |
| leftOpenValue                        | TranslateX value for opening the row to the left (positive number)                                                                                                                                                                                                                                                                                                                               | number   | NO       | Android IOS   | YES               |
| rightOpenValue                     | TranslateX value for opening the row to the right (negative number)                                                                                                                                                                                                                                                                                                                              | number | NO       | Android IOS   | YES               |
| leftActivationValue                | TranslateX value for firing onLeftActionStatusChange (positive number)                                                                                                                                                                                                                                                                                                                           | number | NO       | Android IOS      | NO                |
| rightActivationValue               | TranslateX value for firing onRightActionStatusChange (negative number)                                                                                                                                                                                                                                                                                                                          | number | NO       | Android IOS   | YES               |
| rightActionValue                   | TranslateX value for right action to which the row will be shifted after gesture release                                                                                                                                                                                                                                                                                                         | number | NO       | Android IOS   | YES               |
| initialLeftActionState             | Initial value for left action state (default is false)                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android IOS   | YES               |
| initialRightActionState            | Initial value for right action state (default is false)                                                                                                                                                                                                                                                                                                                                          | bool   | NO       | Android IOS   | YES               |
| closeOnRowPress                    | Should open rows be closed when a row is pressed                                                                                                                                                                                                                                                                                                                                                 | bool   | NO       | Android IOS | YES               |
| closeOnRowOpen                     | Should open rows be closed when another row is opened                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android IOS   | YES               |
| closeOnRowBeginSwipe               | Should open rows be closed when a row begins to swipe open                                                                                                                                                                                                                                                                                                                                       | bool   | NO       | Android IOS | YES               |
| closeOnScroll                      | Should open rows be closed when the listView begins scrolling                                                                                                                                                                                                                                                                                                                                    | bool   | NO       | Android IOS   | YES               |
| disableLeftSwipe                   | Disable ability to swipe the row left                                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android IOS   | YES               |
| disableRightSwipe                  | Disable ability to swipe the row right                                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android IOS   | YES               |
| stopLeftSwipe                      | TranslateX value for stop the row to the left (positive number). This number is the stop value corresponding to the leftOpenValue (while the row is swiping in the right direction)                                                                                                                                                                                                            | number | NO       | Android IOS   | YES               |
| stopRightSwipe                     | TranslateX value for stop the row to the right (negative number). This number is the stop value corresponding to the rightOpenValue (while the row is swiping in the left direction)                                                                                                                                                                                                           | number | NO       | Android IOS   | YES               |
| directionalDistanceChangeThreshold | Change the sensitivity of the row                                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android IOS   | YES               |
| swipeToOpenPercent                 | What % of the left/right openValue does the user need to swipe past to trigger the row opening.                                                                                                                                                                                                                                                                                                  | number | NO       | Android IOS   | YES               |
| swipeToClosePercent                | What % of the left/right openValue does the user need to swipe past to trigger the row closing.                                                                                                                                                                                                                                                                                                  | number | NO       | Android IOS   | YES               |
| swipeToOpenVelocityContribution    | Describes how much the ending velocity of the gesture affects whether the swipe will result in the item being closed or open. A velocity factor of 0 (the default) means that the velocity will have no bearing on whether the swipe settles on a closed or open position and it'll just take into consideration the swipeToOpenPercent. Ideal values for this prop tend to be between 5 and 15. | number | NO       | Android IOS   | YES               |

**SwipeRow**

| Name                                 | Description                                                                                                                                                                                                                                                                                                                                                                                      | Type     | Required | Platform      | HarmonyOS Support |
|:------------------------------------:|:------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------:|:--------:|:--------:|:-------------:| ----------------- |
| closeOnRowPress                    | Should the row be closed when it is tapped                                                                                                                                                                                                                                                                                                                                                       | bool   | NO       | Android IOS   | YES               |
| directionalDistanceChangeThreshold | Change the sensitivity of the row                                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android IOS   | YES               |
| friction                           | Friction for the open / close animation. Controls "bounciness"/overshoot. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                           | number | NO       | Android IOS   | YES               |
| tension                            | Tension for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                                             | number | NO       | Android IOS | YES               |
| restSpeedThreshold                 | RestSpeedThreshold for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                                  | number | NO       | Android IOS | YES               |
| restDisplacementThreshold          | RestDisplacementThreshold for the open / close animation. Controls speed. https://facebook.github.io/react-native/docs/animated#spring                                                                                                                                                                                                                                                           | number | NO       | Android IOS   | YES               |
| leftOpenValue                      | TranslateX value for opening the row to the left (positive number)                                                                                                                                                                                                                                                                                                                               | number | YES      | Android IOS | YES               |
| rightOpenValue                     | TranslateX value for opening the row to the right (negative number)                                                                                                                                                                                                                                                                                                                              | number | YES      | Android IOS | YES               |
| leftActivationValue                | TranslateX value for firing onLeftActionStatusChange (positive number)                                                                                                                                                                                                                                                                                                                           | number | NO       | Android IOS   | YES               |
| rightActivationValue               | TranslateX value for firing onRightActionStatusChange (negative number)                                                                                                                                                                                                                                                                                                                          | number | NO       | Android IOS   | YES               |
| initialLeftActionState             | Initial value for left action state (default is false)                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android IOS   | YES               |
| initialRightActionState`           | Initial value for right action state (default is false)                                                                                                                                                                                                                                                                                                                                          | bool   | NO       | Android IOS   | YES               |
| leftActionValue                    | TranslateX value for left action to which the row will be shifted after gesture release                                                                                                                                                                                                                                                                                                          | number | NO       | Android IOS   | YES               |
| rightActionValue                   | TranslateX value for right action to which the row will be shifted after gesture release                                                                                                                                                                                                                                                                                                         | number | NO       | Android IOS   | YES               |
| stopLeftSwipe                      | TranslateX value for stop the row to the left (positive number). This number is the stop value corresponding to the leftOpenValue (while the row is swiping in the right direction)                                                                                                                                                                                                            | number | NO       | Android IOS   | YES               |
| stopRightSwipe                     | TranslateX value for stop the row to the right (negative number). This number is the stop value corresponding to the rightOpenValue (while the row is swiping in the left direction)                                                                                                                                                                                                           | number | NO       | Android IOS   | YES               |
| onRowPress                         | Called when row is pressed.                                                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android IOS   | YES               |
| onRowOpen                          | Called when row is animating open. Used by the SwipeListView to keep references to open rows.                                                                                                                                                                                                                                                                                                    | func   | NO       | Android IOS   | YES               |
| onRowDidOpen                       | Called when row has animated open                                                                                                                                                                                                                                                                                                                                                                | func   | NO       | Android IOS   | YES               |
| onRowClose                         | Called when row is animating closed                                                                                                                                                                                                                                                                                                                                                              | func   | NO       | Android IOS   | YES               |
| onRowDidClose                      | Called when a swipe row has animated closed                                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android IOS   | YES               |
| onLeftActionStatusChange           | Called once when swipe value crosses the leftActivationValue                                                                                                                                                                                                                                                                                                                                     | func   | NO       | Android IOS   | YES               |
| onRightActionStatusChange          | Called once when swipe value crosses the rightActivationValue                                                                                                                                                                                                                                                                                                                                    | func   | NO       | Android IOS   | YES               |
| onLeftAction                       | Called when row shifted to leftActivationValue                                                                                                                                                                                                                                                                                                                                                   | func   | NO       | Android IOS   | YES               |
| onRightAction                      | Called when row shifted to rightActivationValue                                                                                                                                                                                                                                                                                                                                                  | func   | NO       | Android IOS   | YES               |
| swipeToOpenPercent                 | What % of the left/right openValue does the user need to swipe past to trigger the row opening.                                                                                                                                                                                                                                                                                                  | number | NO       | Android IOS   | YES               |
| swipeToClosePercent                | What % of the left/right openValue does the user need to swipe past to trigger the row closing.                                                                                                                                                                                                                                                                                                  | number | NO       | Android IOS   | YES               |
| setScrollEnabled                   | Used by the SwipeListView to close rows on scroll events. You shouldn't need to use this prop explicitly.                                                                                                                                                                                                                                                                                        | func   | NO       | Android IOS   | YES               |
| disableLeftSwipe                   | Disable ability to swipe the row left                                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android IOS   | YES               |
| disableRightSwipe                  | Disable ability to swipe the row right                                                                                                                                                                                                                                                                                                                                                           | bool   | NO       | Android IOS   | YES               |
| recalculateHiddenLayout            | Enable hidden row onLayout calculations to run always                                                                                                                                                                                                                                                                                                                                            | bool   | NO       | Android IOS | YES               |
| style                              | Styles for the parent wrapper View of the SwipeRow                                                                                                                                                                                                                                                                                                                                               | object | YES      | Android IOS   | YES               |
| preview                            | Should the row do a slide out preview to show that it is swipeable                                                                                                                                                                                                                                                                                                                               | bool   | NO       | Android IOS   | YES               |
| previewDuration                    | Duration of the slide out preview animation                                                                                                                                                                                                                                                                                                                                                      | number | NO       | Android IOS   | YES               |
| previewRepeat                      | Should the animation repeat                                                                                                                                                                                                                                                                                                                                                                      | bool   | NO       | Android IOS   | YES               |
| previewRepeatDelay                 | Delay between each preview repeat in milliseconds                                                                                                                                                                                                                                                                                                                                                | number | NO       | Android IOS   | YES               |
| previewOpenValue                   | TranslateX value for the slide out preview animation                                                                                                                                                                                                                                                                                                                                             | number | NO       | Android IOS   | YES               |
| onSwipeValueChange                 | Callback invoked any time the translateX value of the row changes                                                                                                                                                                                                                                                                                                                                | func   | NO       | Android IOS   | YES               |
| swipeGestureBegan                  | Called when the row is animating swipe                                                                                                                                                                                                                                                                                                                                                           | func   | NO       | Android IOS   | YES               |
| swipeGestureEnded                  | Called when user has ended their swipe gesture                                                                                                                                                                                                                                                                                                                                                   | func   | NO       | Android IOS   | YES               |
| swipeToOpenVelocityContribution    | Describes how much the ending velocity of the gesture affects whether the swipe will result in the item being closed or open. A velocity factor of 0 (the default) means that the velocity will have no bearing on whether the swipe settles on a closed or open position and it'll just take into consideration the swipeToOpenPercent. Ideal values for this prop tend to be between 5 and 15. | number | NO       | Android IOS | YES               |
| shouldItemUpdate                   | Callback to determine whether component should update                                                                                                                                                                                                                                                                                                                                            | func   | NO       | Android IOS   | YES               |
| forceCloseToLeftThreshold          | TranslateX amount(not value!) threshold that triggers force-closing the row to the Left End (positive number)                                                                                                                                                                                                                                                                                    | number | NO       | Android IOS   | YES               |
| forceCloseToRightThreshold         | TranslateX amount(not value!) threshold that triggers force-closing the row to the Right End (positive number)                                                                                                                                                                                                                                                                                   | number | NO       | Android IOS   | YES               |
| onForceCloseToLeft                 | Callback invoked when row is force closing to the Left End                                                                                                                                                                                                                                                                                                                                       | func   | NO       | Android IOS   | YES               |
| onForceCloseToRight                | Callback invoked when row is force closing to the Right End                                                                                                                                                                                                                                                                                                                                      | func   | NO       | Android IOS   | YES               |
| onForceCloseToLeftEnd              | Callback invoked when row has finished force closing to the Left End                                                                                                                                                                                                                                                                                                                             | func   | NO       | Android IOS   | YES               |
| onForceCloseToRightEnd             | Callback invoked when row has finished force closing to the Right End                                                                                                                                                                                                                                                                                                                            | func   | NO       | Android IOS   | YES               |
| useNativeDriver                    | useNativeDriver: true for all animations                                                                                                                                                                                                                                                                                                                                                       | bool   | NO       | Android IOS   | YES               |
| swipeKey                           | Optional key to identify a standalone row, used in the onSwipeValueChange callback                                                                                                                                                                                                                                                                                                             | string | NO       | Android IOS   | YES               |
| onPreviewEnd                       | Callback that runs after row swipe preview is finished                                                                                                                                                                                                                                                                                                                                           | func   | NO       | Android IOS   | YES               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-swipe-list-view/blob/sig/LICENSE) ，请自由地享受和参与开源。



<!-- {% endraw %} -->