> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>lottie-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lottie-react-native/lottie-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lottie-react-native/lottie-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/npm/l/lottie-react-native.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/lottie-react-native)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/lottie-react-native Releases](https://github.com/react-native-oh-library/lottie-react-native/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/lottie-react-native@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/lottie-react-native@file:#
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

```js
import LottieView from "lottie-react-native";

<LottieView source={require("./assets/animations.json")} autoPlay loop />;
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-lottie": "file:../../node_modules/@react-native-oh-tpl/lottie-react-native/harmony/lottie.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-lottie": "file:../../node_modules/@react-native-oh-tpl/lottie-react-native/harmony/lottie"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 LottieAnimationViewPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-lottie/src/main/cpp" ./lottie)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_lottie)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "LottieAnimationViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<LottieAnimationViewPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 Lottie 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
+ import { LottieAnimationView, LOTTIE_TYPE } from "rnoh-lottie"

@Builder
function buildCustomComponent(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnComponentContext,
      tag: ctx.tag,
      buildCustomComponent: buildCustomComponent
    })
  }
+ else if (ctx.componentName === LOTTIE_TYPE) {
+   LottieAnimationView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
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

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/lottie-react-native Releases](https://github.com/react-native-oh-library/lottie-react-native/releases)

### 权限要求

- 如果 source 使用网络 url 应用需要申请网络权限
- 如果使用的 json 文件里有依赖图片资源或使用 imageAssetsFolder 属性，需要将资源文件放置到鸿蒙工程 rawfile 下对应的路径中

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                                                                                                                                                                                                                                                                                                                                    | Type                                        | Default   | Required | Platform              | HarmonyOS Support |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- | --------- | -------- | --------------------- | ----------------- |
| source             | Mandatory - The source of animation. Can be referenced as a local asset by a string, or remotely with an object with a uri property, or it can be an actual JS object of an animation, obtained (for example) with something like require('../path/to/animation.json')                                                                                         | string\| AnimationObject \| { uri: string } | None      | Yes      | All                   | Yes               |
| progress           | A number between 0 and 1. This number represents the normalized progress of the animation. If you update this prop, the animation will correspondingly update to the frame at that progress value. This prop is not required if you are using the imperative API.                                                                                              | number                                      | 0         | No       | iOS, Android, Windows | Yes               |
| speed              | The speed the animation will progress. Sending a negative value will reverse the animation                                                                                                                                                                                                                                                                     | number                                      | 1         | No       | All                   | Yes               |
| duration           | The duration of the animation in ms. Takes precedence over speed when set. This only works when source is an actual JS object of an animation.                                                                                                                                                                                                                 | number                                      | undefined | No       | iOS, Android, Windows | Yes               |
| loop               | A boolean flag indicating whether or not the animation should loop.                                                                                                                                                                                                                                                                                            | boolean                                     | true      | No       | All                   | Yes               |
| autoPlay           | A boolean flag indicating whether or not the animation should start automatically when mounted. This only affects the imperative API.                                                                                                                                                                                                                          | boolean                                     | false     | No       | All                   | Yes               |
| resizeMode         | Determines how to resize the animated view when the frame doesn't match the raw image dimensions. Supports cover, contain and center.                                                                                                                                                                                                                          | 'cover'\| 'contain' \| 'center'             | contain   | No       | iOS, Android, Windows | No                |
| style              | Style attributes for the view, as expected in a standard View, aside from border styling                                                                                                                                                                                                                                                                       | StyleProp<ViewStyle>                        | None      | No       | iOS, Android, Windows | Yes               |
| webStyle           | Style attributes for the view, it uses CSSProperties.                                                                                                                                                                                                                                                                                                          | CSSProperties                               | None      | No       | Web                   | No                |
| imageAssetsFolder  | Needed for Android and HarmonyOS to work properly with assets, iOS will ignore it.                                                                                                                                                                                                                                                                             | string                                      | None      | No       | Android               | Yes               |
| useNativeLooping   | Only Windows. When enabled, uses platform-level looping to improve smoothness, but onAnimationLoop will not fire and changing the loop prop will reset playback rather than finishing gracefully.                                                                                                                                                              | boolean                                     | false     | No       | Windows               | No                |
| onAnimationLoop    | Only Windows and Web. A callback function invoked when the animation loops.                                                                                                                                                                                                                                                                                    | callback                                    | None      | No       | Windows, Web          | No                |
| onAnimationFinish  | A callback function which will be called when animation is finished. This callback is called with a boolean isCancelled argument, indicating if the animation actually completed playing, or if it was cancelled, for instance by calling play() or reset() while is was still playing. Note that this callback will be called only when loop is set to false. | callback                                    | None      | No       | All                   | Yes               |
| renderMode         | a String flag to set whether or not to render with HARDWARE or SOFTWARE acceleration                                                                                                                                                                                                                                                                           | 'AUTOMATIC'\| 'HARDWARE' \| 'SOFTWARE'      | AUTOMATIC | No       | iOS, Android          | No                |
| cacheComposition   | Only Android and HarmonyOS, a boolean flag indicating whether or not the animation should do caching.                                                                                                                                                                                                                                                          | boolean                                     | true      | No       | Android               | Yes               |
| colorFilters       | An array of objects denoting layers by KeyPath and a new color filter value (as hex string).                                                                                                                                                                                                                                                                   | Array<ColorFilter>                          | []        | No       | iOS, Android, Windows | No                |
| textFiltersAndroid | Only Android, an array of objects denoting text values to find and replace.                                                                                                                                                                                                                                                                                    | Array<TextFilterAndroid>                    | []        | No       | Android               | No                |
| textFiltersIOS     | Only iOS, an array of objects denoting text layers by KeyPath and a new string value.                                                                                                                                                                                                                                                                          | Array<TextFilterIOS>                        | []        | No       | iOS                   | No                |
| hover              | Only Web, a boolean denoting whether to play on mouse hover.                                                                                                                                                                                                                                                                                                   | boolean                                     | false     | No       | Web                   | No                |
| direction          | Only Web a number from 1 or -1 denoting playing direction.                                                                                                                                                                                                                                                                                                     | 1\| -1                                      | 1         | No       | Web                   | No                |

## 方法 (Imperative API)

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                                                                                                                                             | Type     | Required | Platform | HarmonyOS Support |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| play   | Play the animation all the way through, at the speed specified as a prop. It can also play a section of the animation (not available on web) when called as play(startFrame, endFrame). | function | No       | All      | Yes               |
| reset  | Reset the animation back to 0 progress.                                                                                                                                                 | function | No       | All      | Yes               |
| pause  | Pauses the animation.                                                                                                                                                                   | function | No       | All      | Yes               |
| resume | Resumes the paused animation.                                                                                                                                                           | function | No       | All      | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/lottie-react-native/lottie-react-native/blob/master/LICENSE) ，请自由地享受和参与开源。
