> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-spring-scrollview)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-spring-scrollview Releases](https://github.com/react-native-oh-library/react-native-spring-scrollview/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-spring-scrollview@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-spring-scrollview@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
  Platform,
  Animated,
  ScrollView,
} from 'react-native';
import {SpringScrollView} from 'react-native-spring-scrollview';

const AnimatedSpringScrollView = Animated.createAnimatedComponent(SpringScrollView);
export default class ScrollToAndOnScrollExample extends React.Component {
  _contentCount = 20;
  _scrollView;
  _nativeOffset = {
    y: new Animated.Value(0),
  };

  render() {
    const arr = [];
    for (let i = 0; i < this._contentCount; ++i) arr.push(i);
    return (
      <View style={styles.container}>
        <TouchableOpacity style={styles.scrollTo} onPress={this._scrollTo}>
          <Text>Tap to ScrollTo y=200</Text>
        </TouchableOpacity>
        <SpringScrollView
          style={styles.container}
          ref={(ref) => (this._scrollView = ref)}
          onTouchBegin={this._onTouchBegin}
          onTouchFinish={this._onTouchEnd}
          onMomentumScrollBegin={this.onMomentumScrollBegin}
          onMomentumScrollEnd={this._onMomentumScrollEnd}
          onNativeContentOffsetExtract={this._nativeOffset}
          >
          {arr.map((i, index) => (
            <Text key={index} style={styles.text}>
              Scroll and Look up the console log to check if
              'onScroll','onTouchBegin','onTouchEnd','onMomentumScrollBegin' and
              'onMomentumScrollEnd' work well!
            </Text>
          ))}
          <Animated.View style={this._stickyHeaderStyle}>
            <Text>Test `onNativeContentOffsetExtract`</Text>
          </Animated.View>
        </SpringScrollView>
      </View>
    );
  }
```

## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

本库HarmonyOS侧实现依赖@react-native-oh-tpl/lottie-react-native的原生端代码，如已在HarmonyOS工程中引入过该库，则无需再次引入，可跳过本章步骤，直接使用。

如未引入请参考[@react-native-oh-tpl/lottie-react-native文档的link章节](/zh-cn/lottie-react-native.md#link)进行引入

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-spring-scrollview": "file:../../node_modules/@react-native-oh-tpl/react-native-spring-scrollview/harmony/spring_scrollview.har",
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

### 3.配置 CMakeLists 和引入 SpringScrollViewPackge

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 4.在 ArkTs 侧引入 SpringScrollViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

打开 `entry/src/main/ets/pages/Index.ets`，添加：
```diff
...
+ const arkTsComponentNames: Array<string> =["SampleView","GeneratedSampleView","PropsDisplayer","LottieAnimationView"];
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-spring-scrollview Releases](https://github.com/react-native-oh-library/react-native-spring-scrollview/releases)


## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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
| tapToHideKeyboard  | hide the currently displayed keyboard        |  boolean  | yes | iOS/Android      | yes |
| onTouchBegin()  | begin touch         | ()=>any  | yes | iOS/Android      | yes|
| onTouchFinish()   | touch finished         | ()=>any | yes | iOS/Android      | yes|
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

## 遗留问题

- [ ] showsVerticalScrollIndicator属性harmony暂不支持[issue#3](https://github.com/react-native-oh-library/react-native-spring-scrollview/issues/3)
- [ ] showsHorizontalScrollIndicator属性harmony暂不支持[issue#4](https://github.com/react-native-oh-library/react-native-spring-scrollview/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bolan9999/react-native-spring-scrollview/blob/master/LICENSE) ，请自由地享受和参与开源。
