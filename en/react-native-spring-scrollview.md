> Template version: v0.2.2

<p align="center">
  <h1 align="center">react-native-spring-scrollview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bolan9999/react-native-spring-scrollview">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bolan9999/react-native-spring-scrollview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-spring-scrollview)

## Installation and Usage

Find the matching version information in the release address of a third-party library:[@react-native-oh-tpl/react-native-spring-scrollview Releases](https://github.com/react-native-oh-library/react-native-spring-scrollview/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-spring-scrollview
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-spring-scrollview
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import {
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
  Platform,
  Animated
} from 'react-native';
import {SpringScrollView} from 'react-native-spring-scrollview';
export default class ScrollToAndOnScrollExample extends React.Component {
  _contentCount = 20;
  _scrollView;
  render() {
    const arr = [];
    for (let i = 0; i < this._contentCount; ++i) arr.push(i);
    return (
      <View style={styles.container}>
        <TouchableOpacity style={styles.scrollTo} onPress={this._scrollTo}>
          <Text>Tap to ScrollTo y=200</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.scrollTo} onPress={this._scroll}>
          <Text>scroll</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.scrollTo} onPress={this._scrollToBegin}>
          <Text>scrollToBegin</Text>
        </TouchableOpacity>
        <TouchableOpacity style={styles.scrollTo} onPress={this._scrollToEnd}>
          <Text>scrollToEnd</Text>
        </TouchableOpacity>
        <SpringScrollView
          style={styles.container}
          ref={(ref) => (this._scrollView = ref)}
          onTouchBegin={this._onTouchBegin}
          onTouchEnd={this._onTouchEnd}
          onMomentumScrollBegin={this.onMomentumScrollBegin}
          onMomentumScrollEnd={this._onMomentumScrollEnd}
          onScrollBeginDrag={this._onScrollBeginDrag}
          onSizeChange={this._onSizeChange}
          onContentSizeChange={this._onContentSizeChange}
          onScroll={this._onScroll}
          >
          {arr.map((i, index) => (
            <Text key={index} style={styles.text}>
              Scroll and Look up the console log to check if
              'onScroll','onTouchBegin','onTouchEnd','onMomentumScrollBegin' and
              'onMomentumScrollEnd' work well!
            </Text>
          ))}
        </SpringScrollView>
      </View>
    );
  }
  _onScroll = offset => {
    console.log("onScroll", offset.nativeEvent);
  };
  _onSizeChange= (wh) => {
    console.log('onSizeChange:'+JSON.stringify(wh));
  };
  _onContentSizeChange= (wh) => {
    console.log('onContentSizeChange:'+JSON.stringify(wh));
  };
  _onNativeContentOffsetExtract = () => {
    console.log('onNativeContentOffsetExtract');
  };
  _onScrollBeginDrag = () => {
    console.log('onScrollBeginDrag');
  };
  _scroll = () => {
    console.log('scroll');
    if (this._scrollView) {
      this._scrollView
        .scroll({x: 0, y: 200});
    }
  };
  _scrollTo = () => {
    console.log('scrollTo');
    if (this._scrollView) {
      this._scrollView
        .scrollTo({x: 0, y: 200})
        .then(() => console.log('ScrollTo has finished'));
    }
  };
  _scrollToBegin = () => {
    console.log('scrollToBegin');
    if (this._scrollView) {
      this._scrollView.scrollToBegin(true);
    }
  };
  _scrollToEnd = () => {
    console.log('scrollToEnd');
    if (this._scrollView) {
      this._scrollView.scrollToEnd(true);
    }
  };
  _onTouchBegin = () => {
    console.log('onTouchBegin');
  };
  _onTouchEnd = () => {
    console.log('onTouchEnd');
  };
  onMomentumScrollBegin = () => {
    console.log('onMomentumScrollBegin');
  };
  _onMomentumScrollEnd = () => {
    console.log('onMomentumScrollEnd');
  };
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  scrollTo: {
    marginTop: Platform.OS === 'ios' ? 20 : 0,
    backgroundColor: 'gray',
    zIndex: 100,
    height: 50,
    justifyContent: 'center',
    alignItems: 'center',
  },
  text: {
    fontSize: 16,
    margin: 20,
  },
});
```

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

The implementation of this library depends on the native code of @react-native-oh-tpl/lottie-react-native, @react-native-oh-tpl/async-storage. If you have already included this library in your HarmonyOS project, you do not need to include it again. You can skip this section and  use the library directly.

If you have not included it, please refer to the [Linking section of the @react-native-oh-tpl/lottie-react-native](/zh-cn/lottie-react-native.md#link), [Linking section of the @react-native-oh-tpl/async-storage](/zh-cn/react-native-async-storage-async-storage.md#link)

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
    "@react-native-oh-tpl/react-native-spring-scrollview": "file:../../node_modules/@react-native-oh-tpl/react-native-spring-scrollview/harmony/spring_scrollview.har",
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

### 3. Configuring CMakeLists and Introducing SpringScrollViewPackge

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-spring-scrollview/src/main/cpp" ./spring_scrollview)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_spring_scrollview)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "SpringScrollViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<SpringScrollViewPackage>(ctx),
    };
}
```

