> 模板版本：v0.0.1

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

## 安装与使用

> [!tip] 目前 React-Native-OpenHarmony(RNOH) 三方库的 npm 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```bash
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add @react-native-community/slider@npm:@react-native-oh-library/slider
```

#### **npm**

```bash
npm install @react-native-community/slider@npm:@react-native-oh-library/slider
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import Slider from "@react-native-community/slider";

<Slider
  style={{ width: 200, height: 40 }}
  minimumValue={0}
  maximumValue={1}
  minimumTrackTintColor="#FFFFFF"
  maximumTrackTintColor="#000000"
/>;
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
    "rnoh-slider": "file:../../node_modules/@react-native-community/slider/harmony/slider.har"
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
    "rnoh-slider": "file:../../node_modules/@react-native-community/slider/harmony/slider"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 SliderPackge

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-slider/src/main/cpp" ./slider)
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

### 在 ArkTs 侧引入 slider 组件

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
+ import { RNCSlider, SLIDER_TYPE } from "rnoh-slider"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.descriptor.type === SLIDER_TYPE) {
+   RNCSlider({
+     ctx: ctx.rnohContext,
+     tag: ctx.descriptor.tag,
+     buildCustomComponent: CustomComponentBuilder
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

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/slider Releases](https://github.com/react-native-oh-library/react-native-slider/releases)

## 属性

| 名称                    | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 类型                                         | 是否必填 | 原库平台     | 鸿蒙支持 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------- | -------- | ------------ | -------- |
| `style`                 | Used to style and layout the `Slider`. See `StyleSheet.js` and `ViewStylePropTypes.js` for more info.                                                                                                                                                                                                                                                                                                                                                                              | View.style                                   | No       | All          | yes      |
| `disabled`              | If true the user won't be able to move the slider.<br/>Default value is false.                                                                                                                                                                                                                                                                                                                                                                                                     | bool                                         | No       | All          | yes      |
| `maximumValue`          | Initial maximum value of the slider.<br/>Default value is 1.                                                                                                                                                                                                                                                                                                                                                                                                                       | number                                       | No       | All          | yes      |
| `minimumTrackTintColor` | The color used for the track to the left of the button.<br/>Overrides the default blue gradient image on iOS.                                                                                                                                                                                                                                                                                                                                                                      | [color](https://reactnative.dev/docs/colors) | No       | All          | yes      |
| `minimumValue`          | Initial minimum value of the slider.<br/>Default value is 0.                                                                                                                                                                                                                                                                                                                                                                                                                       | number                                       | No       | All          | yes      |
| `lowerLimit`            | Slide lower limit. The user won't be able to slide below this limit.                                                                                                                                                                                                                                                                                                                                                                                                               | number                                       | No       | Android, iOS | no       |
| `upperLimit`            | Slide upper limit. The user won't be able to slide above this limit.                                                                                                                                                                                                                                                                                                                                                                                                               | number                                       | No       | Android, iOS | no       |
| `onSlidingStart`        | Callback that is called when the user picks up the slider.<br/>The initial value is passed as an argument to the callback handler.                                                                                                                                                                                                                                                                                                                                                 | function                                     | No       | All          | yes      |
| `onSlidingComplete`     | Callback that is called when the user releases the slider, regardless if the value has changed.<br/>The current value is passed as an argument to the callback handler.                                                                                                                                                                                                                                                                                                            | function                                     | No       | All          | yes      |
| `onValueChange`         | Callback continuously called while the user is dragging the slider.                                                                                                                                                                                                                                                                                                                                                                                                                | function                                     | No       | All          | yes      |
| `step`                  | Step value of the slider. The value should be between 0 and (maximumValue - minimumValue). Default value is 0.<br/>On Windows OS the default value is 1% of slider's range (from `minimumValue` to `maximumValue`).                                                                                                                                                                                                                                                                | number                                       | No       | All          | yes      |
| `maximumTrackTintColor` | The color used for the track to the right of the button.<br/>Overrides the default gray gradient image on iOS.                                                                                                                                                                                                                                                                                                                                                                     | [color](https://reactnative.dev/docs/colors) | No       | All          | yes      |
| `testID`                | Used to locate this view in UI automation tests.                                                                                                                                                                                                                                                                                                                                                                                                                                   | string                                       | No       | All          | yes      |
| `value`                 | Write-only property representing the value of the slider. Can be used to programmatically control the position of the thumb. Entered once at the beginning still acts as an initial value. Changing the value programmatically does not trigger any event.<br/>The value should be between minimumValue and maximumValue, which default to 0 and 1 respectively. Default value is 0.<br/>_This is not a controlled component_, you don't need to update the value during dragging. | number                                       | No       | All          | yes      |
| `tapToSeek`             | Permits tapping on the slider track to set the thumb position.<br/>Defaults to false on iOS. No effect on Android or Windows.                                                                                                                                                                                                                                                                                                                                                      | bool                                         | No       | iOS          | no       |
| `inverted`              | Reverses the direction of the slider.<br/>Default value is false.                                                                                                                                                                                                                                                                                                                                                                                                                  | bool                                         | No       | All          | yes      |
| `vertical`              | Changes the orientation of the slider to vertical, if set to `true`.<br/>Default value is false.                                                                                                                                                                                                                                                                                                                                                                                   | bool                                         | No       | Windows      | yes      |
| `thumbTintColor`        | Color of the foreground switch grip.<br/>**NOTE:** This prop will override the `thumbImage` prop set, meaning that if both `thumbImage` and `thumbTintColor` will be set, image used for the thumb may not be displayed correctly!                                                                                                                                                                                                                                                 | [color](https://reactnative.dev/docs/colors) | No       | Android      | yes      |
| `maximumTrackImage`     | Assigns a maximum track image. Only static images are supported. The leftmost pixel of the image will be stretched to fill the track.                                                                                                                                                                                                                                                                                                                                              | Image<br/>.propTypes<br/>.source             | No       | iOS          | no       |
| `minimumTrackImage`     | Assigns a minimum track image. Only static images are supported. The rightmost pixel of the image will be stretched to fill the track.                                                                                                                                                                                                                                                                                                                                             | Image<br/>.propTypes<br/>.source             | No       | iOS          | no       |
| `thumbImage`            | Sets an image for the thumb. Only static images are supported. Needs to be a URI of a local or network image; base64-encoded SVG is not supported.                                                                                                                                                                                                                                                                                                                                 | Image<br/>.propTypes<br/>.source             | No       | All          | yes      |
| `trackImage`            | Assigns a single image for the track. Only static images are supported. The center pixel of the image will be stretched to fill the track.                                                                                                                                                                                                                                                                                                                                         | Image<br/>.propTypes<br/>.source             | No       | iOS          | no       |
| `ref`                   | Reference object.                                                                                                                                                                                                                                                                                                                                                                                                                                                                  | MutableRefObject                             | No       | web          | no       |
| `View`                  | [Inherited `View` props...](https://github.com/facebook/react-native-website/blob/master/docs/view.md#props)                                                                                                                                                                                                                                                                                                                                                                       |                                              |          |              |

## 遗留问题

- [ ] upperLimit 和 lowerLimit 只对数值生效，滑动限制不生效: [issue#2](https://github.com/react-native-oh-library/react-native-slider/issues/2)
- [ ] 不支持滑轨设置图片: [issue#3](https://github.com/react-native-oh-library/react-native-slider/issues/3)
- [ ] 未适配无障碍

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。
