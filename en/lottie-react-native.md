> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/lottie-react-native)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/lottie-react-native Releases](https://github.com/react-native-oh-library/lottie-react-native/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/lottie-react-native
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/lottie-react-native
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] 以下 demo 中使用的是本地文件。

```js
import React from "react";
import { View } from "react-native";
import LottieView from "lottie-react-native";

const App = () => {
  return (
    <View style={{ flex: 1 }}>
      <LottieView 
        style={{ width: 300, height: 300 }} 
        source={require("./assets/xxx.json")} 
        autoPlay 
        loop />
    </View>
  );
};

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
    "@react-native-oh-tpl/lottie-react-native": "file:../../node_modules/@react-native-oh-tpl/lottie-react-native/harmony/lottie.har"
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

### 3. Configuring CMakeLists and Introducing LottieAnimationViewPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/lottie-react-native/src/main/cpp" ./lottie)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_lottie)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

Open `entry/src/main/ets/RNPackagesFactory.ts` and add:
> [!TIP] Required for version `6.4.1-0.1.13` and above

```diff
  ...
+ import {LottieAnimationViewPackage} from '@react-native-oh-tpl/lottie-react-native/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new LottieAnimationViewPackage(ctx)
  ];
}
```

### 4.Introducing Lottie Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { LottieAnimationView, LOTTIE_TYPE } from "@react-native-oh-tpl/lottie-react-native"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === LOTTIE_TYPE) {
+   LottieAnimationView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
 ...
}

```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ LOTTIE_TYPE
  ];
