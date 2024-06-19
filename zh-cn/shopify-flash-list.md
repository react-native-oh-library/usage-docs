> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@shopify/flash-list</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/Shopify/flash-list">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Shopify/flash-list/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/flash-list)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/flash-list Releases](https://github.com/react-native-oh-library/flash-list/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/flash-list@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/flash-list@file:#
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Text } from "react-native";
import { FlashList } from "@shopify/flash-list";

const DATA = [
  {
    title: "First Item",
  },
  {
    title: "Second Item",
  },
];

const MyList = () => {
  return (
    <FlashList
      data={DATA}
      renderItem={({ item }) => <Text>{item.title}</Text>}
      estimatedItemSize={200}
    />
  );
};
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "rnoh-flash-list": "file:../../node_modules/@react-native-oh-tpl/flash-list/harmony/flash_list.har"
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

### 配置 CMakeLists 和引入 FlashListPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-flash-list/src/main/cpp" ./flash_list)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_flash_list)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "FlashListPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<FlashListPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 flash-list 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { RNAutoLayoutView, FLASH_LIST_TYPE } from "rnoh-flash-list"
+ import { RNCellContainer, CELL_CONTAINER_TYPE } from "rnoh-flash-list"

  @Builder
  function buildCustomComponent(ctx: ComponentBuilderContext) {
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnComponentContext,
        tag: ctx.tag,
        buildCustomComponent: buildCustomComponent
      })
    }
