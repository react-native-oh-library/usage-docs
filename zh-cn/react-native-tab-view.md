<!-- {% raw %} -->
> 模板版本：v0.2.2

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

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases/)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**SceneMap**：用于 renderScene 道具的函数, 接受route.key 映射到 React 组件的对象

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|       scenes        |   创建元素的键值对    |     Object      |    Yes    |   All    |        Yes        |
|       jumpTo        |    导航到其他选项卡   |     Function     |     No    |   All    |        Yes        |

**TabView**：选项卡组件
|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|     renderScene     | Callback which returns a react element to render as the page for the tab      |   Function   |   Yes    |   All    |    Yes       |
|       renderTabBar  | Callback which returns a custom React Element to use as the tab bar     |   Function   |     No   |   All    |        Yes        |
|       lazy          |Function which takes an object with the current route and returns a boolean to indicate whether to lazily render the scenes |    Function |     No    |   All    |        Yes        |
|   lazyPreloadDistance |  When lazy is enabled, you can specify how many adjacent routes should be preloaded with this prop.This value defaults to 0 which means lazy pages are loaded as they come into the viewport               |    Number    |     No    |   All    |        Yes        |
|   renderLazyPlaceholder | Callback which returns a custom React Element to render for routes that haven't been rendered yet. Receives an object containing the route as the argument. The lazy prop also needs to be enabled                   |    Function  |     No    |   All    |        Yes        |
|   keyboardDismissMode | String indicating whether the keyboard gets dismissed in response to a drag gesture. 'auto' (default)       |    String    |     No    |   All    |        Yes        |
|   swipeEnabled | Boolean indicating whether to enable swipe gestures. Swipe gestures are enabled by default        |    Boolean   |     No    |   All    |        Yes        |
|   animationEnabled |Enables animation when changing tab. By default it's true                                    |    Boolean   |     No    |   All    |        Yes        |
|   onSwipeStart |  Callback which is called when the swipe gesture starts, i.e. the user touches the screen and moves it      |    Function  |     No    |   All    |        Yes        |
|   onSwipeEnd |  Callback which is called when the swipe gesture ends, i.e. the user lifts their finger from the screen after the swipe gesture        |    Function  |     No    |   All    |        Yes        |
|   initialLayout |  Object containing the initial height and width of the screens. Passing this will improve the initial rendering performance  |    Object    |     No     |   All    |        Yes        |
|   overScrollMode |  Used to override default value of pager's overScroll mode    |    String    |     No     |   All    |        Yes        |
|   sceneContainerStyle |  Style to apply to the view wrapping each screen. You can pass this to override some default styles such as overflow clipping                                         |    Object    |     No     |   All    |        Yes        |
|   pagerStyle |  Style to apply to the pager view wrapping all the scenes |    Object    |     No     |   All    |        Yes        |

 
**TabBar**：选项卡标签栏

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|       renderIcon    |   Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a icon |   Function |     No    |   All    |        Yes        |
|       renderLabel   |  Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a label  |   Function |    No    |   All    |        Yes        |
|       renderTabBarItem | Function which takes a TabBarItemProps object and returns a custom React Element to be used as a tab button |  Function  |     No    |   All    |  Yes      |
|       renderIndicator|  Function which takes an object with the current route and returns a custom React Element to be used as a tab indicator  | Function  | No  |   All |   Yes  |
|       onTabPress    | Function to execute on tab press. It receives the scene for the pressed tab, useful for things like scroll to top. | Function |  No | All |Yes  |
|       onTabLongPress| Function to execute on tab long press, use for things like showing a menu with more options  |   Function |     No    |   All    |        Yes   |
|       activeColor   |Custom color for icon and label in the active tab        |  String    |     No    |   All    |        Yes         |
|       inactiveColor |Custom color for icon and label in the inactive tab       |    String  |     No    |   All    |        Yes       |
|       pressColor    |    Color for material ripple          |   String   |     No    |   All    |        Yes        |
|       pressOpacity  |Opacity for pressed tab                   |   Number   |     No    |   All    |        Yes        |
|       scrollEnabled |       Boolean indicating whether to make the tab bar scrollable             |   Boolean  |     No    |   All    |        Yes        |
|       bounces       |       Boolean indicating whether the tab bar bounces when scrolling        |   Boolean  |     No    |   All    |        Yes        |
|       tabStyle      |Style to apply to the individual tab items in the tab bar                      |   Object   |     No    |   All    |        Yes        |
|       indicatorStyle|   Style to apply to the active indicator                         |   Object   |     No    |   All    |        Yes        |
|       indicatorContainerStyle  |Style to apply to the container view for the indicator      |  Object    |     No    |   All    |        Yes        |
|       labelStyle    |Style to apply to the tab item label                              |   Object   |     No    |   All    |        Yes        |
|       contentContainerStyle  |Style to apply to the inner container for tabs     |   Object   |     No    |   All    |        Yes        |
|       gap           |      Define a spacing between tabs     |  Number  |     No    |   All    |        Yes        |
|       testID        |         Test id for the tabBar. Can be used for scrolling the tab bar in tests       |   String  |     No    |   All    |        Yes        |

