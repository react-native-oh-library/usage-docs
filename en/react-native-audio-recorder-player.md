> Template version: v0.2.2

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

> [!tip] [ GitHub address](https://github.com/react-native-oh-library/react-native-audio-recorder-player)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-audio-recorder-player Releases](https://github.com/react-native-oh-library/react-native-audio-recorder-player/releases).

Go to the project directory and execute the following instruction:

> [!tip] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-audio-recorder-player@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-audio-recorder-player@file:#
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!tip] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-audio-recorder-player": "file:../../node_modules/@react-native-oh-tpl/react-native-audio-recorder-player/harmony/audio_recorder_player.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!tip] or details, see [Directly Linking Source Code](/en/link-source-code.md).

### Configuring CMakeLists and Introducing RNAudioRecorderPlayerPackage

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### Introducing react-native-audio-recorder-player Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {RNAudioRecorderPlayerPackage} from '@react-native-oh-tpl/react-native-audio-recorder-player/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAudioRecorderPlayerPackage(ctx)
  ];
}
```

### Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-audio-recorder-player Releases](https://github.com/react-native-oh-library/react-native-audio-recorder-player/releases)

### Permission Requirements

#### Include applicable permissions in the module.json5 file within the entry directory.

Open the `entry/src/main/module.json5` file and add the following code:

```diff
...
"requestPermissions": [
+  {"name": "ohos.permission.INTERNET"},
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

#### Apply the reasons for applicable permission in the entry directory.

Open the `entry/src/main/resources/base/element/string.json` file and add the following code:

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

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                                                                      | Type                                                                                    | Required | Platform     | HarmonyOS Support |
| -------------------------- | ---------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------- | -------- | ------------ | ----------------- |
| `mmss`                     | Convert milliseconds to minute:second string                                                                     | function(milliseconds:number): string                                                   | No       | Android，iOS | yes               |
| `mmssss`                   | Convert milliseconds to minute:second:milliseconds string                                                        | function(milliseconds:number): string                                                   | No       | Android，iOS | yes               |
| `setSubscriptionDuration`  | Set default callback time when starting recorder or player. Default to 0.5 which is 500ms                        | function(seconds:float):void                                                            | No       | Android，iOS | yes               |
| `addRecordBackListener`    | Get callback from native module. Will receive currentPosition, currentMetering (if configured in startRecorder). | function(callBack:(value:RecordBackType)=>void): void                                   | No       | Android，iOS | yes               |
| `removeRecordBackListener` | Removes recordBack listener.                                                                                     | function(): void                                                                        | No       | Android，iOS | yes               |
| `addPlayBackListener`      | Get callback from native module. Will receive duration, currentPosition.                                         | function(callBack:(value: PlayBackType)=>void): void                                    | No       | Android，iOS | yes               |
| `removePlayBackListener`   | Removes playback listener.                                                                                       | function(): void                                                                        | No       | Android，iOS | yes               |
| `startRecorder`            | Start recording. Not passing uri will save audio in default location.                                            | function(uri?:string,audioSets?: AudioSet,meteringEnabled?: boolean): Promise< string > | No       | Android，iOS | yes               |
| `pauseRecorder`            | Pause recording.                                                                                                 | function() : Promise< string >                                                          | No       | Android，iOS | yes               |
| `resumeRecorder`           | Resume recording.                                                                                                | function() : Promise< string >                                                          | No       | Android，iOS | yes               |
| `stopRecorder`             | Stop recording.                                                                                                  | function() : Promise< string >                                                          | No       | Android，iOS | yes               |
| `startPlayer`              | Start playing. Not passing the param will play audio in default location.                                        | function(uri?:string,httpHeaders?:Record<string,string>) : Promise< string >            | No       | Android，iOS | yes               |
| `stopPlayer`               | Stop playing.                                                                                                    | function() : Promise< string >                                                          | No       | Android，iOS | yes               |
| `pausePlayer`              | Pause playing.                                                                                                   | function() : Promise< string >                                                          | No       | Android，iOS | yes               |
| `resumePlayer`             | Resume playing.                                                                                                  | function() : Promise< string >                                                          | No       | Android，iOS | yes               |
| `seekToPlayer`             | Seek audio.                                                                                                      | function(milliseconds:number) : Promise< string >                                       | No       | Android，iOS | yes               |
| `setVolume`                | Set volume of audio player (default 1.0, range: 0.0 ~ 1.0).                                                      | function(volume:float) : Promise< string >                                              | No       | Android，iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/hyochan/react-native-audio-recorder-player/blob/main/LICENSE).
