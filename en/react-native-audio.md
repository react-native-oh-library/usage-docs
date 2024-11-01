> Template version: v0.2.2

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

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-audio/)


## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-audio Releases](https://github.com/react-native-oh-library/react-native-audio/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

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

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-audio": "file:../../node_modules/@react-native-oh-tpl/react-native-audio/harmony/audio.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).


### 3. Introducing AudioPackage Component to ArkTS


Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

This document is verified based on the following versions:

react-native-harmony：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

Check the release version information in the release address of the third-party library: [react-native-audio Releases](https://github.com/react-native-oh-library/react-native-audio/releases)

## API

> [!tip]  The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| requestAuthorization  | Request microphone permission  | function  | no | Android/IOS | yes |
| checkAuthorizationStatus  | Check authorization status  | function  | no | Android/IOS | yes |
| prepareRecordingAtPath  | Initialize recording instance parameters  | function  | no | Android/IOS | yes |
| startRecording  | start recording   | function  | no | Android/IOS | yes |
| pauseRecording  | Pause recording  | function  | no | Android/IOS | yes |
| resumeRecording  | Resume recording  | function  | no | Android/IOS | yes |
| stopRecording  | stop recording   | function  | no | Android/IOS | yes |

## Known Issues

## Others
### Encoding formats supported by different systems

Encodings supported on iOS: lpcm, ima4, aac, MAC3, MAC6, ulaw, alaw, mp1, mp2, alac, amr.

Encodings supported on Android: aac, aac_eld, amr_nb, amr_wb, he_aac, vorbis.

Encodings supported on Harmony: aac.

AudioQuality、MeteringEnabled、MeasurementMode is only for ios now.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jsierles/react-native-audio/blob/master/LICENSE), Please enjoy and participate freely in open source.