> 模板版本：v0.0.1

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

## 安装与使用

正在 npm 发布中，当前请先从仓库Release中获取库 tgz，通过使用本地依赖来安装本库。

```bash
yarn add xxx
```

或者

```bash
npm install xxx
```

下面的代码展示了这个库的基本使用场景：

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

tabview是js库，依赖pagerview，原生不需要配置，只需配置好pagerview的link相关配置即可

### 引入pagerview代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-pager-view": "file:../../node_modules/react-native-pager-view/harmony/pager_view.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-pager-view": "file:../../node_modules/react-native-pager-view/harmony/pager_view"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 ViewPagerPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-pager-view/src/main/cpp" ./pager_view)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_pager_view)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ViewPagerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ViewPagerPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 RNCViewPager 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
import {
  RNApp,
  ComponentBuilderContext,
  RNAbility,
  AnyJSBundleProvider,
  MetroJSBundleProvider,
  ResourceJSBundleProvider,
} from 'rnoh'
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
import { createRNPackages } from '../RNPackagesFactory'
+ import { RNCViewPager, PAGER_VIEW_TYPE } from 'rnoh-pager-view'

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if(ctx.descriptor.type === PAGER_VIEW_TYPE){
+   RNCViewPager({
+     tag:ctx.descriptor.tag,
+     ctx:ctx.rnohContext,
+     buildCustomComponent:CustomComponentBuilder
+   })
+ }
 ...
}
...
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-tab-view Releases](https://github.com/react-native-oh-library/react-navigation/releases/)

## 属性

详情请查看[tabview 官方文档](https://github.com/react-navigation/react-navigation/blob/main/packages/react-native-tab-view/README.md)

如下是 tabview 已经鸿蒙化的属性：

| 名称                  | 说明                                                                                                   | 类型     | 是否必填 | 原库平台    | 鸿蒙支持 |
| --------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------- | -------- |
| `onIndexChange`       | Callback which is called on tab change, receives the index of the new tab as argument                  | function | No       | All         | yes      |
| `renderScene`         | Callback which returns a react element to render as the page for the tab.                              | function | No       | All         | yes      |
| `renderTabBar`        | Callback which returns a custom React Element to use as the tab bar.                                   | function | No       | All         | yes      |
| `tabBarPosition`      | Position of the tab bar in the tab view.                                                               | string   | No       | All         | yes      |
| `keyboardDismissMode` | String indicating whether the keyboard gets dismissed in response to a drag gesture.                   | string   | No       | All         | yes      |
| `swipeEnabled`        | Passing false will disable swipe gestures, but the user can still switch tabs by pressing the tab bar. | boolean  | No       | All         | yes      |
| `style`               | Style to apply to the pager view wrapping all the scenes.                                              | boolean  | No       | All         | yes      |
| `tabStyle`            | Style to apply to the individual tab items in the tab bar.                                             | boolean  | No       | All         | yes      |
| `indicatorStyle`      | Style to apply to the active indicator.                                                                | boolean  | No       | All         | yes      |
| `labelStyle`          | Style to apply to the tab item label.                                                                  | boolean  | No       | All         | yes      |
| `style`               | Style to apply to the tab bar container.                                                               | boolean  | No       | All         | yes      |
| `activeColor`         | Custom color for icon and label in the active tab.                                                     | string   | No       | All         | yes      |
| `inactiveColor`       | Custom color for icon and label in the inactive tab.                                                   | string   | No       | All         | yes      |
| `scrollEnabled`       | Boolean indicating whether to make the tab bar scrollable.                                             | boolean  | No       | All         | yes      |
| `bounces`             | Function that is invoked when the webview calls window.ReactNativeWebView.postMessage.                 | boolean  | No       | All         | yes      |
| `gap`                 | Define a spacing between tabs.                                                                         | number   | No       | All         | yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/satya164/react-native-tab-view/blob/main/LICENSE.md) ，请自由地享受和参与开源。
