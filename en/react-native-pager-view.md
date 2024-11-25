> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-pager-view</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-pager-view">
         <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
       <a href="https://github.com/callstack/react-native-pager-view/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-pager-view)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-pager-view Releases](https://github.com/react-native-oh-library/react-native-pager-view/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-pager-view
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-pager-view
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, View, Text } from "react-native";
import PagerView from "react-native-pager-view";

const MyPager = () => {
  return (
    <PagerView style={styles.pagerView} initialPage={0}>
      <View key="1">
        <Text>First page</Text>
      </View>
      <View key="2">
        <Text>Second page</Text>
      </View>
    </PagerView>
  );
};

const styles = StyleSheet.create({
  pagerView: {
    flex: 1,
  },
});
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

    "@react-native-oh-tpl/react-native-pager-view": "file:../../node_modules/@react-native-oh-tpl/react-native-pager-view/harmony/pager_view.har"
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

### 3. Configuring CMakeLists and Introducing ViewPagerPackage

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

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-pager-view/src/main/cpp" ./pager_view)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_pager_view )
# RNOH_END: link_packages
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing ViewPagerPackage to ArkTS 

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { ViewPagerPackage } from '@react-native-oh-tpl/react-native-pager-view/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ViewPagerPackage(ctx)
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

## Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:[@react-native-oh-tpl/react-native-pager-view Releases](https://github.com/react-native-oh-library/react-native-pager-view/releases)

## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                     | Description                                                  | Type                            | Required | Platform     | HarmonyOS Support                                           |
| ---------------------------------------- | ------------------------------------------------------------ | ------------------------------- | -------- | ------------ | ----------------------------------------------------------- |
| initialPage                              | Index of initial page that should be selected                | number                          | yes      | ios，android | yes                                                         |
| scrollEnabled                            | Should pager view scroll, when scroll enabled                | bool                            | yes      | ios，android | yes                                                         |
| onPageScroll                             | Executed when transitioning between pages (ether because the animation for the requested page has changed or when the user is swiping/dragging between pages) | function                        | no       | ios，android | yes                                                         |
| onPageScrollStateChanged                 | Function called when the page scrolling state has changed    | function                        | no       | ios，android | yes                                                         |
| onPageSelected                           | This callback will be called once the ViewPager finishes navigating to the selected page | function                        | no       | ios，android | yes                                                         |
| pageMargin                               | Blank space to be shown between pages                        | number (Range: 0 ~ ScreenWidth) | no       | ios，android | Only values between 0 and 368 (screen width) are supported. |
| keyboardDismissMode                      | Determines whether the keyboard gets dismissed in response to a drag | one of 'none' ,'on-drag'        | no       | ios,android  | yes                                                         |
| orientation                              | Set horizontal or vertical scrolling orientation (it does not work dynamically) | one of horizontal vertical      | no       | ios，android | yes                                                         |
| overScrollMode                           | Used to override default value of overScroll mode. Can be auto, always or never. Defaults to auto | one of auto, always ,never      | no       | android      | yes                                                         |
| offscreenPageLimit                       | Set the number of pages that should be retained to either side of the currently visible page(s). Pages beyond this limit will be recreated from the adapter when needed. Defaults to RecyclerView's caching strategy. The given value must either be larger than 0. | number                          | no       | android      | no                                                          |
| overdrag                                 | Allows for overscrolling after reaching the end or very beginning or pages. Defaults to false | bool                            | no       | ios          | yes                                                         |
| layoutDirection                          | Specifies layout direction. Use ltr or rtl to set explicitly or locale to deduce from the default language script of a locale. Defaults to locale | string                          | no       | android,ios  | yes                                                         |
| setPage(index: number)                   | Function to scroll to a specific page in the PagerView. Invalid index is ignored. | function                        | no       | android,ios  | yes                                                         |
| setPageWithoutAnimation(index: number)   | Function to scroll to a specific page in the PagerView. Invalid index is ignored. | function                        | no       | android,ios  | yes                                                         |
| setScrollEnabled(scrollEnabled: boolean) | FA helper function to enable/disable scroll imperatively. The recommended way is using the scrollEnabled prop, however, there might be a case where a imperative solution is more useful (e.g. for not blocking an animation) | function                        | no       | android,ios  | yes                                                         |

## Known Issues

- [ ] offscreenPageLimit is not adapted to HarmonyOS[issue#7](https://github.com/react-native-oh-library/react-native-pager-view/issues/7)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-pager-view/blob/harmony/LICENSE).