+   else if (ctx.componentName === FLASH_LIST_TYPE) {
+     RNAutoLayoutView({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomComponent
+     })
+   } else if (ctx.componentName === CELL_CONTAINER_TYPE) {
+     RNCellContainer({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomComponent
+     })
+   }

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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/flash-list releases](https://github.com/react-native-oh-library/flash-list/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                   | Description                                                                                                                                                                                                                                                    | Type                | Required | Platform | HarmonyOS Support  |
| -------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------- | -------- | -------- | ------------------ |
| contentContainerStyle                  | You can use contentContainerStyle to apply padding that will be applied to the whole content itself.                                                                                                                                                           | ContentStyle        | No       | All      | Yes                |
| estimatedListSize                      | Estimated visible height and width of the list. It is not the scroll content size. Defining this prop will enable the list to be rendered immediately. Without it, the list first needs to measure its size, leading to a small delay during the first render. | object              | No       | All      | Yes                |
| horizontal                             | If true, renders items next to each other horizontally instead of stacked vertically. Default is false.                                                                                                                                                        | boolean             | No       | All      | partially（false） |
| keyExtractor                           | Used to extract a unique key for a given item at the specified index. Key is used for optimizing performance.                                                                                                                                                  | function            | No       | All      | Yes                |
| numColumns                             | Multiple columns can only be rendered with horizontal={false} and will zig-zag like a flexWrap layout. Items should all be the same height - masonry layouts are not supported.                                                                                | number              | No       | All      | Yes                |
| extraData                              | A marker property for telling the list to re-render (since it implements PureComponent)                                                                                                                                                                        | any                 | No       | All      | Yes                |
| drawDistance                           | Draw distance for advanced rendering (in dp/px).                                                                                                                                                                                                               | number              | No       | All      | Yes                |
| estimatedItemSize                      | estimatedItemSize is a single numeric value that hints FlashList about the approximate size of the items before they're rendered.                                                                                                                              | number              | No       | All      | Yes                |
| viewabilityConfig                      | viewabilityConfig is a default configuration for determining whether items are viewable.                                                                                                                                                                       | object              | No       | All      | Yes                |
| renderItem                             | Takes an item from data and renders it into the list.                                                                                                                                                                                                          | function            | Yes      | All      | Yes                |
| data                                   | For simplicity, data is a plain array of items of a given type.                                                                                                                                                                                                | ItemT[]             | Yes      | All      | Yes                |
| CellRendererComponent                  | Each cell is rendered using this element. Can be a React Component Class, or a render function                                                                                                                                                                 | JXS Element         | No       | All      | Yes                |
| ListFooterComponent                    | Rendered at the bottom of all the items                                                                                                                                                                                                                        | JXS Element         | No       | All      | Yes                |
| ListHeaderComponent                    | Rendered at the top of all the items                                                                                                                                                                                                                           | JXS Element         | No       | All      | Yes                |
| refreshControl                         | A custom refresh control element.                                                                                                                                                                                                                              | JXS Element         | No       | All      | Yes                |
| renderScrollComponent                  | Rendered as the main scrollview.                                                                                                                                                                                                                               | JXS Element         | No       | All      | Yes                |
| onEndReached                           | Called once when the scroll position gets within onEndReachedThreshold of the rendered content.                                                                                                                                                                | callback            | No       | All      | Yes                |
| onEndReachedThreshold                  | How far from the end (in units of visible length of the list) the bottom edge of the list must be from the end of the content to trigger the onEndReached callback                                                                                             | number              | No       | All      | Yes                |
| onViewableItemsChanged                 | Called when the viewability of rows changes, as defined by the viewabilityConfig prop.                                                                                                                                                                         | callback            | No       | All      | Yes                |
| getItemType                            | Allows developers to specify item types.                                                                                                                                                                                                                       | function            | No       | All      | Yes                |
| overrideItemLayout                     | This method can be used to provide explicit size estimates or change column span of an item.                                                                                                                                                                   | function            | No       | All      | Yes                |
| ItemSeparatorComponent                 | Rendered in between each item, but not at the top or bottom.                                                                                                                                                                                                   | JXS Element         | No       | All      | No                 |
| ListEmptyComponent                     | Rendered when the list is empty                                                                                                                                                                                                                                | JXS Element         | No       | All      | No                 |
| ListFooterComponentStyle               | Styling for internal View for ListFooterComponent.                                                                                                                                                                                                             | React.ComponentType | No       | All      | No                 |
| ListHeaderComponentStyle               | Styling for internal View for ListHeaderComponent.                                                                                                                                                                                                             | StyleProp           | No       | All      | No                 |
| disableAutoLayout                      | FlashList applies some fixes to layouts of its children which can conflict with custom CellRendererComponent implementations. You can disable this behavior by setting this to true.                                                                           | boolean             | No       | All      | No                 |
| disableHorizontalListHeightMeasurement | When set to true the list's rendered size needs to be deterministic (i.e., height and width greater than 0) as FlashList will skip rendering the extra item for measurement. Default value is false.                                                           | boolean             | No       | All      | No                 |
| estimatedFirstItemOffset               | estimatedFirstItemOffset specifies how far the first item is drawn from start of the list window or offset of the first item of the list (not the header).                                                                                                     | number              | No       | All      | No                 |
| initialScrollIndex                     | Instead of starting at the top with the first item, start at initialScrollIndex                                                                                                                                                                                | number              | No       | All      | No                 |
| inverted                               | Reverses the direction of scroll. Uses scale transforms of -1.                                                                                                                                                                                                 | boolean             | No       | All      | No                 |
| onBlankArea                            | FlashList computes blank space that is visible to the user during scrolling or the initial loading of the list.                                                                                                                                                | callback            | No       | All      | No                 |
| onLoad                                 | This event is raised once the list has drawn items on the screen.                                                                                                                                                                                              | callback            | No       | All      | No                 |
| onRefresh                              | If provided, a standard RefreshControl will be added for "Pull to Refresh" functionality. Make sure to also set the refreshing prop correctly.                                                                                                                 | callback            | No       | All      | No                 |
| overrideProps                          | We do not recommend using this prop for anything else than debugging. Internal props of the list will be overriden with the provided values.                                                                                                                   | object              | No       | All      | No                 |
| progressViewOffset                     | Set this when offset is needed for the loading indicator to show correctly.                                                                                                                                                                                    | number              | No       | All      | No                 |
| refreshing                             | Set this true while waiting for new data from a refresh.                                                                                                                                                                                                       | boolean             | No       | All      | No                 |
| viewabilityConfigCallbackPairs         | List of ViewabilityConfig/onViewableItemsChanged pairs. A specific onViewableItemsChanged will be called when its corresponding ViewabilityConfig's conditions are met.                                                                                        | object              | No       | All      | No                 |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                            | Description                                                                                                                                                   | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| prepareForLayoutAnimationRender | Run this method before running layout animations, such as when animating an element when deleting it.                                                         | function | No       | All      | No                |
| recordInteraction               | Tells the list an interaction has occurred, which should trigger viewability calculations, e.g. if waitForInteractions is true and the user has not scrolled. | function | No       | All      | No                |
| scrollToEnd                     | Scrolls to the end of the content.                                                                                                                            | function | No       | All      | No                |
| scrollToIndex                   | Scroll to a given index.                                                                                                                                      | function | No       | All      | No                |
| scrollToItem                    | Scroll to a given item.                                                                                                                                       | function | No       | All      | No                |
| scrollToOffset                  | Scroll to a specific content pixel offset in the list.                                                                                                        | function | No       | All      | No                |

## 遗留问题

- [ ] flash-list 部分属性未实现 HarmonyOS 化: [issue#I8QVS0](https://gitee.com/react-native-oh-library/usage-docs/issues/I8QVS0)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Shopify/flash-list/blob/main/LICENSE.md) ，请自由地享受和参与开源。
