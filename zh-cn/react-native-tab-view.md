> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-tab-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-navigation/react-navigation/tree/main/packages/react-native-tab-view">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20web%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-navigation/react-navigation/blob/main/packages/react-native-tab-view/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-navigation/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-tab-view@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-tab-view@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```js
import React from "react";
import { View, Text, Dimensions, StyleSheet } from "react-native";
import {
  TabView,
  TabBar,
  SceneMap,
  NavigationState,
  SceneRendererProps,
} from "react-native-tab-view";

type State = NavigationState<{
  key: string,
  title: string,
}>;

const FirstRoute = () => (
  <View
    style={{
      alignItems: "center",
      padding: 10,
      margin: 10,
      width: "80%",
      height: "80%",
      flex: 1,
      backgroundColor: "#62BBD4",
    }}
  >
    <Text
      style={{
        width: "100%",
        height: "100%",
        fontWeight: "bold",
      }}
    >
      First tab
    </Text>
  </View>
);

const SecondRoute = () => (
  <View
    style={{
      alignItems: "center",
      padding: 10,
      margin: 10,
      width: "80%",
      height: "80%",
      flex: 1,
      backgroundColor: "#A0D44E",
    }}
  >
    <Text
      style={{
        width: "100%",
        height: "100%",
        fontWeight: "bold",
      }}
    >
      Second tab
    </Text>
  </View>
);

const renderScene = SceneMap({
  first: FirstRoute,
  second: SecondRoute,
});
const TabViewTest = () => {
  const initialLayout = { width: Dimensions.get("window").width };
  const [index, setIndex] = React.useState(0);
  const renderTabBar = (
    props: SceneRendererProps & { navigationState: State }
  ) => (
    <TabBar
      {...props}
      scrollEnabled={true}
      indicatorStyle={styles.indicator}
      style={styles.tabbar}
      labelStyle={styles.label}
      tabStyle={styles.tabStyle}
    />
  );

  const [routes] = React.useState([
    { key: "first", title: "First" },
    { key: "second", title: "Second" },
  ]);

  return (
    <TabView
      style={{
        flex: 1,
        width: 350,
        height: 200,
        margin: 10,
        backgroundColor: "#6D8585",
      }}
      navigationState={{ index, routes }}
      renderScene={renderScene}
      renderTabBar={renderTabBar}
      onIndexChange={setIndex}
      initialLayout={initialLayout}
    />
  );
};

export default TabViewTest;

const styles = StyleSheet.create({
  tabbar: {
    backgroundColor: "#3f51b5",
    height: 70,
    width: 350,
  },
  indicator: {
    backgroundColor: "#ffeb3b",
    width: 175,
    height: 5,
  },
  label: {
    fontWeight: "400",
    fontSize: 20,
    width: 100,
    height: 50,
    color: "black",
  },
  tabStyle: {
    height: 65,
    width: 175,
    backgroundColor: "#BAFDAD",
  },
});
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-pager-view 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-pager-view 文档的 Link 章节](/zh-cn/react-native-pager-view.md#link)进行引入

## Tip
本库依赖react-native-pager-view的能力，react-native-pager-view的能力已从ArkTS切换至CAPI。开启CAPI配置后过渡动画功能才能正常生效。

请在entry目录下的src/main/ets/pages/index.ets中的build函数中修改配置 
```js
   RNApp({   
      rnInstanceConfig: {
       ...,
       //enableCAPIArchitecture 默认为false 需改成true 
       enableCAPIArchitecture: true
      },
    ...
    })
```
<!-- {% endraw %} -->

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases/)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[tabview 官方文档](https://github.com/react-navigation/react-navigation/blob/main/packages/react-native-tab-view/README.md)

如下是 tabview 已经 HarmonyOS 化的属性：

> [!tip] " HarmonyOS 支持"列为 yes 的属性表示支持 HarmonyOS 平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

| Name                  | Description                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `onIndexChange`       | Callback which is called on tab change, receives the index of the new tab as argument                  | function | No       | All      | yes               |
| `renderScene`         | Callback which returns a react element to render as the page for the tab.                              | function | No       | All      | yes               |
| `renderTabBar`        | Callback which returns a custom React Element to use as the tab bar.                                   | function | No       | All      | yes               |
| `tabBarPosition`      | Position of the tab bar in the tab view.                                                               | string   | No       | All      | yes               |
| `keyboardDismissMode` | String indicating whether the keyboard gets dismissed in response to a drag gesture.                   | string   | No       | All      | yes               |
| `swipeEnabled`        | Passing false will disable swipe gestures, but the user can still switch tabs by pressing the tab bar. | boolean  | No       | All      | yes               |
| `style`               | Style to apply to the pager view wrapping all the scenes.                                              | boolean  | No       | All      | yes               |
| `tabStyle`            | Style to apply to the individual tab items in the tab bar.                                             | boolean  | No       | All      | yes               |
| `indicatorStyle`      | Style to apply to the active indicator.                                                                | boolean  | No       | All      | yes               |
| `labelStyle`          | Style to apply to the tab item label.                                                                  | boolean  | No       | All      | yes               |
| `style`               | Style to apply to the tab bar container.                                                               | boolean  | No       | All      | yes               |
| `activeColor`         | Custom color for icon and label in the active tab.                                                     | string   | No       | All      | yes               |
| `inactiveColor`       | Custom color for icon and label in the inactive tab.                                                   | string   | No       | All      | yes               |
| `scrollEnabled`       | Boolean indicating whether to make the tab bar scrollable.                                             | boolean  | No       | All      | yes               |
| `bounces`             | Boolean indicating whether the tab bar bounces when scrolling.                                         | boolean  | No       | All      | yes               |
| `gap`                 | Define a spacing between tabs.                                                                         | number   | No       | All      | yes               |

## 遗留问题

- [x] 已解决： 页面滑动时，有概率卡在中间，无法自动回正[issue#5](https://github.com/react-native-oh-library/react-navigation/issues/5)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/satya164/react-native-tab-view/blob/main/LICENSE.md) ，请自由地享受和参与开源。
