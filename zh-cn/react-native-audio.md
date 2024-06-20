> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-audio</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jsierles/react-native-audio">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jsierles/react-native-audio/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-audio/)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-audio Releases](https://github.com/react-native-oh-library/react-native-audio/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-audio@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-audio@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```js
import { AudioRecorder, AudioUtils } from "@react-native-oh-tpl/react-native-audio";

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
<!-- {% endraw %} -->

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-audio": "file:../../node_modules/@react-native-oh-tpl/react-native-audio/harmony/audio.har"
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


### 在 ArkTs 侧引入 AudioPackage

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

本文档内容基于以下版本验证通过：

react-native-harmony：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[react-native-audio Releases](https://github.com/react-native-oh-library/react-native-audio/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| requestAuthorization  | Request microphone permission  | function  | no | Android/IOS | yes |
| checkAuthorizationStatus  | Check authorization status  | function  | no | Android/IOS | yes |
| prepareRecordingAtPath  | Initialize recording instance parameters  | function  | no | Android/IOS | yes |
| startRecording  | start recording   | function  | no | Android/IOS | yes |
| pauseRecording  | Pause recording  | function  | no | Android/IOS | yes |
| resumeRecording  | Resume recording  | function  | no | Android/IOS | yes |
| stopRecording  | stop recording   | function  | no | Android/IOS | yes |

## 遗留问题

## 其他
### 不同系统支持的编码格式

Encodings supported on iOS: lpcm, ima4, aac, MAC3, MAC6, ulaw, alaw, mp1, mp2, alac, amr.

Encodings supported on Android: aac, aac_eld, amr_nb, amr_wb, he_aac, vorbis.

Encodings supported on Harmony: aac.

AudioQuality、MeteringEnabled、MeasurementMode is only for ios now.

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jsierles/react-native-audio/blob/master/LICENSE) ，请自由地享受和参与开源。