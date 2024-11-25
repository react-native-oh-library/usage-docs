> Template version: v0.2.2

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/flash-list)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/flash-list Releases](https://github.com/react-native-oh-library/flash-list/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



#### **npm**

```bash
npm install @react-native-oh-tpl/flash-list
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/flash-list
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
    "@react-native-oh-tpl/flash-list": "file:../../node_modules/@react-native-oh-tpl/flash-list/harmony/flash_list.har"
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

### 3. Configuring CMakeLists and Introducing FlashListPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/flash-list/src/main/cpp" ./flah-list)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_flash_list)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "FlashListPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<FlashListPackage>(ctx)
    };
}
```

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/flash-list Releases](https://github.com/react-native-oh-library/flash-list/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| contentContainerStyle                  | You can use contentContainerStyle to apply padding that will be applied to the whole content itself.                                                                                                                                                           | ContentStyle        | No       | All      | Yes                |
| estimatedListSize                      | Estimated visible height and width of the list. It is not the scroll content size. Defining this prop will enable the list to be rendered immediately. Without it, the list first needs to measure its size, leading to a small delay during the first render. | object              | No       | All      | Yes                |
| horizontal                             | If true, renders items next to each other horizontally instead of stacked vertically. Default is false.                                                                                                                                                        | boolean             | No       | All      | Yes |
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
| ItemSeparatorComponent                 | Rendered in between each item, but not at the top or bottom.                                                                                                                                                                                                   | JXS Element         | No       | All      | Yes                |
| ListEmptyComponent                     | Rendered when the list is empty                                                                                                                                                                                                                                | JXS Element         | No       | All      |Yes               |
| ListFooterComponentStyle               | Styling for internal View for ListFooterComponent.                                                                                                                                                                                                             | React.ComponentType | No       | All      | Yes                |
| ListHeaderComponentStyle               | Styling for internal View for ListHeaderComponent.                                                                                                                                                                                                             | StyleProp           | No       | All      | Yes                |
| disableAutoLayout                      | FlashList applies some fixes to layouts of its children which can conflict with custom CellRendererComponent implementations. You can disable this behavior by setting this to true.                                                                           | boolean             | No       | All      | Yes                |
| disableHorizontalListHeightMeasurement | When set to true the list's rendered size needs to be deterministic (i.e., height and width greater than 0) as FlashList will skip rendering the extra item for measurement. Default value is false.                                                           | boolean             | No       | All      | Yes                |
| estimatedFirstItemOffset               | estimatedFirstItemOffset specifies how far the first item is drawn from start of the list window or offset of the first item of the list (not the header).                                                                                                     | number              | No       | All      | Yes               |
| initialScrollIndex                     | Instead of starting at the top with the first item, start at initialScrollIndex                                                                                                                                                                                | number              | No       | All      | Yes               |
| inverted                               | Reverses the direction of scroll. Uses scale transforms of -1.                                                                                                                                                                                                 | boolean             | No       | All      | Yes                |
| onBlankArea                            | FlashList computes blank space that is visible to the user during scrolling or the initial loading of the list.                                                                                                                                                | callback            | No       | All      | Yes                 |
| onLoad                                 | This event is raised once the list has drawn items on the screen.                                                                                                                                                                                              | callback            | No       | All      | Yes               |
| onRefresh                              | If provided, a standard RefreshControl will be added for "Pull to Refresh" functionality. Make sure to also set the refreshing prop correctly.                                                                                                                 | callback            | No       | All      | Yes                |
| overrideProps                          | We do not recommend using this prop for anything else than debugging. Internal props of the list will be overriden with the provided values.                                                                                                                   | object              | No       | All      | Yes               |
| progressViewOffset                     | Set this when offset is needed for the loading indicator to show correctly.                                                                                                                                                                                    | number              | No       | All      | Yes                |
| refreshing                             | Set this true while waiting for new data from a refresh.                                                                                                                                                                                                       | boolean             | No       | All      | Yes                 |
| viewabilityConfigCallbackPairs         | List of ViewabilityConfig/onViewableItemsChanged pairs. A specific onViewableItemsChanged will be called when its corresponding ViewabilityConfig's conditions are met.                                                                                        | object              | No       | All      | Yes                 |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| prepareForLayoutAnimationRender | Run this method before running layout animations, such as when animating an element when deleting it.                                                         | function | No       | All      | Yes               |
| recordInteraction               | Tells the list an interaction has occurred, which should trigger viewability calculations, e.g. if waitForInteractions is true and the user has not scrolled. | function | No       | All      | Yes              |
| scrollToEnd                     | Scrolls to the end of the content.                                                                                                                            | function | No       | All      | Yes               |
| scrollToIndex                   | Scroll to a given index.                                                                                                                                      | function | No       | All      | Yes               |
| scrollToItem                    | Scroll to a given item.                                                                                                                                       | function | No       | All      | Yes              |
| scrollToOffset                  | Scroll to a specific content pixel offset in the list.                                                                                                        | function | No       | All      | Yes              |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/Shopify/flash-list/blob/main/LICENSE.md).