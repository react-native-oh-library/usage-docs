> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/slider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-slider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20web|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-slider/blob/main/LICENSE.md">
        <img src="https://img.shields.io/npm/l/@react-native-community/slider.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-slider)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/slider Releases](https://github.com/react-native-oh-library/react-native-slider/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/slider
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/slider
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 使用thumbImage属性时请确保引入的图片路径地址正确，可检查harmony/entry/src/main/resources/rawfile/assets目录下是否被打包至静态资源目录，如若不存在则图片放置文件目录不对

```js
import Slider from "@react-native-community/slider"
import { View } from 'react-native'

export default function SliderExample() {
    return (
        <View style={{ backgroundColor: 'red', width: 200, height: 100 }}>
            <Slider
                style={{ width: 200, height: 40 }}
                minimumValue={0}
                maximumValue={1}
                minimumTrackTintColor="#FFFFFF"
                maximumTrackTintColor="#000000"
            />
        </View>
    );
};

```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

## 在工程根目录的 oh-package.json5 添加 overrides 字段

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

    "@react-native-oh-tpl/slider": "file:../../node_modules/@react-native-oh-tpl/slider/harmony/slider.har"
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

### 3.配置 CMakeLists 和引入 SliderPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/slider/src/main/cpp" ./slider)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_slider)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "SliderPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<SliderPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 slider 组件

找到 function buildCustomRNComponent()，一般位于 entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets，添加：

```diff
  ...
+ import { RNCSlider, SLIDER_TYPE } from "@react-native-oh-tpl/slider"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SLIDER_TYPE) {
+   RNCSlider({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
 ...
}
...
```
> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ SLIDER_TYPE
  ];
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/slider Releases](https://github.com/react-native-oh-library/react-native-slider/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description       | Type     | Required | Platform     | HarmonyOS Support |
| ----------------------- | ------------------------ | -------------------------------------------- | ---- | ------------ | ----------------- |
| `style`         | Used to style and layout the `Slider`. See `StyleSheet.js` and `ViewStylePropTypes.js` for more info.    | View.style  | No   | All      | yes       |
| `disabled`      | If true the user won't be able to move the slider.<br/>Default value is false. | bool    | No   | All      | yes       |
| `maximumValue`      | Initial maximum value of the slider.<br/>Default value is 1.                      | number      | No   | All      | yes       |
| `minimumTrackTintColor` | The color used for the track to the left of the button.<br/>Overrides the default blue gradient image on iOS.  | [color](https://reactnative.dev/docs/colors) | No   | All      | yes       |
| `minimumValue`      | Initial minimum value of the slider.<br/>Default value is 0.       | number      | No   | All      | yes       |
| `lowerLimit`        | Slide lower limit. The user won't be able to slide below this limit.              | number      | No   | Android, iOS | yes      |
| `upperLimit`        | Slide upper limit. The user won't be able to slide above this limit.              | number      | No   | Android, iOS | yes        |
| `onSlidingStart`    | Callback that is called when the user picks up the slider.<br/>The initial value is passed as an argument to the callback handler.       | function    | No   | All      | yes       |
| `onSlidingComplete`     | Callback that is called when the user releases the slider, regardless if the value has changed.<br/>The current value is passed as an argument to the callback handler.    | function    | No   | All      | yes       |
| `onValueChange`     | Callback continuously called while the user is dragging the slider.| function    | No   | All      | yes       |
| `step`          | Step value of the slider. The value should be between 0 and (maximumValue - minimumValue). Default value is 0.<br/>On Windows OS the default value is 1% of slider's range (from `minimumValue` to `maximumValue`).       | number      | No   | All      | yes       |
| `maximumTrackTintColor` | The color used for the track to the right of the button.<br/>Overrides the default gray gradient image on iOS.        | [color](https://reactnative.dev/docs/colors) | No   | All      | yes       |
| `value`         | Write-only property representing the value of the slider. Can be used to programmatically control the position of the thumb. Entered once at the beginning still acts as an initial value. Changing the value programmatically does not trigger any event.<br/>The value should be between minimumValue and maximumValue, which default to 0 and 1 respectively. Default value is 0.<br/>_This is not a controlled component_, you don't need to update the value during dragging. | number      | No   | All      | yes       |
| `tapToSeek`         | Permits tapping on the slider track to set the thumb position.<br/>Defaults to false on iOS. No effect on Android or Windows.       | bool    | No   | iOS      | no        |
| `inverted`      | Reverses the direction of the slider.<br/>Default value is false.  | bool    | No   | All      | yes       |
| `vertical`      | Changes the orientation of the slider to vertical, if set to `true`.<br/>Default value is false.   | bool    | No   | Windows      | yes       |
| `thumbTintColor`    | Color of the foreground switch grip.<br/>**NOTE:** This prop will override the `thumbImage` prop set, meaning that if both `thumbImage` and `thumbTintColor` will be set, image used for the thumb may not be displayed correctly!| [color](https://reactnative.dev/docs/colors) | No   | Android      | yes       |
| `maximumTrackImage`     | Assigns a maximum track image. Only static images are supported. The leftmost pixel of the image will be stretched to fill the track.              | Image<br/>.propTypes<br/>.source         | No   | iOS      | no        |
| `minimumTrackImage`     | Assigns a minimum track image. Only static images are supported. The rightmost pixel of the image will be stretched to fill the track.             | Image<br/>.propTypes<br/>.source         | No   | iOS      | no        |
| `thumbImage`        | Sets an image for the thumb. Only static images are supported. Needs to be a URI of a local or network image; base64-encoded SVG is not supported.     | Image<br/>.propTypes<br/>.source         | No   | All      | yes       |
| `trackImage`        | Assigns a single image for the track. Only static images are supported. The center pixel of the image will be stretched to fill the track.         | Image<br/>.propTypes<br/>.source         | No   | iOS      | no        |
| `ref`           | Reference object. | MutableRefObject                     | No   | web      | no        |
| `View`          | [Inherited `View` props...](https://github.com/facebook/react-native-website/blob/master/docs/view.md#props)      |         |      |      |  |

## 遗留问题

- [x] upperLimit 和 lowerLimit 只对数值生效，滑动限制不生效: [issue#2](https://github.com/react-native-oh-library/react-native-slider/issues/2)
- [ ] 不支持滑轨设置图片: [issue#3](https://github.com/react-native-oh-library/react-native-slider/issues/3)
- [ ] 未适配无障碍: [issue#9](https://github.com/react-native-oh-library/react-native-slider/issues/9)
- [ ] 不支持点击滑块轨道来设置拇指位置，不支持指定最大轨迹图像，不支持分配最小轨道图像: [issue#10](https://github.com/react-native-oh-library/react-native-slider/issues/10)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。