### 4. Introducing SpringScrollViewPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {SpringScrollViewPackage} from '@react-native-oh-tpl/react-native-spring-scrollview/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SpringScrollViewPackage(ctx),
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-spring-scrollview Releases](https://github.com/react-native-oh-library/react-native-spring-scrollview/releases)


## Properties 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| contentStyle | set content style	        | ViewStyle  | yes | iOS/Android      | yes |
| bounces  | 	Bounces if the content offset is out of the content view. It won't be bounces on the horizontal direction if the content view is not wider than the wrapper view although bounces is true. But it will on the vertical direction.        | boolean  | yes | iOS/Android      | yes |
| scrollEnabled  | scrollEnabled         | boolean  | yes | iOS/Android      | yes |
| directionalLockEnabled  | When true, the SpringScrollView will try to lock to only vertical or horizontal scrolling while dragging.        | boolean  | yes | iOS/Android      | yes |
| initialContentOffset  | initial content offset. Only works when initiation.         |  Offset  | yes | iOS/Android      | yes |
| showsVerticalScrollIndicator  | showsVerticalScrollIndicator         |  boolean | yes | iOS/Android      | no |
| showsHorizontalScrollIndicator  | showsHorizontalScrollIndicator         |  boolean  | yes | iOS/Android      | no |
| refreshHeader  | refresh header         |  React.ComponentClass<RefreshHeaderPropType,RefreshHeaderStateType>  | yes | iOS/Android      | yes |
| loadingFooter  | loading header         |  React.ComponentClass<LoadingFooterPropType,LoadingFooterStateType>  | yes | iOS/Android      | yes |
| onRefresh | he callback when refreshing. When this props is configured, a refresh header will be add on the top of the SpringScrollView         |  	()=>any  | yes | iOS/Android      | yes |
| onLoading()  | The callback of loading. If set this prop, a loading footer will add to the botom of the SpringScrollView         |  ()=>any  | yes | iOS/Android      | yes |
| allLoaded  | Whether the data is all loaded.         |  boolean  | yes | iOS/Android      | yes |
| textInputRefs  |  text input      |  any[]  | yes | iOS/Android      | yes |
| inverted  | inverted. It is a service for LargeList.         |  boolean  | yes | iOS/Android      | yes |
| inputToolBarHeight  | set height of the input toolbar        |  number  | yes | iOS/Android      | yes |
| dragToHideKeyboard  | hide the currently displayed keyboard        |  boolean  | yes | iOS/Android      | yes |
| onTouchBegin()  | begin touch         | ()=>any  | yes | iOS/Android      | yes|
| onTouchEnd()   | touch finished         | ()=>any | yes | iOS/Android      | yes|
| beginRefresh()  | If you want to begin refreshing programally without finger draging, call this method after initialized.         | Promise<any>  | yes | iOS/Android      | yes|
| endRefresh()  | End the refreshing status.        | void  | yes | iOS/Android      | yes|
| endLoading()  | End the loading status.        | void  | yes | iOS/Android      | yes|
| scrollTo()  | animate scroll to a specific position          | Promise<void>  | yes | iOS/Android      | yes|
| scroll()  | scroll animation to a specific position        | Promise<void>  | yes | iOS/Android      | yes|
| scrollToBegin()  | scroll begin         | Promise<void>  | yes | iOS/Android      | yes|
| scrollToEnd()  | scroll end         | Promise<void>  | yes | iOS/Android      | yes|
| onScroll()  | scroll         | (evt: ScrollEvent) => any  | yes | iOS/Android      | yes|
| onNativeContentOffsetExtract  |  calculate content offset       |  NativeContentOffset | yes | iOS/Android      | yes|
| onScrollBeginDrag()  | an event that is triggered when the user starts dragging (scrolling) content.         | ()=>any  | yes | iOS/Android     | yes|
| onMomentumScrollBegin()  | When the user scrolls content and the momentum scroll animation begins, it triggers an event.         | ()=>any  | yes | iOS/Android      | yes|
| onMomentumScrollEnd()  | When the user scrolls content and the momentum scroll animation ends, it triggers an event.         | ()=>any  | yes | iOS/Android      | yes|
| onSizeChange  | The callback when the wrapper view size changed.         | (size: Size) => any | yes | iOS/Android      | yes |
| onContentSizeChange  | The callback when the content view size changed.         | (size: Size) => any  | yes | iOS/Android      | yes |

## Known Issues

- [ ] showsVerticalScrollIndicator is not surported in harmony [issue#3](https://github.com/react-native-oh-library/react-native-spring-scrollview/issues/3)
- [ ] showsHorizontalScrollIndicator is not surported in harmony [issue#4](https://github.com/react-native-oh-library/react-native-spring-scrollview/issues/4)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bolan9999/react-native-spring-scrollview/blob/master/LICENSE).
