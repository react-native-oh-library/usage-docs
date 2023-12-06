> 模板版本：v0.0.1

<p align="center">
  <h1 align="center"> <code>react-native-video</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-video/react-native-video/tree/support/5.2.X">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20tvos%20|%20windows%20|%20harmony%20|%20react_native_dom%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-video/react-native-video/blob/support/5.2.X/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **yarn**

```bash
yarn add react-native-video@npm:@react-native-oh-tpl/react-native-video
```

#### **npm**

```bash
npm install react-native-video@npm:@react-native-oh-tpl/react-native-video
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```js
import React, {useState, useRef} from 'react';
import {View, ScrollView, StyleSheet, Text,TextInput} from 'react-native';
import RNCVideo from 'react-native-video'

function RNCVideoDemo() {
  const videoRef = React.useRef<typeof RNCVideo>(null);
    
  const [muted, setMuted] = useState(true);
  const [paused, setPaused] = useState(false);
  const [repeat, setRepeat] = useState(true);
  const [disableFocus, setDisableFocus] = useState(false);
  const [uri, setUri] = useState('https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4');
  const [txt, setTxt] = useState('empty');
  const [resizeMode, setResizeMode] = useState('none');
  const [posterResizeMode, setPosterResizeMode] = useState('cover');
  const [seekSec, setSeekSec] = useState(5000);

  const [onVideoLoad, setOnVideoLoad] = useState("onVideoLoad");
  const [onVideoLoadStart, setOnVideoLoadStart] = useState("onVideoLoadStart");
  const [onVideoError, setOnVideoError] = useState("onVideoError");
  const [onVideoProgress, setOnVideoProgress] = useState("onVideoProgress");
  const [onVideoEnd, setOnVideoEnd] = useState("onVideoEnd");
  const [onVideoBuffer, setOnVideoBuffer] = useState("onVideoBuffer");
  const [onPlaybackStalled, setOnPlaybackStalled] = useState("onPlaybackStalled");
  const [onPlaybackResume, setOnPlaybackResume] = useState("onPlaybackResume");
    
  return (

      <View
              style={{
                flexDirection: "row",
                flexWrap:"wrap",
                padding: 0
              }}
            >
       <Text style={styles.button} onPress={() => {  videoRef.current?.seek(5)}} >seek:5s</Text>
	 </View>
	<RNCVideo
        style={styles.video}
        ref={videoRef}
        source={{ uri: uri ,isNetwork:true}}
        paused={paused}
        muted={muted}
        resizeMode={resizeMode}
        repeat={repeat}
        volume={1}
        disableFocus={disableFocus}
		poster={'https://res.vmallres.com/pimages/uomcdn/CN/pms/202304/sbom/4002010007801/group/800_800_9B1356F1330EADDCB20D35D2AE1F46E0.jpg'}
        posterResizeMode={posterResizeMode}
        onLoad={(e) => {
            console.log(`onLoad`)
        }}
        onLoadStart={(e) => {
            console.log(`onLoadStart`)
        }}
        onProgress={(e) => {
            console.log(`onProgress`)
        }}
        onError={(e) => {
            console.log(`onError`)
        }}
        onEnd={() => {
             console.log(`onEnd`)
        }}
        onBuffer={(e) => {
             console.log(`onBuffer`)
        }}
        onPlaybackStalled={() => {
             console.log(`onPlaybackStalled`)
        }}
        onPlaybackResume={() => {
             console.log(`onPlaybackResume`)
        }}
        onReadyForDisplay={() => {
             console.log(`onReadyForDisplay`)
        }}
      ></RNCVideo>
	);
}
const styles = StyleSheet.create({
  video: {
    width: '100%',
    height: 260,
	},
  button: {
    paddingHorizontal: 8,
    paddingVertical: 6,
    borderRadius: 4,
    backgroundColor: "oldlace",
    alignSelf: "flex-start",
    marginHorizontal: "1%",
    marginBottom: 6,
    minWidth: "25%",
    minHeight:20,
    textAlign: "center",
  },
 });

