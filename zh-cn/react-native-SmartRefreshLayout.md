> 模板版本：v0.0.1

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

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add xxx
```

#### **npm**

```bash
npm install xxx
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useState} from 'react';
import {View, Text, FlatList, StyleSheet, TouchableOpacity} from 'react-native';
import {SmartRefreshControl, AnyHeader} from 'react-native-smartrefreshlayout';

const App = () => {
  const [text, setText] = useState('状态');
  const [data, setData] = useState([
    {id: 1, text: 'Item 1'},
    {id: 2, text: 'Item 2'},
    {id: 3, text: 'Item 3'},
    {id: 4, text: 'Item 4'},
    {id: 5, text: 'Item 5'},
    {id: 6, text: 'Item 6'},
    {id: 7, text: 'Item 7'},
    {id: 8, text: 'Item 8'},
    // ... more data ...
  ]);

  const renderItem = ({item}) => (
    <View style={styles.item}>
      <Text style={styles.item}>{item.text}</Text>
    </View>
  );
  let smartRefreshControlRef: React.RefObject<SmartRefreshControl>;
  return (
    <View>
      <TouchableOpacity
        onPress={() => {
          smartRefreshControlRef.finishRefresh({delayed: -1, success: true});
        }}>
        <Text style={{height: 40, width: '100%', backgroundColor: 'red'}}>
          点击完成刷新finish
        </Text>
      </TouchableOpacity>

      <Text style={{height: 40, width: '100%', backgroundColor: ''}}>
        {text}
      </Text>
      <SmartRefreshControl
        ref={ref => (smartRefreshControlRef = ref)}
        primaryColor={'#f3f3f3'}
        headerHeight={66}
        style={{height: 500, width: '100%', backgroundColor: '#ffcc00'}}
        enableRefresh
        enableLoadMore
        onHeaderMoving={e => {
          setText('onHeaderMoving' + JSON.stringify(e.nativeEvent));
        }}
        HeaderComponent={
          <AnyHeader>
            <Text style={{height: 66, width: '100%'}}>刷新头</Text>
          </AnyHeader>
        }>
        <FlatList
          style={{flex: 1, height: '100%', width: '100%'}}
          bounces={false}
          data={data}
          renderItem={renderItem}
          keyExtractor={item => item.id.toString()}
        />
      </SmartRefreshControl>
    </View>
  );
};

const styles = StyleSheet.create({
  item: {
    padding: 16,
    width: '100%',
    height: 100,
  },
});
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-smart-refresh-layout": "file:../../node_modules/react-native-smartrefreshlayout/harmony/smart_refresh_layout.har"
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
    "rnoh-smart-refresh-layout": "file:../../node_modules/react-native-smartrefreshlayout/harmony/smart_refresh_layout"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 SmartRefreshLayoutPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-smart-refresh-layout/src/main/cpp" ./smart-refresh-layout)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_smart_refresh_layout)
# RNOH_END: link_packages
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