**TabBarIndicator**：选项卡指示器

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|     getTabWidth     |   获取当前元素的宽度   |   Function      |   Yes    |   All    |    Yes            |
|       width         | 元素宽度              |   Number        |    Yes   |   All    |        Yes        |

**TabBarItem**：单个选项卡

|        Name         |     Description      |      Type       | Required | Platform | HarmonyOS Support |
| :-----------------: | :------------------: | :-------------: | :------: | :------: | :---------------: |
|       route         | 路由元素              |   Object        |    Yes   |   All    |        Yes        |

**公共属性**：

Common props 组件属性 HarmonyOS 侧支持情况

|       Name       |                 Description                 |    Type     |  Default  | Required | Platform | HarmonyOS Support |
| :--------------: | :-----------------------------------------: | :---------: | :-------: | :------: | :------: | :---------------: |
|   navigationState|   选项卡视图的状态,对象包含激活路由的索引以及呈现选项卡的路由对象列表的数组 |    Object    |      -     |   Yes    |    All          |    Yes   |
|   onIndexChange  |  在选项卡更改时调用的回调，将接收新选项卡的索引作为参数。调用时需要更新导航状态，否则将删除更改。|   Function    |     -   |    Yes    |   All    | Yes    |
|       style      |              要应用于容器的样式。            |   Object |     -    |   Yes    |        All        |  Yes   |
|       layout     |             覆盖组件样式，宽高               |   Object    |    -      |   No     |   All    |  Yes   |
|   tabBarPosition |            标签栏在标签视图中的位置           |    String    |    "top"   |   No    |        All        | Yes   |
|       position   |   元素动画位置                               |    Animated.AnimatedInterpolation<number> |   -  |   Yes |    All        | Yes   |
|    getLabelText  |  该函数接受具有当前路由的对象并返回选项卡的标签文本,默认情况下使用 route.title  |     Function  |    -    |   No    |        All   |Yes   |
|    getTestID     | 该函数接受具有当前路由的对象，并返回制表符按钮的测试 ID，以便在测试中定位该制表符按钮        |  Function  |     -    |    No     |    All    |Yes   |
|    getAccessible |   该函数接受具有当前路由的对象并返回一个布尔值                                            |   Function |      -    |    No     |    All   |Yes   |
|   getAccessibilityLabel  |    该函数接受具有当前路由的对象并返回制表符按钮的可访问性标签。如果指定，则默认使用 route.accessibilityLabel，否则使用路由标题  |   Function |   -  |  No |All |Yes   |

## 遗留问题

- [x] 已解决： 页面滑动时，有概率卡在中间，无法自动回正[issue#5](https://github.com/react-native-oh-library/react-navigation/issues/5)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/satya164/react-native-tab-view/blob/main/LICENSE.md) ，请自由地享受和参与开源。

<!-- {% endraw %} -->