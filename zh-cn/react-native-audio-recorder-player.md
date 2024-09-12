> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-audio-recorder-player</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hyochan/react-native-audio-recorder-player">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hyochan/react-native-audio-recorder-player/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-audio-recorder-player)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-audio-recorder-player Releases](https://github.com/react-native-oh-library/react-native-audio-recorder-player/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!tip] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-audio-recorder-player@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-audio-recorder-player@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import AudioRecorderPlayer, {
    AVEncoderAudioQualityIOSType,
    AVEncodingOption,
    AudioEncoderAndroidType,
    AudioSourceAndroidType,
    OutputFormatAndroidType,
} from 'react-native-audio-recorder-player'; import type {
    PlayBackType,
    RecordBackType,
} from 'react-native-audio-recorder-player';
import { AudioMimeHarmonyType, AudioFormatHarmonyType, AudioSourceHarmonyType, AudioSet } from "@react-native-oh-tpl/react-native-audio-recorder-player";

import {
    Dimensions,
    Platform,
    ActivityIndicator,
    Image,
    SafeAreaView,
    StyleSheet,
    Text,
    TouchableOpacity,
    View,
} from 'react-native';
import React, { Component } from 'react';

import type { ReactElement, ReactNode } from 'react';

const stylesButton: any = StyleSheet.create({
    btn: {
        backgroundColor: 'transparent',
        alignSelf: 'center',
        borderRadius: 4,
        borderWidth: 2,
        width: 320,
        height: 52,
        borderColor: 'white',

        alignItems: 'center',
        justifyContent: 'center',
    },
    btnDisabled: {
        backgroundColor: 'rgb(243,243,243)',
        alignSelf: 'center',
        borderRadius: 4,
        borderWidth: 2,
        width: 320,
        height: 52,
        borderColor: '#333',

        alignItems: 'center',
        justifyContent: 'center',
    },
    txt: {
        fontSize: 14,
        color: 'white',
    },
    imgLeft: {
        width: 24,
        height: 24,
        position: 'absolute',
        left: 16,
    },
});

interface ItemProps {
    children?: ReactNode;
    isLoading?: boolean;
    isDisabled?: boolean;
    onPress?: () => void;
    style?: any;
    disabledStyle?: any;
    textStyle?: any;
    imgLeftSrc?: any;
    imgLeftStyle?: any;
    indicatorColor?: string;
    activeOpacity?: number;
}

class Button extends Component<ItemProps, any> {
    private static defaultProps: Partial<ItemProps> = {
        isLoading: false,
        isDisabled: false,
        style: stylesButton.btn,
        textStyle: stylesButton.txt,
        imgLeftStyle: stylesButton.imgLeft,
        indicatorColor: 'white',
        activeOpacity: 0.5,
    };

    constructor(props: ItemProps) {
        super(props);
        this.state = {};
    }

    public render(): ReactElement {
        if (this.props.isDisabled) {
            return (
                <View style={this.props.disabledStyle}>
                    <Text style={this.props.textStyle}>{this.props.children}</Text>
                </View>
            );
        }

        if (this.props.isLoading) {
            return (
                <View style={this.props.style}>
                    <ActivityIndicator size="small" color={this.props.indicatorColor} />
                </View>
            );
        }

        return (
            <TouchableOpacity
                activeOpacity={this.props.activeOpacity}
                onPress={this.props.onPress}>
                <View style={this.props.style}>
                    {this.props.imgLeftSrc ? (
                        <Image
                            style={this.props.imgLeftStyle}
                            source={this.props.imgLeftSrc}
                        />
                    ) : null}
                    <Text style={this.props.textStyle}>{this.props.children}</Text>
                </View>
            </TouchableOpacity>
        );
    }
}

