> Template version: v0.2.2

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

> [!Tip] [Github address](https://github.com/react-native-oh-library/react-native-smartrefreshlayout)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-smartrefreshlayout Releases](https://github.com/react-native-oh-library/react-native-smartrefreshlayout/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-smartrefreshlayout@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-smartrefreshlayout@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
  const [text, setText] = useState("Status");
  const [text1, setText1] = useState("Refresh time");

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
          Switch Color (Background color switching is not supported while refreshing)
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
          setText1("Time：" + new Date().getTime() + "onRefresh");
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

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```
### 2. Introducing Native Code

Currently, two methods are available:


Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-smartrefreshlayout": "file:../../node_modules/@react-native-oh-tpl/react-native-smartrefreshlayout/harmony/smart_refresh_layout.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing SmartRefreshLayoutPackage

Open  `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp`  and add the following code:

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

### 4. Introducing SmartRefreshPackage to ArkTS（Version>=0.6.7-0.2.9）

Open the  `entry/src/main/ets/RNPackagesFactory.ts`  file and add the following code:

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

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-smartrefreshlayout Releases](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/releases)

## Properties

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

**SmartRefreshControl**

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

**AnyHeader**

当前组件支持

| Name           | Description                      | Type   | Required | Platform |  HarmonyOS Support |
| -------------- | ------------------------ | ------ | -------- | -------- | -------- |
| `primaryColor` | 刷新组件 Header 的主调色 | string | No       | Android  | Yes   |

**DefaultHeader/ClassicsHeader**

当前组件支持

| Name          | Description                      | Type   | Required  | Platform |  HarmonyOS Support |
| -------------- | ------------------------ | ------ | -------- | -------- | -------- |
| `primaryColor` | 刷新组件 Header 的主调色 | string | No       | Android  | Yes   |
| `accentColor`  | 刷新组件 Header 的强调色 | string | No       | Android  | Yes   |

**StoreHouseHeader**

当前组件支持

| Name       | Description                         | Type    | Required  | Platform |  HarmonyOS Support |
| ----------- | --------------------------- | ------ | -------- | -------- | -------- |
| `text`      | StoreHouseHeader 的文字     | string | No       | Android  | Yes   |
| `textColor` | StoreHouseHeader 的文字颜色 | string | No       | Android  | Yes   |
| `lineWidth` | StoreHouseHeader 的文字线宽 | number | No       | Android  | Yes   |

---

## Static Methods

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| finishRefresh  | complete refresh         | function  | No | Android      | Yes |

## Known Issues

- [X] SmartRefreshLayout 包裹 FlatList 组件，多次下拉刷新，item 会回弹：[Issue #11 ](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/issues/11)
- [ ] SmartRefreshLayout 的StoreHouseHeader刷新头，暂不支持透明度的变化：[Issue #45 ](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/issues/45)

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/react-native-studio/react-native-SmartRefreshLayout/blob/0.6.7/LICENSE).