### 在 ArkTs 侧引入 SmartRefresh 组件

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
+ import { SmartRefreshControl,SMART_REFRESH_CONTROL_TYPE ,ANY_HEADER_TYPE,RNCAnyHeader,DEFAULT_HEADER_TYPE,RNCDefaultHeader} from "rnoh-smart-refresh-layout"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.descriptor.type == SMART_REFRESH_CONTROL_TYPE){
+    SmartRefreshControl({
+      ctx: ctx.rnohContext,
+      tag: ctx.descriptor.tag,
+      buildCustomComponent: CustomComponentBuilder
+    })
+  } else if (ctx.descriptor.type == ANY_HEADER_TYPE){
+    RNCAnyHeader({
+      ctx: ctx.rnohContext,
+      tag: ctx.descriptor.tag,
+      buildCustomComponent: CustomComponentBuilder
+    })
+  } else if (ctx.descriptor.type == DEFAULT_HEADER_TYPE) {
+    RNCDefaultHeader({
+      ctx: ctx.rnohContext,
+      tag: ctx.descriptor.tag,
+      buildCustomComponent: CustomComponentBuilder
+    })
+  }
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-smartrefreshlayout Releases](https://github.com/react-native-oh-library/react-native-SmartRefreshLayout/releases)

## 属性

**组件 SmartRefreshControl**

| 名称                    | 说明                                       | 类型                                       | 是否必填 | 原库平台    | 鸿蒙支持 |
| --------------------- | ---------------------------------------- | ---------------------------------------- | ---- | ------- | ---- |
| `HeaderComponent`     | 用于渲染 SmartRefreshLayout 组件的 header,默认为 DefaultHeader。 | Element                                  | No   | Android | Yes  |
| `renderHeader`        | 用于渲染 SmartRefreshLayout 组件的 header,默认为 DefaultHeader。 | Element/func                             | No   | Android | No   |
| `enableRefresh`       | 是否启用下拉刷新,默认为 true                        | boolean                                  | No   | Android | No   |
| `headerHeight`        | 设定 header 的高度                            | number                                   | No   | Android | Yes  |
| `primaryColor`        | 设置刷新组件的主调色                               | string                                   | No   | Android | Yes  |
| `autoRefresh`         | 是否自动刷新                                   | object:{refresh:boolean, time:number}    | No   | Android | No   |
| `pureScroll`          | 是否启用纯滚动                                  | boolean                                  | No   | Android | No   |
| `overScrollBounce`    | 是否启用越界拖动，类似 IOS 样式。                      | boolean                                  | No   | Android | No   |
| `dragRate`            | 设置组件下拉高度与手指真实下拉高度的比值,默认为 0.5。            | number                                   | No   | Android | No   |
| `maxDragRate`         | 设置最大显示下拉高度与 header 标准高度的比值，默认为 2.0。      | number                                   | No   | Android | No   |
| `onPullDownToRefresh` | 可下拉刷新时触发                                 | function                                 | No   | Android | No   |
| `onReleaseToRefresh`  | 可释放刷新时触发                                 | function                                 | No   | Android | No   |
| `onRefresh`           | 刷新时触发                                    | function                                 | No   | Android | Yes  |
| `onHeaderReleased`    | Header 释放时触发                             | function                                 | No   | Android | No   |
| `onHeaderMoving`      | header 移动过程中触发,包括下拉过程和释放过程。              | ({nativeEvent: {percent:number, offset:number, headerHeight:number}})=>void; | No   | Android | Yes  |
| `finishRefresh`       | 完成刷新                                     | Methods                                  | No   | Android | Yes  |

**组件 AnyHeader**

仅组件支持渲染，在 RNOH0.72.10 版本中需要给 List 类型子组件添加 bounces = {false}属性，否则无法触发本组件的下拉。（0.72.11 版本已解决）

| 名称             | 说明               | 类型     | 是否必填 | 原库平台    | 鸿蒙支持 |
| -------------- | ---------------- | ------ | ---- | ------- | ---- |
| `primaryColor` | 刷新组件 Header 的主调色 | string | No   | Android | 不支持  |

**组件 DefaultHeader/ClassicsHeader**

当前组件不支持

| 名称             | 说明               | 类型     | 是否必填 | 原库平台    | 鸿蒙支持 |
| -------------- | ---------------- | ------ | ---- | ------- | ---- |
| `primaryColor` | 刷新组件 Header 的主调色 | string | No   | Android | 不支持  |
| `accentColor`  | 刷新组件 Header 的强调色 | string | No   | Android | 不支持  |

**组件 StoreHouseHeader**

当前组件不支持

| 名称          | 说明                     | 类型     | 是否必填 | 原库平台    | 鸿蒙支持 |
| ----------- | ---------------------- | ------ | ---- | ------- | ---- |
| `text`      | StoreHouseHeader 的文字   | string | No   | Android | 不支持  |
| `textColor` | StoreHouseHeader 的文字颜色 | string | No   | Android | 不支持  |
| `lineWidth` | StoreHouseHeader 的文字线宽 | number | No   | Android | 不支持  |

---

## 遗留问题

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/react-native-studio/react-native-SmartRefreshLayout/blob/0.6.7/LICENSE) ，请自由地享受和参与开源。