const styles: any = StyleSheet.create({
    container: {
        flex: 1,
        backgroundColor: '#455A64',
        flexDirection: 'column',
        alignItems: 'center',
        height: Dimensions.get('screen').height
    },
    titleTxt: {
        marginTop: 100,
        color: 'white',
        fontSize: 28,
    },
    viewRecorder: {
        marginTop: 40,
        width: '100%',
        alignItems: 'center',
    },
    recordBtnWrapper: {
        flexDirection: 'row',
    },
    viewPlayer: {
        marginTop: 60,
        alignSelf: 'stretch',
        alignItems: 'center',
    },
    viewBarWrapper: {
        marginTop: 28,
        marginHorizontal: 28,
        alignSelf: 'stretch',
    },
    viewBar: {
        backgroundColor: '#ccc',
        height: 4,
        alignSelf: 'stretch',
    },
    viewBarPlay: {
        backgroundColor: 'white',
        height: 4,
        width: 0,
    },
    playStatusTxt: {
        marginTop: 8,
        color: '#ccc',
    },
    playBtnWrapper: {
        flexDirection: 'row',
        marginTop: 40,
    },
    btn: {
        borderColor: 'white',
        borderWidth: 1,
    },
    txt: {
        color: 'white',
        fontSize: 14,
        marginHorizontal: 8,
        marginVertical: 4,
    },
    txtRecordCounter: {
        marginTop: 32,
        color: 'white',
        fontSize: 20,
        textAlignVertical: 'center',
        fontWeight: '200',
        fontFamily: 'Helvetica Neue',
        letterSpacing: 3,
        width: 300
    },
    txtCounter: {
        marginTop: 12,
        color: 'white',
        fontSize: 20,
        textAlignVertical: 'center',
        fontWeight: '200',
        fontFamily: 'Helvetica Neue',
        letterSpacing: 3,
        width: 300
    },
});

interface State {
    isLoggingIn: boolean;
    recordSecs: number;
    recordTime: string;
    currentPositionSec: number;
    currentDurationSec: number;
    playTime: string;
    duration: string;
}

const screenWidth = Dimensions.get('screen').width;

class Page extends Component<any, State> {
    private audioRecorderPlayer

    constructor(props: any) {
        super(props);
        this.state = {
            isLoggingIn: false,
            recordSecs: 0,
            recordTime: '00:00:00',
            currentPositionSec: 0,
            currentDurationSec: 0,
            playTime: '00:00:00',
            duration: '00:00:00',
        };

        this.audioRecorderPlayer = new AudioRecorderPlayer()
        this.audioRecorderPlayer.setSubscriptionDuration(0.5); // optional. Default is 0.5
    }

    public render(): ReactElement {
        let playWidth =
            (this.state.currentPositionSec / this.state.currentDurationSec) *
            (screenWidth - 56);

        if (!playWidth) {
            playWidth = 0;
        }

        return (
            <SafeAreaView style={styles.container}>
                <Text style={styles.titleTxt}>Audio Recorder Player</Text>
                <Text style={styles.txtRecordCounter}>{this.state.recordTime}</Text>
                <View style={styles.viewRecorder}>
                    <View style={styles.recordBtnWrapper}>
                        <Button
                            style={styles.btn}
                            onPress={this.onStartRecord}
                            textStyle={styles.txt}>
                            startRecord
                        </Button>
                        <Button
                            style={[
                                styles.btn,
                                {
                                    marginLeft: 12,
                                },
                            ]}
                            onPress={this.onPauseRecord}
                            textStyle={styles.txt}>
                            Pause
                        </Button>
                        <Button
                            style={[
                                styles.btn,
                                {
                                    marginLeft: 12,
                                },
                            ]}
                            onPress={this.onResumeRecord}
                            textStyle={styles.txt}>
                            Resume
                        </Button>
                        <Button
                            style={[styles.btn, { marginLeft: 12 }]}
                            onPress={this.onStopRecord}
                            textStyle={styles.txt}>
                            Stop
                        </Button>
                    </View>
                </View>
                <View style={styles.viewPlayer}>
                    <TouchableOpacity
                        style={styles.viewBarWrapper}
                        onPress={this.onStatusPress}>
                        <View style={styles.viewBar}>
                            <View style={[styles.viewBarPlay, { width: playWidth }]} />
                        </View>
                    </TouchableOpacity>
                    <Text style={styles.txtCounter}>
                        {this.state.playTime} / {this.state.duration}
                    </Text>
                    <View style={styles.playBtnWrapper}>
                        <Button
                            style={styles.btn}
                            onPress={this.onStartPlay}
                            textStyle={styles.txt}>
                            Play
                        </Button>
                        <Button
                            style={[
                                styles.btn,
                                {
                                    marginLeft: 12,
                                },
                            ]}
                            onPress={this.onPausePlay}
                            textStyle={styles.txt}>
                            Pause
                        </Button>
                        <Button
                            style={[
                                styles.btn,
                                {
                                    marginLeft: 12,
                                },
                            ]}
                            onPress={this.onResumePlay}
                            textStyle={styles.txt}>
                            Resume
                        </Button>
                        <Button
                            style={[
                                styles.btn,
                                {
                                    marginLeft: 12,
                                },
                            ]}
                            onPress={this.onStopPlay}
                            textStyle={styles.txt}>
                            Stop
                        </Button>
                    </View>
                </View>
            </SafeAreaView>
        );
    }

