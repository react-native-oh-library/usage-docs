> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-audio</code> </h1>
</p>

This project is based on [react-native-audio@4.2.2](https://github.com/jsierles/react-native-audio).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-audio`, The version correspondence details are as follows:

| Version                        | Package Name                             | Repository                                                   | Release                                                      |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 4.2.2@deprecated | @react-native-oh-library/react-native-audio  | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-audio) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-audio/releases) |
| > 4.2.2                        | @react-native-ohos/react-native-audio | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-audio) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-audio/releases) |

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState, useEffect } from 'react';
import { SafeAreaView, StatusBar, Text, Button, TextInput, View, Switch, StyleSheet, TouchableOpacity } from 'react-native';
import { AudioRecorder, AudioUtils } from 'react-native-audio';

type FileType = {
    base64: string;
    duration: number;
    status: string;
    audioFileSize: number;
    audioFileURL: string;
}

export default () => {
    const [second, setSecond] = useState<number>(0);
    const [file, setFile] = useState<FileType>();

    const initAudio = async () => {

        // request microphone premission
        await AudioRecorder.requestAuthorization()

        // you check premission any time
        await AudioRecorder.checkAuthorizationStatus();

        // Initialize recording parameters
        await AudioRecorder.prepareRecordingAtPath(
            `${AudioUtils.FilesDirectoryPath}/audio_demo.m4a`,
            {
                SampleRate: 48000,
                Channels: 2,
                AudioQuality: 'High',//only ios
                AudioEncoding: 'aac',
                AudioEncodingBitRate: 100000,
                AudioSource: 1,
                OutputFormat: 'm4a',
                MeteringEnabled: false,//only ios
                MeasurementMode: false,//only ios
                IncludeBase64: true
            })
        AudioRecorder.onProgress = (data) => {
            setSecond(data.currentTime);
        }
        AudioRecorder.onFinished = (data) => {
            const { duration, status, audioFileSize, audioFileURL } = data
            let str = data.base64.slice(0, 20);
            setFile({ base64: str + '...', duration, status, audioFileSize, audioFileURL })
        }
    }
    const resetRecording = () => {
        setFile({
            base64: "",
            duration: 0,
            status: "",
            audioFileSize: 0,
            audioFileURL: ""
        })
        setSecond(0)
        initAudio()
    }
    const renderFileLinesComp = () => {
        if (!file?.base64) return false
        return Object.keys(file).map(name => (
            <View key={name} style={{ display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center', marginTop: 10 }}>
                <Text style={{ fontSize: 12 }}>{name}:</Text>
                <Text >{`${file[name]}`}</Text>
            </View>))
    }

    useEffect(() => {
        initAudio()
        return () => { }
    }, [])

    return (
        <SafeAreaView>
            <View style={{ marginTop: 10, borderColor: '#aaa', borderWidth: 1, padding: 10 }}>
                <View>
                    <Text>{`currentTime: ${parseInt(`${second}`)}`}</Text>
                </View>
            </View>
            <View style={{ marginTop: 10, display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' }}>
                <View style={{ width: 80 }}>
                    <Button
                        title="start"
                        onPress={async () => {
                            await AudioRecorder.startRecording();
                        }}
                    />
                </View>
                <View style={{ width: 80 }}>
                    <Button
                        title="pause"
                        onPress={async () => {
                            await AudioRecorder.pauseRecording();
                        }}
                    />
                </View>
                <View style={{ width: 80 }}>
                    <Button
                        title="resume"
                        onPress={async () => {
                            await AudioRecorder.resumeRecording();
                        }}
                    />
                </View>
                <View style={{ width: 80 }}>
                    <Button
                        title="stop"
                        onPress={async () => {
                            await AudioRecorder.stopRecording();
                            !AudioRecorder.onFinished && resetRecording()
                        }}
                    />
                </View>
            </View>

            {!!file.base64 && <View style={{ marginTop: 10, borderColor: '#aaa', borderWidth: 1, padding: 10 }}>
                <View style={{ marginTop: 10, display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' }}>
                    <Text>录音文件：</Text>
                    <Text style={{ fontSize: 12 }}>{`audio_demo.m4a`}</Text>
                </View>
                {renderFileLinesComp()}
                <View style={{ marginTop: 10, display: 'flex', flexDirection: 'row', justifyContent: 'space-between', alignItems: 'center' }}>
                    <View style={{ width: 160 }}>
                        <Button
                            title="reset"
                            onPress={resetRecording}
                        />
                    </View>
                </View>
            </View>}

        </SafeAreaView >
    )
}
```

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-audio": "file:../../node_modules/@react-native-ohos/react-native-audio/harmony/audio.har"
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


### 2.3 Configuring CMakeLists and Introducing AudioPackage Package

> **[!TIP] Version 4.2.3 and above requires.**

Open entry/src/main/cpp/CMakeLists.txt and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-audio/src/main/cpp" ./audio)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_audio)
# RNOH_END: manual_package_linking_2
```

Open entry/src/main/cpp/PackageProvider.cpp and add the following code:

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

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {AudioPackage} from '@react-native-ohos/react-native-audio/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AudioPackage(ctx)
  ];
}
```

### 2.4 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

Check the release version information in the release address of the third-party library:[@react-native-ohos/react-native-audio Releases](https://gitee.com/openharmony-sig/rntpc_react-native-audio/releases)

## 4. API

> [!TIP]  The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| requestAuthorization  | Request microphone permission  | function  | no | Android/IOS | yes |
| checkAuthorizationStatus  | Check authorization status  | function  | no | Android/IOS | yes |
| prepareRecordingAtPath  | Initialize recording instance parameters  | function  | no | Android/IOS | yes |
| startRecording  | start recording   | function  | no | Android/IOS | yes |
| pauseRecording  | Pause recording  | function  | no | Android/IOS | yes |
| resumeRecording  | Resume recording  | function  | no | Android/IOS | yes |
| stopRecording  | stop recording   | function  | no | Android/IOS | yes |

## 5. Known Issues

## 6. Others
### 6.1 Encoding formats supported by different systems

Encodings supported on iOS: lpcm, ima4, aac, MAC3, MAC6, ulaw, alaw, mp1, mp2, alac, amr.

Encodings supported on Android: aac, aac_eld, amr_nb, amr_wb, he_aac, vorbis.

Encodings supported on Harmony: aac.

AudioQuality、MeteringEnabled、MeasurementMode is only for ios now.

## 7. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-audio/blob/master/LICENSE), Please enjoy and participate freely in open source.