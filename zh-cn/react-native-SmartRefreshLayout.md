> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-SmartRefreshLayout</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-studio/react-native-SmartRefreshLayout">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-studio/react-native-SmartRefreshLayout/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!Tip] [Github 地址](https://github.com/react-native-oh-library/react-native-smartrefreshlayout)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-smartrefreshlayout Releases](https://github.com/react-native-oh-library/react-native-smartrefreshlayout/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-smartrefreshlayout
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-smartrefreshlayout
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import {
  View,
  Text,
  FlatList,
  StyleSheet,
  TouchableOpacity,
} from "react-native";
import {
  SmartRefreshControl,
  AnyHeader,
} from "react-native-smartrefreshlayout";

const App = () => {
  const [text, setText] = useState("状态");
  const [text1, setText1] = useState("刷新时间");

  const [headerHeight, setHeaderHeight] = useState(66);
  const [color, setColor] = useState("#fff000");

  const [data, setData] = useState([
    { id: 1, text: "Item 1" },
    { id: 2, text: "Item 2" },
    { id: 3, text: "Item 3" },
    { id: 4, text: "Item 4" },
    { id: 5, text: "Item 5" },
    { id: 6, text: "Item 6" },
    { id: 7, text: "Item 7" },
    { id: 8, text: "Item 8" },
    { id: 9, text: "Item 9" },
    { id: 10, text: "Item 10" },
    { id: 11, text: "Item 11" },

    // ... more data ...
  ]);

  const onLoadMore = () => {
    // Simulate loading more data
    setTimeout(() => {
      setData([
        ...data,
        { id: data.length + 1, text: `New Item ${data.length + 1}` },
        // ... more loaded data ...
      ]);
    }, 1000);
  };

  const renderItem = ({ item }) => (
    <View style={styles.item}>
      <Text style={styles.item}>{item.text}</Text>
    </View>
  );
  let smartRefreshControlRef: React.RefObject<SmartRefreshControl>;
  return (
    <View>
      <TouchableOpacity
        onPress={() => {
          smartRefreshControlRef.finishRefresh({ delayed: -1, success: true });
        }}
      >
        <Text style={{ height: 40, width: "100%", backgroundColor: "red" }}>
          finish
        </Text>
      </TouchableOpacity>

      <TouchableOpacity
        onPress={() => {
          setHeaderHeight(headerHeight == 66 ? 132 : 66);
        }}
      >
        <Text style={{ height: 40, width: "100%", backgroundColor: "pink" }}>
          切换高度 66/132
        </Text>
      </TouchableOpacity>

      <TouchableOpacity
        onPress={() => {
          setColor(color === "#fff000" ? "red" : "#fff000");
        }}
      >
        <Text style={{ height: 40, width: "100%", backgroundColor: "green" }}>
          切换颜色（正在刷新中不支持切换背景色）
        </Text>
      </TouchableOpacity>

      <Text style={{ height: 40, width: "100%", backgroundColor: "" }}>
        {text}
      </Text>
      <Text style={{ height: 40, width: "100%", backgroundColor: "" }}>
        {text1}
      </Text>
      <SmartRefreshControl
        ref={(ref) => (smartRefreshControlRef = ref)}
        primaryColor={color}
        headerHeight={headerHeight}
        style={{ height: 500, width: "100%", backgroundColor: "#ffcc00" }}
        onHeaderMoving={(e) => {
          setText("onHeaderMoving" + JSON.stringify(e.nativeEvent));
        }}
        onRefresh={() => {
          setText1("时间：" + new Date().getTime() + "onRefresh触发刷新");
        }}
        HeaderComponent={
          <AnyHeader style = {{ height: 0 }}>
            <Text style={{ height: 66, width: "100%" }}>{text}</Text>
          </AnyHeader>
        }
      >
        <FlatList
          style={{ flex: 1, height: "100%", width: "100%" }}
          bounces={false}
          data={data}
          renderItem={renderItem}
          keyExtractor={(item) => item.id.toString()}
        />
      </SmartRefreshControl>
    </View>
  );
};

const styles = StyleSheet.create({
  item: {
    padding: 16,
    borderBottomWidth: 1,
    borderBottomColor: "#ccc",
    width: 100,
    height: 100,
  },
});