    private onStatusPress = (e: any): void => {
        const touchX = e.nativeEvent.locationX;
        console.log(`touchX: ${touchX}`);

        const playWidth =
            (this.state.currentPositionSec / this.state.currentDurationSec) *
            (screenWidth - 56);
        console.log(`currentPlayWidth: ${playWidth}`);

        const currentPosition = Math.round(this.state.currentPositionSec);

        if (playWidth && playWidth < touchX) {
            const addSecs = Math.round(currentPosition + 1000);
            this.audioRecorderPlayer.seekToPlayer(addSecs);
            console.log(`addSecs: ${addSecs}`);
        } else {
            const subSecs = Math.round(currentPosition - 1000);
            this.audioRecorderPlayer.seekToPlayer(subSecs);
            console.log(`subSecs: ${subSecs}`);
        }
    };

    private onStartRecord = async (): Promise<void> => {

        const audioSet: AudioSet = {
            AudioEncoderAndroid: AudioEncoderAndroidType.AAC,
            AudioSourceAndroid: AudioSourceAndroidType.MIC,
            AVEncoderAudioQualityKeyIOS: AVEncoderAudioQualityIOSType.high,
            AVNumberOfChannelsKeyIOS: 2,
            AVFormatIDKeyIOS: AVEncodingOption.aac,
            OutputFormatAndroid: OutputFormatAndroidType.AAC_ADTS,
            AudioSourceHarmony: AudioSourceHarmonyType.MIC,
            AudioMimeHarmony: AudioMimeHarmonyType.AUDIO_AAC,
            AudioFileFormatHarmony: AudioFormatHarmonyType.MPEG_4A,
            AudioEncodingBitRateHarmony: 3200,
            AudioSamplingRateHarmony: 44100,
            AudioChannelsHarmony: 2,
        };

        console.log('audioSet', audioSet);

        const uri = await this.audioRecorderPlayer.startRecorder(
            'audio.m4a',
            audioSet,
        );

        this.audioRecorderPlayer.addRecordBackListener((e: RecordBackType) => {
            console.log('record-back', e);
            this.setState({
                recordSecs: e.currentPosition,
                recordTime: this.audioRecorderPlayer.mmssss(
                    Math.floor(e.currentPosition),
                ),
            });
        });

        console.log(`uri: ${uri}`);
    };

    private onPauseRecord = async (): Promise<void> => {
        try {
            const r = await this.audioRecorderPlayer.pauseRecorder();
            console.log(r);
        } catch (err) {
            console.log('pauseRecord', err);
        }
    };

    private onResumeRecord = async (): Promise<void> => {
        await this.audioRecorderPlayer.resumeRecorder();
    };

    private onStopRecord = async (): Promise<void> => {
        const result = await this.audioRecorderPlayer.stopRecorder();
        this.audioRecorderPlayer.removeRecordBackListener();
        this.setState({
            recordSecs: 0,
        });
        console.log(result, '>>>>>>>stopRecorder');
    };

    private onStartPlay = async (): Promise<void> => {
        console.log('onStartPlay');

        try {


            const msg = await this.audioRecorderPlayer.startPlayer('https://sis-sample-audio.obs.cn-north-1.myhuaweicloud.com/16k16bit.mp3', { 'User-Agent': 'Mozilla/5.0 (X11; Linux x86_64; rv:12.0) Gecko/20100101 Firefox/21.0' });
            const volume = await this.audioRecorderPlayer.setVolume(1);
            this.audioRecorderPlayer.addPlayBackListener((e: PlayBackType) => {
                console.log('playBackListener', e);
                this.setState({
                    currentPositionSec: e.currentPosition,
                    currentDurationSec: e.duration,
                    playTime: this.audioRecorderPlayer.mmssss(e.currentPosition),
                    duration: this.audioRecorderPlayer.mmssss(Math.floor(e.duration)),
                });
            });

        } catch (err) {
            console.log('startPlayer error', err);
        }
    };

    private onPausePlay = async (): Promise<void> => {
        await this.audioRecorderPlayer.pausePlayer();
    };

    private onResumePlay = async (): Promise<void> => {
        await this.audioRecorderPlayer.resumePlayer();
    };

    private onStopPlay = async (): Promise<void> => {
        console.log('onStopPlay');
        this.audioRecorderPlayer.stopPlayer();
        this.audioRecorderPlayer.removePlayBackListener();
    };
}