export default RNCVideoDemo;
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
    "rnoh-video": "file:../../node_modules/react-native-video/harmony/rn_video.har"
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
    "rnoh-slider": "file:../../node_modules/react-native-video/harmony/rn_video"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 RNCVideoPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-video/src/main/cpp" ./video)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_video)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNCVideoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNCVideoPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 RNCVideo 组件

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
+ import { RNCVideo, RNC_VIDEO_TYPE } from "rnoh-video"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === RNC_VIDEO_TYPE) {
+   RNCVideo({
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-video Releases](https://github.com/react-native-oh-library/react-native-video/releases)

## 属性

详情请查看[react-native-video 官方文档]([react-native-video/README.md at support/5.2.X · react-native-video/react-native-video (github.com)](https://github.com/react-native-video/react-native-video/blob/support/5.2.X/README.md))

如下是 react-native-video 已经鸿蒙化的属性：

| 名称                    | 说明                                                                                                                                                                                                                                                                                                                                                                                                                                                                               | 类型          | 是否必填 | 原库平台     | 鸿蒙支持 |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | :------------------------------------------- | -------- | ------------ | -------- |
| `source` | Sets the media source. You can pass an asset loaded via require or an object with a uri.                                                                                                                                                                                                                                                                                      | object            | Yes    | All          | yes      |
| `disableFocus`  | Determines whether video audio should override background music/audio in Android devices.<br/>**false (default)**                                                                                                                                                                                                                                                                     | bool                                         | No       | Android Exoplayer | yes      |
| `muted`     | Controls whether the audio is muted.<br/>**false (default)** - Don't mute audio                                                                                                                                                                                                                                                                                                                                     | bool                                   | No       | All          | yes      |
| `paused` | Controls whether the media is paused.<br/>**false (default)** - Don't pause the media                                                                                                                                                                                                                                                                                 | bool | No       | All          | yes      |
| `repeat`    | Determine whether to repeat the video when the end is reached.<br/>**false (default)** - Don't repeat the video                                                                                                                                                                                                                                | bool                                   | No       | All          | yes      |
| `resizeMode`  | Determines how to resize the video when the frame doesn't match the raw video dimensions.<br/>**"none" (default)** - Don't apply resize                                                                                                                                                                                                                                                                        | string                                 | No       | Android ExoPlayer, Android MediaPlayer, iOS, Windows UWP | yes    |
| `volume`      | Adjust the volume.<br/>**1.0 (default)** - Play at full volume                                                                                                                                                                                                                                                                                                                                                 | number                                       | No       | All                                                          | yes    |
| `poster`  | An image to display while the video is loading<br/>Value: string with a URL for the poster, e.g. "<https://baconmockup.com/300/200/>"                                                                                                                                                                                                            | string                               | No       | All          | yes      |
| `posterResizeMode` | Determines how to resize the poster image when the frame doesn't match the raw video dimensions..<br/>**"contain" (default)**- Scale the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or less than the corresponding dimension of the view (minus padding). | string                               | No       | All          | yes      |

## 事件回调

| 名称                | 说明                                                         | 类型     | 是否必填 | 原库平台                                         | 鸿蒙支持 |
| ------------------- | ------------------------------------------------------------ | :------- | -------- | ------------------------------------------------ | -------- |
| `onLoad`            | Callback function that is called when the media is loaded and ready to play. | function | No       | All                                              | yes      |
| `onLoadStart`       | Callback function that is called when the media starts loading. | function | No       | All                                              | yes      |
| `onReadyForDisplay` | Callback function that is called when the first video frame is ready for display. This is when the poster is removed. | function | No       | Android ExoPlayer, Android MediaPlayer, iOS, Web | yes      |
| `onProgress`        | Callback function that is called every progressUpdateInterval seconds with info about which position the media is currently playing. | function | No       | All                                              | yes      |
| `onEnd`             | Callback function that is called when the player reaches the end of the media. | function | No       | All                                              | yes      |
| `onError`           | Callback function that is called when the player experiences a playback error. | function | No       | All                                              | yes      |
| `onBuffer`          | Callback function that is called when the player buffers.    | function | No       | Android, iOS                                     | yes      |
| `onPlaybackStalled` | Callback function that is MediaPlayer MEDIA_INFO_BUFFERING_START | function | No       | Android MediaPlayer                              | yes      |
| `onPlaybackResume`  | Callback function that is MediaPlayer MEDIA_INFO_BUFFERING_END | function | No       | Android MediaPlayer                              | yes      |

## 静态方法

| 名称     | 说明                                                         | 类型     | 是否必填 | 原库平台 | 鸿蒙支持 |
| -------- | ------------------------------------------------------------ | :------- | -------- | -------- | -------- |
| `seek()` | Seek to the specified position represented by seconds. seconds is a float value. | function | No       | All      | yes      |

## 遗留问题

- [ ] source暂时只支持在线URL资源。
- [ ] 未适配无障碍

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/callstack/react-native-slider/blob/main/LICENSE.md) ，请自由地享受和参与开源。