```

### 5.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/lottie-react-native Releases](https://github.com/react-native-oh-library/lottie-react-native/releases)

### Permission Requirements

- 如果 source 使用网络 url 应用需要申请网络权限

Include applicable permissions in the module.json5 file within the entry directory.

```json
requestPermissions: [
  {
    name: "ohos.permission.INTERNET",
  },
],
```

- 如果使用的 json 文件里有依赖图片资源或使用 imageAssetsFolder 属性，需要将资源文件放置到 HarmonyOS 工程 rawfile 下对应的路径中

rawfile 路径：`entry/src/main/resources/rawfile`

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description                                                                                                                                                                                                                                                                                                                                                    | Type                                        | Default   | Required | Platform              | HarmonyOS Support |
| ------------------ | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------- | --------- | -------- | --------------------- |-------------------|
| source             | Mandatory - The source of animation. Can be referenced as a local asset by a string, or remotely with an object with a uri property, or it can be an actual JS object of an animation, obtained (for example) with something like require('../path/to/animation.json')                                                                                         | string\| AnimationObject \| { uri: string } | None      | Yes      | All                   | Yes               |
| progress           | A number between 0 and 1. This number represents the normalized progress of the animation. If you update this prop, the animation will correspondingly update to the frame at that progress value. This prop is not required if you are using the imperative API.                                                                                              | number                                      | 0         | No       | iOS, Android, Windows | Yes               |
| speed              | The speed the animation will progress. Sending a negative value will reverse the animation                                                                                                                                                                                                                                                                     | number                                      | 1         | No       | All                   | Yes               |
| duration           | The duration of the animation in ms. Takes precedence over speed when set. This only works when source is an actual JS object of an animation.                                                                                                                                                                                                                 | number                                      | undefined | No       | iOS, Android, Windows | Yes               |
| loop               | A boolean flag indicating whether or not the animation should loop.                                                                                                                                                                                                                                                                                            | boolean                                     | true      | No       | All                   | Yes               |
| autoPlay           | A boolean flag indicating whether or not the animation should start automatically when mounted. This only affects the imperative API.                                                                                                                                                                                                                          | boolean                                     | false     | No       | All                   | Yes               |
| resizeMode         | Determines how to resize the animated view when the frame doesn't match the raw image dimensions. Supports cover, contain and center.                                                                                                                                                                                                                          | 'cover'\| 'contain' \| 'center'             | contain   | No       | iOS, Android, Windows | Yes               |
| style              | Style attributes for the view, as expected in a standard View, aside from border styling                                                                                                                                                                                                                                                                       | StyleProp<ViewStyle>                        | None      | No       | iOS, Android, Windows | Yes               |
| webStyle           | Style attributes for the view, it uses CSSProperties.                                                                                                                                                                                                                                                                                                          | CSSProperties                               | None      | No       | Web                   | No                |
| imageAssetsFolder  | Needed for Android and HarmonyOS to work properly with assets, iOS will ignore it.                                                                                                                                                                                                                                                                             | string                                      | None      | No       | Android               | Yes               |
| useNativeLooping   | Only Windows. When enabled, uses platform-level looping to improve smoothness, but onAnimationLoop will not fire and changing the loop prop will reset playback rather than finishing gracefully.                                                                                                                                                              | boolean                                     | false     | No       | Windows               | No                |
| onAnimationLoop    | Only Windows and Web. A callback function invoked when the animation loops.                                                                                                                                                                                                                                                                                    | callback                                    | None      | No       | Windows, Web          | No                |
| onAnimationFinish  | A callback function which will be called when animation is finished. This callback is called with a boolean isCancelled argument, indicating if the animation actually completed playing, or if it was cancelled, for instance by calling play() or reset() while is was still playing. Note that this callback will be called only when loop is set to false. | callback                                    | None      | No       | All                   | Yes               |
| onAnimationFailure | A callback function which will be called if an error occurs while working with the animation (loading, running, etc). This callback is called with a string error argument, which contains the error message that occured.                                                                                                                                     | callback                                    | None      | No       | All                   | Yes               |
| onAnimationLoaded  | A callback function which will be called when animation is done loading. This callback is called with no parameters.                                                                                                                                                                                                                                           | callback                                    | None      | No       | All                   | Yes               |
| renderMode         | a String flag to set whether or not to render with HARDWARE or SOFTWARE acceleration                                                                                                                                                                                                                                                                           | 'AUTOMATIC'\| 'HARDWARE' \| 'SOFTWARE'      | AUTOMATIC | No       | iOS, Android          | No                |
| cacheComposition   | Only Android and HarmonyOS, a boolean flag indicating whether or not the animation should do caching.                                                                                                                                                                                                                                                          | boolean                                     | true      | No       | Android               | Yes               |
| colorFilters       | An array of objects denoting layers by KeyPath and a new color filter value (as hex string).                                                                                                                                                                                                                                                                   | Array<ColorFilter>                          | []        | No       | iOS, Android, Windows | Yes               |
| textFiltersAndroid | Only Android, an array of objects denoting text values to find and replace.                                                                                                                                                                                                                                                                                    | Array<TextFilterAndroid>                    | []        | No       | Android               | No                |
| textFiltersIOS     | Only iOS, an array of objects denoting text layers by KeyPath and a new string value.                                                                                                                                                                                                                                                                          | Array<TextFilterIOS>                        | []        | No       | iOS                   | No                |
| hover              | Only Web, a boolean denoting whether to play on mouse hover.                                                                                                                                                                                                                                                                                                   | boolean                                     | false     | No       | Web                   | No                |
| direction          | Only Web a number from 1 or -1 denoting playing direction.                                                                                                                                                                                                                                                                                                     | 1\| -1                                      | 1         | No       | Web                   | No                |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                                                                                                                                                                             | Type     | Required | Platform | HarmonyOS Support |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| play   | Play the animation all the way through, at the speed specified as a prop. It can also play a section of the animation (not available on web) when called as play(startFrame, endFrame). | function | No       | All      | Yes               |
| reset  | Reset the animation back to 0 progress.                                                                                                                                                 | function | No       | All      | Yes               |
| pause  | Pauses the animation.                                                                                                                                                                   | function | No       | All      | Yes               |
| resume | Resumes the paused animation.                                                                                                                                                           | function | No       | All      | Yes               |

## Known Issues

- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑，问题: [issue#18](https://github.com/react-native-oh-library/lottie-react-native/issues/18)

## Others

## License

This project is licensed under [Apache License 2.0](https://github.com/lottie-react-native/lottie-react-native/blob/master/LICENSE).
