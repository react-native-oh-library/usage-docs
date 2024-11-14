> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-navigation/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-tab-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-tab-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-webview. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-pager-view](/en/react-native-pager-view.md#link) to add it to your project.

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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [ @react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases/)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**TabView**：选项卡组件

| Name                  | Description                                                                                                                                                                                         | Type                              | Required | Platform | HarmonyOS Support |
|-----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------|----------|----------|-------------------|
| navigationState       | State for the tab view.                                                                                                                                                                             | fucntion                          | yes      | all      | yes               |
| onIndexChange         | Callback which is called on tab change, receives the index of the new tab as argument. The navigation state needs to be updated when it's called, otherwise the change is dropped.                  | function                          | yes      | all      | yes               |
| renderScene           | Callback which returns a react element to render as the page for the tab.                                                                                                                           | function                          | yes      | all      | yes               |
| renderTabBar          | Callback which returns a custom React Element to use as the tab bar                                                                                                                                 | function                          | no       | all      | yes               |
| tabBarPosition        | Position of the tab bar in the tab view.                                                                                                                                                            | 'top'&#124;'bottom'               | no       | all      | yes               |
| lazy                  | Function which takes an object with the current route and returns a boolean to indicate whether to lazily render the scenes.                                                                        | function                          | no       | all      | yes               |
| lazyPreloadDistance   | When lazy is enabled, you can specify how many adjacent routes should be preloaded with this prop. This value defaults to 0 which means lazy pages are loaded as they come into the viewport.       | number                            | no       | all      | yes               |
| renderLazyPlaceholder | Callback which returns a custom React Element to render for routes that haven't been rendered yet. Receives an object containing the route as the argument. The lazy prop also needs to be enabled. | string                            | no       | all      | yes               |
| keyboardDismissMode   | String indicating whether the keyboard gets dismissed in response to a drag gesture.                                                                                                                | 'auto'&#124;'on-drag'&#124;'none' | no       | all      | yes               |
| swipeEnabled          | Boolean indicating whether to enable swipe gestures. Swipe gestures are enabled by default. Passing false will disable swipe gestures, but the user can still switch tabs by pressing the tab bar.  | boolean                           | no       | all      | yes               |
| animationEnabled      | Enables animation when changing tab. By default it's true.                                                                                                                                          | boolean                           | no       | all      | yes               |
| onSwipeStart          | Callback which is called when the swipe gesture starts, i.e. the user touches the screen and moves it.                                                                                              | boolean                           | no       | all      | yes               |
| onSwipeEnd            | Callback which is called when the swipe gesture ends, i.e. the user lifts their finger from the screen after the swipe gesture.                                                                     | boolean                           | no       | all      | yes               |
| initialLayout         | Object containing the initial height and width of the screens. Passing this will improve the initial rendering performance.                                                                         | object                            | no       | all      | yes               |
| overScrollMode        | Used to override default value of pager's overScroll mode. Can be auto, always or never (Android only).                                                                                             | 'auto'&#124;'always'&#124;'never' | no       | Android  | yes               |
| sceneContainerStyle   | Style to apply to the view wrapping each screen. You can pass this to override some default styles such as overflow clipping                                                                        | object                            | no       | all      | yes               |
| pagerStyle            | Style to apply to the pager view wrapping all the scenes.                                                                                                                                           | object                            | no       | all      | yes               |
| style                 | Style to apply to the tab view container.                                                                                                                                                           | object                            | no       | all      | yes               |

**TabBar**：选项卡标签栏

| Name                    | Description                                                                                                                                                                                        | Type     | Required | Platform | HarmonyOS Support |
|-------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|----------|----------|----------|-------------------|
| getLabelText            | Function which takes an object with the current route and returns the label text for the tab. Uses route.title by default.                                                                         | function | no       | all      | yes               |
| getAccessible           | Function which takes an object with the current route and returns a boolean to indicate whether to mark a tab as accessible. Defaults to true.                                                     | function | no       | all      | yes               |
| getAccessibilityLabel   | Function which takes an object with the current route and returns a accessibility label for the tab button. Uses route.accessibilityLabel by default if specified, otherwise uses the route title. | function | no       | all      | yes               |
| renderIcon              | Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a icon.                                                           | function | no       | all      | yes               |
| renderLabel             | Function which takes an object with the current route, focused status and color and returns a custom React Element to be used as a label.                                                          | function | no       | all      | yes               |
| renderTabBarItem        | Function which takes a TabBarItemProps object and returns a custom React Element to be used as a tab button.                                                                                       | function | no       | all      | yes               |
| renderIndicator         | Function which takes an object with the current route and returns a custom React Element to be used as a tab indicator.                                                                            | function | no       | all      | yes               |
| renderBadge             | Function which takes an object with the current route and returns a custom React Element to be used as a badge.                                                                                    | function | no       | all      | yes               |
| onTabPress              | Function to execute on tab press. It receives the scene for the pressed tab, useful for things like scroll to top.                                                                                 | function | no       | all      | yes               |
| onTabLongPress          | Function to execute on tab long press, use for things like showing a menu with more options                                                                                                        | function | no       | all      | yes               |
| activeColor             | Custom color for icon and label in the active tab.                                                                                                                                                 | string   | no       | all      | yes               |
| inactiveColor           | Custom color for icon and label in the inactive tab.                                                                                                                                               | string   | no       | all      | yes               |
| pressColor              | Color for material ripple (Android >= 5.0 only).                                                                                                                                                   | string   | no       | Android  | no                |
| pressOpacity            | Opacity for pressed tab (iOS and Android < 5.0 only).                                                                                                                                              | number   | no       | all      | yes               |
| scrollEnabled           | Boolean indicating whether to make the tab bar scrollable.                                                                                                                                         | boolean  | no       | all      | yes               |
| bounces                 | Boolean indicating whether the tab bar bounces when scrolling.                                                                                                                                     | boolean  | no       | iOS      | no                |
| tabStyle                | Style to apply to the individual tab items in the tab bar.                                                                                                                                         | object   | no       | all      | yes               |
| indicatorStyle          | Style to apply to the active indicator.                                                                                                                                                            | object   | no       | all      | yes               |
| indicatorContainerStyle | Style to apply to the container view for the indicator.                                                                                                                                            | object   | no       | all      | yes               |
| labelStyle              | Style to apply to the tab item label.                                                                                                                                                              | object   | no       | all      | yes               |
| contentContainerStyle   | Style to apply to the inner container for tabs.                                                                                                                                                    | object   | no       | all      | yes               |
| style (TabBar)          | Style to apply to the tab bar container.                                                                                                                                                           | object   | no       | all      | yes               |
| gap                     | Define a spacing between tabs.                                                                                                                                                                     | number   | no       | all      | yes               |

## Known Issues

- [x] 已解决： 页面滑动时，有概率卡在中间，无法自动回正[issue#5](https://github.com/react-native-oh-library/react-navigation/issues/5)
- [ ] TabBar中的bounces属性，不生效，无法实现滚动回弹效果[issue#34](https://github.com/react-native-oh-library/react-navigation/issues/34)

## Others

- TabBar中的pressColor属性，不生效，无法实现按下更改颜色。 pressColor属性，是专门为Android平台设计的，这个属性在PlatformPressable中直接传递，在IOS上，pressColor属性没有直接对应的实现，IOS使用不同的机制来处理触摸反馈。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/satya164/react-native-tab-view/blob/main/LICENSE.md).
