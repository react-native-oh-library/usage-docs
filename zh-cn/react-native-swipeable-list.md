> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-swipeable-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/esthor/react-native-swipeable-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/esthor/react-native-swipeable-list/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/esthor/react-native-swipeable-list)

## 安装与使用

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-swipeable-list@0.1.2
```

#### **yarn**

```bash
yarn add react-native-swipeable-list@0.1.2
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import {
  SafeAreaView,
  StyleSheet,
  View,
  Text,
  StatusBar,
  Pressable,
  Alert,
} from "react-native";

import SwipeableFlatList from "react-native-swipeable-list";

type DummyDataItem = {
  name: String,
  subject: String,
  date: String,
  text: String,
  id: Number,
};

type DummyDataArray = DummyDataItem[];

const dummyData: DummyDataArray = [
  {
    name: "Raphael",
    subject: "amet lorem semper auctor. Mauris vel turpis.",
    date: "Sun, 17th, 2019",
    text: "mollis dui, in sodales elit erat vitae risus. Duis a mi fringilla mi lacinia mattis. Integer eu lacus. Quisque imperdiet, erat nonummy ultricies ornare, elit elit fermentum risus, at fringilla purus mauris a nunc. In at pede. Cras vulputate velit eu sem. Pellentesque ut ipsum ac mi eleifend egestas. Sed",
    id: 1,
  },
  {
    name: "Aquila",
    subject: "quis, pede. Praesent",
    date: "Thu, 11th, 2019",
    text: "Nunc quis arcu vel quam dignissim pharetra. Nam ac nulla. In tincidunt congue turpis. In condimentum. Donec at arcu. Vestibulum ante ipsum primis in faucibus orci luctus et ultrices posuere cubilia Curae; Donec tincidunt. Donec vitae erat vel pede blandit congue. In scelerisque scelerisque dui. Suspendisse ac",
    id: 11,
  },
  {
    name: "Geraldine",
    subject: "purus sapien, gravida non,",
    date: "Tue, 24th, 2019",
    text: "pede, nonummy ut, molestie in, tempus eu, ligula. Aenean euismod mauris eu elit. Nulla facilisi. Sed neque. Sed eget lacus. Mauris non dui nec urna suscipit nonummy. Fusce fermentum",
    id: 21,
  },
  {
    name: "Geraldine",
    subject: "nec enim. Nunc ut erat. Sed nunc",
    date: "Thu, 5th, 2020",
    text: "Ut tincidunt vehicula risus. Nulla eget metus eu erat semper rutrum. Fusce dolor quam, elementum at, egestas a, scelerisque sed, sapien. Nunc pulvinar arcu et pede. Nunc sed orci lobortis augue scelerisque mollis. Phasellus libero mauris, aliquam eu, accumsan sed, facilisis vitae, orci. Phasellus dapibus quam quis diam.",
    id: 31,
  },
  {
    name: "Mariko",
    subject: "lobortis mauris. Suspendisse",
    date: "Sat, 25th, 2019",
    text: "mauris sit amet lorem semper auctor. Mauris vel turpis. Aliquam adipiscing lobortis risus. In mi pede, nonummy ut, molestie in, tempus eu, ligula. Aenean euismod mauris eu elit. Nulla facilisi. Sed neque. Sed",
    id: 41,
  },
  {
    name: "Nicole",
    subject: "egestas.",
    date: "Tue, 8th, 2020",
    text: "vitae mauris sit amet lorem semper auctor. Mauris vel turpis. Aliquam adipiscing lobortis risus. In mi pede, nonummy ut, molestie in, tempus eu, ligula. Aenean euismod",
    id: 51,
  },
  {
    name: "Solomon",
    subject: "ac mattis ornare, lectus",
    date: "Fri, 10th, 2019",
    text: "nulla. In tincidunt congue turpis. In condimentum. Donec at arcu. Vestibulum ante ipsum primis in faucibus orci",
    id: 61,
  },
  {
    name: "Diana",
    subject: "Suspendisse",
    date: "Sun, 16th, 2018",
    text: "dignissim magna a tortor. Nunc commodo auctor velit. Aliquam nisl. Nulla eu neque pellentesque massa lobortis ultrices. Vivamus rhoncus. Donec est. Nunc ullamcorper,",
    id: 71,
  },
  {
    name: "Hammett",
    subject: "eu enim. Etiam imperdiet dictum",
    date: "Mon, 11th, 2019",
    text: "molestie sodales. Mauris blandit enim consequat purus. Maecenas libero est, congue a, aliquet vel, vulputate eu, odio.",
    id: 81,
  },
  {
    name: "Brenna",
    subject: "neque. Sed eget lacus. Mauris non",
    date: "Wed, 22nd, 2019",
    text: "sit amet massa. Quisque porttitor eros nec tellus. Nunc lectus pede, ultrices a, auctor non, feugiat nec, diam.",
    id: 91,
  },
  {
    name: "Zelda",
    subject: "enim non nisi.",
    date: "Sat, 27th, 2020",
    text: "dignissim pharetra. Nam ac nulla. In tincidunt congue turpis. In condimentum. Donec at arcu. Vestibulum ante ipsum primis in faucibus orci luctus et",
    id: 101,
  },
  {
    name: "Irene",
    subject: "aptent taciti sociosqu ad litora torquent per",
    date: "Wed, 8th, 2020",
    text: "eget metus eu erat semper rutrum. Fusce dolor quam, elementum at, egestas a, scelerisque sed, sapien. Nunc pulvinar arcu et pede. Nunc sed orci lobortis augue scelerisque mollis. Phasellus libero mauris, aliquam eu, accumsan sed, facilisis vitae, orci. Phasellus dapibus quam quis diam.",
    id: 111,
  },
  {
    name: "Dennis",
    subject: "neque venenatis lacus.",
    date: "Mon, 26th, 2018",
    text: "Mauris blandit enim consequat purus. Maecenas libero est, congue a, aliquet vel, vulputate eu, odio. Phasellus at augue id ante",
    id: 121,
  },
  {
    name: "Slade",
    subject: "dolor dolor, tempus non, lacinia at,",
    date: "Mon, 29th, 2020",
    text: "aliquet libero. Integer in magna. Phasellus dolor elit, pellentesque a, facilisis non, bibendum sed, est. Nunc laoreet lectus",
    id: 131,
  },
  {
    name: "Yvonne",
    subject: "enim. Suspendisse aliquet, sem ut",
    date: "Wed, 23rd, 2019",
    text: "lacus. Quisque purus sapien, gravida non, sollicitudin a, malesuada id, erat. Etiam vestibulum massa rutrum magna. Cras convallis convallis dolor.",
    id: 141,
  },
  {
    name: "Ayanna",
    subject: "Suspendisse dui. Fusce diam",
    date: "Fri, 15th, 2019",
    text: "nec, mollis vitae, posuere at, velit. Cras lorem lorem, luctus ut, pellentesque eget, dictum placerat, augue. Sed molestie. Sed id risus quis diam luctus lobortis. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos hymenaeos. Mauris ut quam vel sapien imperdiet",
    id: 151,
  },
  {
    name: "Jasmine",
    subject: "Donec fringilla. Donec feugiat metus sit amet",
    date: "Fri, 8th, 2019",
    text: "odio, auctor vitae, aliquet nec, imperdiet nec, leo. Morbi neque tellus, imperdiet non, vestibulum nec, euismod in, dolor. Fusce feugiat. Lorem ipsum dolor sit amet, consectetuer adipiscing elit.",
    id: 161,
  },
];

