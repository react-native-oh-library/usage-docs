> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-audio</code> </h1>
</p>

本项目基于 [react-native-audio@4.2.2](https://github.com/jsierles/react-native-audio) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-audio`，具体版本所属关系如下：

| Version                        | Package Name                             | Repository                                                   | Release                                                      |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 4.2.2@deprecated | @react-native-oh-library/react-native-audio  | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-audio) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-audio/releases) |
| > 4.2.2                        | @react-native-ohos/react-native-audio | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-audio) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-audio/releases) |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-audio
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-audio
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import { AudioRecorder, AudioUtils } from "@react-native-ohos/react-native-audio";

// request microphone premission
AudioRecorder.requestAuthorization().then((isAuthorised)=>{
  console.log(`isAuthorised: ${isAuthorised}`)
})

// you check premission any time
AudioRecorder.checkAuthorizationStatus().then((hasPermission)=>{
   console.log(`hasPermission: ${hasPermission}`)
})

// Initialize recording parameters
const path = `${AudioUtils.FilesDirectoryPath}/demo.m4a`
AudioRecorder.prepareRecordingAtPath(path,{
  SampleRate: 48000,
  Channels: 2,
  AudioQuality:'High',//only ios
  AudioEncoding: 'aac',
  AudioEncodingBitRate: 100000,
  AudioSource: 1,
  OutputFormat: 'm4a',
  MeteringEnabled:false,//only ios
  MeasurementMode:false,//only ios
  IncludeBase64:false
})

// start recording
AudioRecorder.start();

// pause recording
AudioRecorder.pause();

// resume recording
AudioRecorder.resume();

// stop recording
AudioRecorder.stop();

// add function onProgress
AudioRecorder.onProgress = (data) => {
  console.log(data.currentTime)
}

// add function onFinished
AudioRecorder.onFinished = (data) => {
  console.log(data.base64);//base64
  console.log(data.duration);//audio duration
  console.log(data.status);//OK/REEOR
  console.log(data.audioFileSize);//audioFileSize
  console.log(data.audioFileURL);//audio file url
}
```

## 2. Manual Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1 Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `harmony/oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-audio": "file:../../node_modules/@react-native-ohos/react-native-audio/harmony/audio.har"
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


### 2.3 配置 CMakeLists 和引入 AudioPackage

 > **[!TIP] 版本 4.2.3 及以上需要.**

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-audio/src/main/cpp" ./audio)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_audio)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "AudioPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<AudioPackage>(ctx)
    };
}
```

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {AudioPackage} from '@react-native-oh-tpl/react-native-audio/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AudioPackage(ctx)
  ];
}
```

### 2.4 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-audio Releases](https://gitee.com/openharmony-sig/rntpc_react-native-audio/releases)

## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| requestAuthorization  | Request microphone permission  | function  | no | Android/IOS | yes |
| checkAuthorizationStatus  | Check authorization status  | function  | no | Android/IOS | yes |
| prepareRecordingAtPath  | Initialize recording instance parameters  | function  | no | Android/IOS | yes |
| startRecording  | start recording   | function  | no | Android/IOS | yes |
| pauseRecording  | Pause recording  | function  | no | Android/IOS | yes |
| resumeRecording  | Resume recording  | function  | no | Android/IOS | yes |
| stopRecording  | stop recording   | function  | no | Android/IOS | yes |

## 5. 遗留问题

## 6. 其他
### 6.1 不同系统支持的编码格式

Encodings supported on iOS: lpcm, ima4, aac, MAC3, MAC6, ulaw, alaw, mp1, mp2, alac, amr.

Encodings supported on Android: aac, aac_eld, amr_nb, amr_wb, he_aac, vorbis.

Encodings supported on Harmony: aac.

AudioQuality、MeteringEnabled、MeasurementMode is only for ios now.

## 7. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-audio/blob/master/LICENSE) ，请自由地享受和参与开源。