export default Page;

```
## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

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

方法一：通过 har 包引入（推荐）

> [!tip] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-audio-recorder-player": "file:../../node_modules/@react-native-oh-tpl/react-native-audio-recorder-player/harmony/audio_recorder_player.har"
  }
```
点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```
方法二：直接链接源码

> [!tip] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 配置 CMakeLists 和引入 RNAudioRecorderPlayerPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-audio-recorder-player/src/main/cpp" ./audio_recorder_player)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_audio_recorder_player)
# RNOH_END: manual_package_linking_2
```
打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNAudioRecorderPlayerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNAudioRecorderPlayerPackage>(ctx)
    };
}
```
### 在 ArkTs 侧引入 react-native-audio-recorder-player Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import {RNAudioRecorderPlayerPackage} from '@react-native-oh-tpl/react-native-audio-recorder-player/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAudioRecorderPlayerPackage(ctx)
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-audio-recorder-player Releases](https://github.com/react-native-oh-library/react-native-audio-recorder-player/releases)

### 权限要求

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {"name": "ohos.permission.INTERNET"},//网络播放音频需添加
+  {
+    "name": "ohos.permission.MICROPHONE",
+    "reason": "$string:Access_Create_Audio",
+     "usedScene": {
+     "abilities": [
+       "EntryAbility"
+     ],
+     "when": "always"
+    }
+  },
 ]
]
```
#### 在 entry 目录下添加申请权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "Access_Create_Audio",
+      "value": "access create Audio"
+    }，
  ]
}
```
## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                                                                                                              | Type                                                                                                                | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `mmss`         | Convert milliseconds to minute:second string                             | function(milliseconds:number): string                                 | No       |  Android，iOS      | yes               |
| `mmssss`         | Convert milliseconds to minute:second:milliseconds string          | function(milliseconds:number): string                                | No       |  Android，iOS       | yes               |
| `setSubscriptionDuration`       | Set default callback time when starting recorder or player. Default to 0.5 which is 500ms| function(seconds:float):void     | No       |  Android，iOS       | yes               |
| `addRecordBackListener`      |Get callback from native module. Will receive currentPosition, currentMetering (if configured in startRecorder).                                                                                      | function(callBack:(value:RecordBackType)=>void): void                                               | No       |  Android，iOS      | yes               |
| `removeRecordBackListener`      |Removes recordBack listener.            | function(): void                                     | No       |  Android，iOS       | yes               |
| `addPlayBackListener`        | Get callback from native module. Will receive duration, currentPosition.                  | function(callBack:(value: PlayBackType)=>void): void  | No       |  Android，iOS       | yes               |
| `removePlayBackListener`        | Removes playback listener.                                                     | function(): void               | No       |  Android，iOS       | yes               |
| `startRecorder`      |Start recording. Not passing uri will save audio in default location. | function(uri?:string,audioSets?: AudioSet,meteringEnabled?: boolean): Promise< string >               | No       | Android，iOS      | yes         |
| `pauseRecorder`     | Pause recording.                           | function() : Promise< string >                                        | No       | Android，iOS       | yes               |
| `resumeRecorder`           | Resume recording.     | function() : Promise< string >                                                                  | No       |  Android，iOS      | yes               |
| `stopRecorder` | Stop recording.                                        | function() : Promise< string >                                                                                                             | No       |  Android，iOS      | yes               |
| `startPlayer` | Start playing. Not passing the param will play audio in default location.                                        | function(uri?:string,httpHeaders?:Record<string,string>) : Promise< string >                                                                                                             | No       |  Android，iOS      | yes            |
| `stopPlayer` | Stop playing.                                      | function() : Promise< string >                                                                                                             | No       |  Android，iOS      | yes               |
| `pausePlayer` | Pause playing.                                      | function() : Promise< string >                                                                                                             | No       |  Android，iOS     | yes               |
| `resumePlayer` | Resume playing.                                       | function() : Promise< string >                                                                                                             | No       |  Android，iOS      | yes               |
| `seekToPlayer` | Seek audio.                                   | function(milliseconds:number) : Promise< string >                                                                                                             | No       |  Android，iOS      | yes               |
| `setVolume` | Set volume of audio player (default 1.0, range: 0.0 ~ 1.0).                                      | function(volume:float) : Promise< string >                                                                                                             | No       |  Android，iOS     | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/hyochan/react-native-audio-recorder-player/blob/main/LICENSE) ，请自由地享受和参与开源。