const darkColors = {
  background: "#121212",
  primary: "#BB86FC",
  primary2: "#3700b3",
  secondary: "#03DAC6",
  onBackground: "#FFFFFF",
  error: "#CF6679",
};

const colorEmphasis = {
  high: 0.87,
  medium: 0.6,
  disabled: 0.38,
};

const extractItemKey = (item) => {
  return item.id.toString();
};

const Item = ({ item, backgroundColor, textColor, deleteItem }) => {
  return (
    <>
      <View style={styles.item}>
        <View style={styles.avatar} />
        <View style={styles.messageContainer}>
          <Text style={styles.name} numberOfLines={1}>
            {item.name}
          </Text>
          <Text style={styles.subject} numberOfLines={1}>
            Subject: {item.subject}
          </Text>
          <Text style={styles.text} numberOfLines={2}>
            {item.text}
          </Text>
        </View>
      </View>
      <View />
    </>
  );
};

function renderItemSeparator() {
  return <View style={styles.itemSeparator} />;
}

const App = () => {
  const [data, setData] = useState(dummyData);

  const deleteItem = (itemId) => {
    // ! Please don't do something like this in production. Use proper state management.
    const newState = [...data];
    const filteredState = newState.filter((item) => item.id !== itemId);
    return setData(filteredState);
  };

  const archiveItem = (itemId) => {
    Alert.alert(
      "DISHONESTY ALERT",
      "Not gonna Archive it. We're actually are gonna just delete it.",
      [
        {
          text: "Just delete it?",
          onPress: () => deleteItem(itemId),
          style: "destructive",
        },
        {
          text: "Cancel",
          onPress: () => console.log("Cancel Pressed"),
          style: "cancel",
        },
      ]
    );
  };

  const snoozeItem = (itemId) => {
    Alert.alert(
      "DISHONESTY ALERT",
      "Not gonna Snooze it. We're actually are gonna just delete it.",
      [
        {
          text: "Just delete it?",
          onPress: () => deleteItem(itemId),
          style: "destructive",
        },
        {
          text: "Cancel",
          onPress: () => console.log("Cancel Pressed"),
          style: "cancel",
        },
      ]
    );
  };

  const QuickActions = (index, qaItem) => {
    return (
      <View style={styles.qaContainer}>
        <View style={[styles.button, styles.button1]}>
          <Pressable onPress={() => archiveItem(qaItem.id)}>
            <Text style={[styles.buttonText, styles.button1Text]}>Archive</Text>
          </Pressable>
        </View>
        <View style={[styles.button, styles.button2]}>
          <Pressable onPress={() => snoozeItem(qaItem.id)}>
            <Text style={[styles.buttonText, styles.button2Text]}>Snooze</Text>
          </Pressable>
        </View>
        <View style={[styles.button, styles.button3]}>
          <Pressable onPress={() => deleteItem(qaItem.id)}>
            <Text style={[styles.buttonText, styles.button3Text]}>Delete</Text>
          </Pressable>
        </View>
      </View>
    );
  };

  return (
    <>
      <StatusBar barStyle="dark-content" />
      <SafeAreaView style={styles.container}>
        <View style={styles.headerContainer}>
          <Text style={styles.headerText}>Inbox</Text>
        </View>
        <SwipeableFlatList
          keyExtractor={extractItemKey}
          data={data}
          renderItem={({ item }) => (
            <Item item={item} deleteItem={() => deleteItem} />
          )}
          maxSwipeDistance={240}
          renderQuickActions={({ index, item }) => QuickActions(index, item)}
          contentContainerStyle={styles.contentContainerStyle}
          shouldBounceOnMount={true}
          ItemSeparatorComponent={renderItemSeparator}
        />
      </SafeAreaView>
    </>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: "#121212",
  },
  headerContainer: {
    height: 80,
    justifyContent: "center",
    alignItems: "center",
    paddingTop: 10,
  },
  headerText: {
    fontSize: 30,
    fontWeight: "800",
    color: darkColors.onBackground,
    opacity: colorEmphasis.high,
  },
  item: {
    backgroundColor: "#121212",
    height: 80,
    flexDirection: "row",
    padding: 10,
  },
  messageContainer: {
    backgroundColor: darkColors.backgroundColor,
    maxWidth: 300,
  },
  name: {
    fontSize: 16,
    color: darkColors.primary,
    opacity: colorEmphasis.high,
    fontWeight: "800",
  },
  subject: {
    fontSize: 14,
    color: darkColors.onBackground,
    opacity: colorEmphasis.high,
    fontWeight: "bold",
    textShadowColor: darkColors.secondary,
    textShadowOffset: { width: 1, height: 1 },
    textShadowRadius: 4,
  },
  text: {
    fontSize: 10,
    color: darkColors.onBackground,
    opacity: colorEmphasis.medium,
  },
  avatar: {
    width: 40,
    height: 40,
    backgroundColor: darkColors.onBackground,
    opacity: colorEmphasis.high,
    borderColor: darkColors.primary,
    borderWidth: 1,
    borderRadius: 20,
    marginRight: 7,
    alignSelf: "center",
    shadowColor: darkColors.secondary,
    shadowOffset: { width: 1, height: 1 },
    shadowRadius: 2,
    shadowOpacity: colorEmphasis.high,
  },
  itemSeparator: {
    height: StyleSheet.hairlineWidth,
    backgroundColor: darkColors.onBackground,
    opacity: colorEmphasis.medium,
  },
  qaContainer: {
    flex: 1,
    flexDirection: "row",
    justifyContent: "flex-end",
  },
  button: {
    width: 80,
    alignItems: "center",
    justifyContent: "center",
  },
  buttonText: {
    fontWeight: "bold",
    opacity: colorEmphasis.high,
  },
  button1Text: {
    color: darkColors.primary,
  },
  button2Text: {
    color: darkColors.secondary,
  },
  button3Text: {
    color: darkColors.error,
  },
  contentContainerStyle: {
    flexGrow: 1,
    backgroundColor: darkColors.backgroundColor,
  },
});

export default App;
```

## 约束与限制

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.27; SDK：HarmonyOS NEXT Developer Beta1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## 属性

SwipeableFlatList 组件接收所有[React Native FlatList](https://facebook.github.io/react-native/docs/flatlist)组件的 Props.

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                                                                                                                                  | Type      | Required | Platform    | HarmonyOS Support |
| ------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------- | -------- | ----------- | ----------------- |
| data                | An array (or array-like list) of items to render.                                                                                                                                            | ArrayLike | yes      | iOS/Android | yes               |
| renderItem          | Takes an item from data and renders it into the list.                                                                                                                                        | function  | yes      | iOS/Android | yes               |
| shouldBounceOnMount | To alert the user that swiping is possible, the first row can bounce on component mount(default = `true`）.                                                                                  | boolean   | no       | iOS/Android | yes               |
| maxSwipeDistance    | Maximum distance to open to after a swipe.                                                                                                                                                   | number    | no       | iOS/Android | yes               |
| renderQuickActions  | Callback method to render the view that will be unveiled on swipe. Type `renderItemType` (which provides `index` and `item`, which will be very useful for performing actions on your items. | function  | yes      | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/esthor/react-native-swipeable-list/blob/main/LICENSE) ，请自由地享受和参与开源。