export default App;
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```
### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入 （推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-smartrefreshlayout": "file:../../node_modules/@react-native-oh-tpl/react-native-smartrefreshlayout/harmony/smart_refresh_layout.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 SmartRefreshLayoutPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_END: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-smartrefreshlayout/src/main/cpp" ./smart-refresh-layout)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_smart_refresh_layout)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SmartRefreshLayoutPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SmartRefreshLayoutPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 SmartRefreshPackage（版本>=0.6.7-0.2.9）

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { SmartRefreshPackage } from '@react-native-oh-tpl/react-native-smartrefreshlayout/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SmartRefreshPackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-smartrefreshlayout Releases](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/releases)

## 属性

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**组件 SmartRefreshControl**

| Name                  | Description                                                      | Type                                                                         | Required | Platform | HarmonyOS Support |
| --------------------- | ---------------------------------------------------------------- | ---------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `HeaderComponent`     | 用于渲染 SmartRefreshLayout 组件的 header,默认为 DefaultHeader。 | Element                                                                      | No       | Android  | Yes               |
| `renderHeader`        | 用于渲染 SmartRefreshLayout 组件的 header,默认为 DefaultHeader。 | Element/func                                                                 | No       | Android  | Yes                |
| `enableRefresh`       | 是否启用下拉刷新,默认为 true                                     | boolean                                                                      | No       | Android  | Yes                |
| `headerHeight`        | 设定 header 的高度                                               | number                                                                       | No       | Android  | Yes               |
| `primaryColor`        | 设置刷新组件的主调色                                             | string                                                                       | No       | Android  | Yes               |
| `autoRefresh`         | 是否自动刷新                                                     | object:{refresh:boolean, time:number}                                        | No       | Android  | Yes                |
| `pureScroll`          | 是否启用纯滚动                                                   | boolean                                                                      | No       | Android  | No                |
| `overScrollBounce`    | 是否启用越界拖动，类似 IOS 样式。                                | boolean                                                                      | No       | Android  | No                |
| `dragRate`            | 设置组件下拉高度与手指真实下拉高度的比值,默认为 0.5。            | number                                                                       | No       | Android  | Yes                |
| `maxDragRate`         | 设置最大显示下拉高度与 header 标准高度的比值，默认为 2.0。       | number                                                                       | No       | Android  | Yes                |
| `onPullDownToRefresh` | 可下拉刷新时触发                                                 | function                                                                     | No       | Android  | Yes                |
| `onReleaseToRefresh`  | 可释放刷新时触发                                                 | function                                                                     | No       | Android  | Yes                |
| `onRefresh`           | 刷新时触发                                                       | function                                                                     | No       | Android  | Yes               |
| `onHeaderReleased`    | Header 释放时触发                                                | function                                                                     | No       | Android  | Yes                |
| `onHeaderMoving`      | header 移动过程中触发,包括下拉过程和释放过程。                   | ({nativeEvent: {percent:number, offset:number, headerHeight:number}})=>void; | No       | Android  | Yes               |


**组件 AnyHeader**

当前组件支持

| Name           | Description                      | Type   | Required | Platform |  HarmonyOS Support |
| -------------- | ------------------------ | ------ | -------- | -------- | -------- |
| `primaryColor` | 刷新组件 Header 的主调色 | string | No       | Android  | Yes   |

**组件 DefaultHeader/ClassicsHeader**

当前组件支持

| Name          | Description                      | Type   | Required  | Platform |  HarmonyOS Support |
| -------------- | ------------------------ | ------ | -------- | -------- | -------- |
| `primaryColor` | 刷新组件 Header 的主调色 | string | No       | Android  | Yes   |
| `accentColor`  | 刷新组件 Header 的强调色 | string | No       | Android  | Yes   |

**组件 StoreHouseHeader**

当前组件支持

| Name       | Description                         | Type    | Required  | Platform |  HarmonyOS Support |
| ----------- | --------------------------- | ------ | -------- | -------- | -------- |
| `text`      | StoreHouseHeader 的文字     | string | No       | Android  | Yes   |
| `textColor` | StoreHouseHeader 的文字颜色 | string | No       | Android  | Yes   |
| `lineWidth` | StoreHouseHeader 的文字线宽 | number | No       | Android  | Yes   |

---

## 静态方法

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| finishRefresh  | complete refresh         | function  | No | Android      | Yes |

## 遗留问题

- [X] SmartRefreshLayout 包裹 FlatList 组件，多次下拉刷新，item 会回弹：[Issue #11 ](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/issues/11)
- [ ] SmartRefreshLayout 的StoreHouseHeader刷新头，暂不支持透明度的变化：[Issue #45 ](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/issues/45)

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/react-native-studio/react-native-SmartRefreshLayout/blob/0.6.7/LICENSE) ，请自由地享受和参与开源。
