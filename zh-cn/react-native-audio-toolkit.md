> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/audio-toolkit</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-audio-toolkit/react-native-audio-toolkit">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-audio-toolkit/react-native-audio-toolkit/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-audio-toolkit)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/audio-toolkit Releases](https://github.com/react-native-oh-library/react-native-audio-toolkit/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/audio-toolkit
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/audio-toolkit
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] # demo使用了三方库[@react-native-oh-tpl/react-native-slider](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-slider.md)

> [!TIP] # demo使用了权限三方库[@react-native-oh-tpl/react-native-permissions](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-permissions.md)

```tsx
import React, { Component } from 'react';
import { Button, PermissionsAndroid, Platform, StyleSheet, Switch, Text, View, ScrollView } from 'react-native';
import Slider from '@react-native-oh-tpl/react-native-slider';
import { Player, Recorder, MediaStates } from '@react-native-community/audio-toolkit';
import RTNPermissions, {RESULTS} from "@react-native-oh-tpl/react-native-permissions";

const filename = 'test.mp4';


type Props = {};

type State = {
  playPauseButton: string,
  recordButton: string,

  stopButtonDisabled: boolean,
  playButtonDisabled: boolean | undefined,
  recordButtonDisabled: boolean,

  recordPauseButtonDisabled: boolean,

  loopButtonStatus: boolean,
  progress: number,

  error: string | null
};

export default class App extends Component<Props, State> {
  player: Player | null = null;
  recorder: Recorder | null = null;
  lastSeek: number = 0;
  _progressInterval: NodeJS.Timeout | null = null;

  constructor(props: Props) {
    super(props);

    this.state = {
      playPauseButton: 'Preparing...',
      recordButton: 'Preparing...',

      stopButtonDisabled: true,
      playButtonDisabled: true,
      recordButtonDisabled: true,
      recordPauseButtonDisabled:true,

      loopButtonStatus: false,
      progress: 0,

      error: null
    };
  }

  componentWillMount() {
    this.player = null;
    this.recorder = null;
    this.lastSeek = 0;
    this._reloadPlayer();
    this._reloadRecorder();

    this._progressInterval = setInterval(() => {
      if (this.player && this._shouldUpdateProgressBar()) {
        let currentProgress = Math.max(0, this.player.currentTime) / this.player.duration;
        if (isNaN(currentProgress)) {
          currentProgress = 0;
        }
        this.setState({ progress: currentProgress });
      }
    }, 100);
  }

  componentWillUnmount() {
    if (this._progressInterval) {
      clearInterval(this._progressInterval);
    }
  }

  _shouldUpdateProgressBar() {
    // Debounce progress bar update by 200 ms
    return Date.now() - this.lastSeek > 200;
  }

  _updateState() {

    this.setState({
      playPauseButton: this.player && this.player.isPlaying ? 'Pause' : 'Play',
      recordButton: this.recorder && this.recorder.isRecording ? 'Stop' : 'Record',

      recordPauseButtonDisabled: !this.recorder || !this.recorder.isRecording,

      stopButtonDisabled: !this.player || !this.player.canStop,
      playButtonDisabled: !this.player || !this.player.canPlay || this.recorder?.isRecording,
      recordButtonDisabled: (!this.recorder || (this.player && !this.player.isStopped)) ?? true,
    });
  }

  _playPause() {
    this.player?.playPause((err, paused) => {
      if (err) {
        this.setState({
          error: err.message
        });
      }
      this._updateState();
    });
  }

  _stop() {
    this.player?.stop(() => {
      this._updateState();
    });
  }

  _seek(percentage: number) {
    if (!this.player) {
      return;
    }

    this.lastSeek = Date.now();
    let position = percentage * this.player.duration;

    this.player.seek(position, () => { });
  }

  _getPlayPath() {
    if (this.recorder) {
      return this.recorder.fsPath;
    }
    return filename;
  }

  _reloadPlayer() {
    if (this.player) {
      this.player.destroy();
    }
    this.player = new Player(this._getPlayPath(), {
      autoDestroy: false
    }).prepare((err) => {
      if (err) {
        console.log('error at _reloadPlayer():');
        console.log(err);
      } else {
        if (this.player) {
          this.player.looping = this.state.loopButtonStatus;
        }
      }

      this._updateState();
    });

    this._updateState();

    this.player.on('ended', () => {
      this._updateState();
    });
    this.player.on('pause', () => {
      this._updateState();
    });
  }

  _reloadRecorder() {
    if (this.recorder) {
      this.recorder.destroy();
    }

    this.recorder = new Recorder(filename, {
      bitrate: 256000,
      channels: 2,
      sampleRate: 44100,
      quality: 'max'
    });

    this._updateState();
  }

  _toggleRecord() {
    if(this.recorder && this.recorder.state === MediaStates.PAUSED){
      this.recorder?.record((err) => {
        this._updateState();
      })
      return
    }
    if (this.player) {
      this.player.destroy();
    }

    let recordAudioRequest;
    if (Platform.OS == 'android') {
      recordAudioRequest = this._requestRecordAudioPermission();
    } else if (Platform.OS === 'harmony') {
      recordAudioRequest = this._requestRecordAudioPermissionHs();
    } else {
      recordAudioRequest = new Promise(function (resolve, reject) { resolve(true); });
    }

    recordAudioRequest.then((hasPermission) => {
      if (!hasPermission) {
        this.setState({
          error: 'Record Audio Permission was denied'
        });
        return;
      }
     
      this.recorder?.toggleRecord((err, stopped) => {
        if (err) {
          this.setState({
            error: err.message
          });
        }
        if (stopped) {
          this._reloadPlayer();
          this._reloadRecorder();
        }
        this._updateState();
      });
    });
  }

  
  async _requestRecordAudioPermissionHs() {
    try {
      let check = await RTNPermissions.request('ohos.permission.MICROPHONE');
      console.info("RTNPermissions===== request", check);
      if (check === RESULTS.GRANTED) {
        return true;
      } else {
        return false;
      }
    } catch (err) {
      console.error(err);
      return false;
    }
  }

  async _requestRecordAudioPermission() {
    try {
      const granted = await PermissionsAndroid.request(
        PermissionsAndroid.PERMISSIONS.RECORD_AUDIO,
        {
          title: 'Microphone Permission',
          message: 'ExampleApp needs access to your microphone to test react-native-audio-toolkit.',
          buttonNeutral: 'Ask Me Later',
          buttonNegative: 'Cancel',
          buttonPositive: 'OK',
        },
      );
      if (granted === PermissionsAndroid.RESULTS.GRANTED) {
        return true;
      } else {
        return false;
      }
    } catch (err) {
      console.error(err);
      return false;
    }
  }

  _toggleLooping(value: boolean) {
    this.setState({
      loopButtonStatus: value
    });
    if (this.player) {
      this.player.looping = value;
    }
  }

  render() {
    return (
      <ScrollView>
        <View>
          <Text style={styles.title}>
            Playback
          </Text>
        </View>
        <View >
          <Button title={this.state.playPauseButton} disabled={this.state.playButtonDisabled} onPress={() => this._playPause()} />
          <Button title={'Stop'} disabled={this.state.stopButtonDisabled} onPress={() => this._stop()} />
        </View>
        <View style={styles.settingsContainer}>
          <Switch
            onValueChange={(value) => this._toggleLooping(value)}
            value={this.state.loopButtonStatus} />
          <Text>Toggle Looping</Text>
        </View>
        <View style={styles.slider}>
          <Slider step={0.0001} disabled={this.state.playButtonDisabled} onValueChange={(percentage) => this._seek(percentage)} value={this.state.progress} />
        </View>
        <View>
          <Text style={styles.title}>
            Recording
          </Text>
        </View>
        <View>
          <Button title={this.state.recordButton} disabled={this.state.recordButtonDisabled} onPress={() => this._toggleRecord()} />
        </View>
        
        <View style={styles.recordPause}>
          <Button title={'Pause recording'} disabled={this.state.recordPauseButtonDisabled} onPress={() => {
            this.recorder?.pause((err) => {
              this._updateState();
            })
          }} />
        </View>
        <View>
          <Text style={styles.errorMessage}>{this.state.error}</Text>
        </View>
      </ScrollView>
    );
  }
}

const styles = StyleSheet.create({
  slider: {
    height: 10,
    margin: 10,
    marginBottom: 30,
  },
  settingsContainer: {
    alignItems: 'center',
  },
  container: {
    borderRadius: 4,
    borderWidth: 0.5,
    borderColor: '#d6d7da',
  },
  title: {
    fontSize: 19,
    fontWeight: 'bold',
    textAlign: 'center',
    padding: 20,
  },
  errorMessage: {
    fontSize: 15,
    textAlign: 'center',
    padding: 10,
    color: 'red'
  },
  recordPause:{
    marginTop:15
  }
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-oh-tpl/audio-toolkit": "file:../../node_modules/@react-native-oh-tpl/audio-toolkit/harmony/audio_toolkit.har"
  }
```

### 3.在 ArkTs 侧引入 AudioModulesPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...

+   import { AudioModulesPackage } from "@react-native-oh-tpl/audio-toolkit/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new AudioModulesPackage(ctx)
  ];
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

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/audio-toolkit Releases](https://github.com/react-native-oh-library/react-native-audio-toolkit/releases/)

### 权限要求

- 如果 source 使用网络 url 应用需要申请网络权限

  在`entry/src/main/module.json5`中添加

```json
requestPermissions: [
  {
    name: "ohos.permission.INTERNET",
  },
],
```

- 如果使用录音功能，需要申请录音权限

  在`entry/src/main/module.json5`中添加

```json
requestPermissions: [
  {
      "name": "ohos.permission.MICROPHONE",
      "reason": "$string:EntryAbility_desc",
        "usedScene": {
          "abilities": [
            "MainAbility"
          ],
         "when": "inuse"
       }
    },
],
```

## Player

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name                        | Description                                                  | Type               | Default                     | Required | Platform | HarmonyOS Support |
| --------------------------- | ------------------------------------------------------------ | ------------------ | --------------------------- | -------- | -------- | ----------------- |
| autoDestroy                 | Boolean to indicate whether the player should self-destruct after playback is finished. If this is not set, you are responsible for destroying the object by calling player.destroy(). | boolean            | True                        | No       | All      | Yes               |
| continuesToPlayInBackground | (Android only) Should playback continue if app is sent to background?<br />iOS will always pause in this case. | boolean            | False                       | No       | Android  | Yes               |
| category                    | (iOS only) Define the audio session category<br /> Options: Playback, Ambient and SoloAmbient<br />More info about categories can be found here:<br /> https://developer.apple.com/documentation/avfoundation/avaudiosession/category | PlaybackCategories | PlaybackCategories.Playback | No       | IOS      | No                |
| mixWithOthers               | Boolean to determine whether other audio sources on the device will mix<br />with sounds being played back by this module. If this is not set, playback<br />of audio will stop other sources | boolean            | False                       | No       | Android<br />IOS   | No                |
| looping                     | Get/set looping status of the current file. If true, file will loop when playback reaches end of file. | boolean            | False                       | No       | All      | Yes               |
| volume                      | Get/set playback volume. The scale is from 0.0 (silence) to 1.0 (full volume). | Number             | 1.0                         | No       | All      | Yes               |
| speed                       | Get/set the playback speed for audio. NOTE: On Android, this is only supported on Android 6.0+. | Number             | 1.0                         | No       | All      | Yes               |

### 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| prepare   | Prepare playback of the file provided during initialization. This method is optional to call but might be useful to preload the file so that the file starts playing immediately when calling play(). Otherwise the file is prepared when calling play() which may result in a small delay.<br />Callback is called with empty first parameter when file is ready for playback with `play()`. If there was an error, the callback is called with an error object as first parameter. See Callbacks for more information. | function | No       | All      | Yes               |
| play      | Start playback.<br />If callback is given, it is called when playback has started. | function | No       | All      | Yes               |
| pause     | Pauses playback. Playback can be resumed by calling `play()` with no parameters.<br />Callback is called after the operation has finished. | function | No       | All      | Yes               |
| playPause | Helper method for toggling pause.<br />Callback is called after the operation has finished. Callback receives `Object error` as first argument, `Boolean paused` as second argument indicating if the player ended up playing (false) or paused (true). | function | No       | All      | Yes               |
| stop      | Stop playback.<br />  If `autoDestroy` option was set during initialization, clears all media resources from memory. In this case the player should no longer be used. | function | No       | All      | Yes               |
| destroy   | Stops playback and destroys the player. The player should no longer be used.<br />Callback is called after the operation has finished. | function | No       | All      | Yes               |
| seek      | Seek in currently playing media. `position` is the offset from the start.<br />If callback is given, it is called when the seek operation completes. If another seek operation is performed before the previous has finished, the previous operation gets an error in its callback with the `err` field set to `oldcallback`. The previous operation should likely do nothing in this case. | function | No       | All      | Yes               |

## Recorder

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### 属性

| Name             | Description                                                  | Type   | Default                     | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | ------ | --------------------------- | -------- | -------- | ----------------- |
| bitrate          | Set bitrate for the recorder, in bits per second             | Number | 128000                      | No       | All      | Yes               |
| channels         | Set number of channels                                       | Number | 2                           | No       | All      | Yes               |
| sampleRate       | Set how many samples per second                              | Number | 48000                       | No       | All      | Yes               |
| format           | Override format. Possible values:<br /> Cross-platform: 'mp4'<br />Android only: 'ogg', 'webm', 'amr'<br />HarmonyOS only: 'm4a' | String | based on filename extension | No       | All      | Yes               |
| encoder          | Override encoder. Android only.<br />Possible values:<br />'aac', 'mp4', 'webm', 'ogg', 'amr'<br />HarmonyOS only: 'aac'| String | based on filename extension | No       | Android      | partially               |
| quality          | Quality of the recording, iOS only.<br />Possible values: 'min', 'low', 'medium', 'high', 'max' | String | medium                      | No       | IOS       | No               |

### 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description                                                  | Type     | Required | Platform | HarmonyOS Support |
| ------- | ------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| prepare | Prepare recording to the file provided during initialization. This method is optional to call but it may be beneficial to call to make sure that recording begins immediately after calling record(). Otherwise the recording is prepared when calling record() which may result in a small delay. NOTE: Assume that this wipes the destination file immediately. | function | No       | All      | Yes               |
| record  | Start recording to file in `path`. Callback is called after recording has started or with error object if an error occurred. | function | No       | All      | Yes               |
| stop    | Stop recording and save the file. Callback is called after recording has stopped or with error object. The recorder is destroyed after calling stop and should no longer be used. | function | No       | All      | Yes               |
| destroy | Destroy the recorder. Should only be used if a recorder was constructed, and for some reason is now unwanted.<br />Callback is called after the operation has finished. | function | No       | All      | Yes               |

## 状态 state - Number (read only)


```json
var MediaStates = {
  DESTROYED: -2,
  ERROR: -1,
  IDLE: 0,
  PREPARING: 1,
  PREPARED: 2,
  SEEKING: 3,
  PLAYING: 4,   // only for Player
  RECORDING: 4, // only for Recorder
  PAUSED: 5
};
```

## 遗留问题

- [ ] Recorder的encoder属性问题：目前仅支持aac,待后续底层能力开放增加其他格式。[issue#15](https://github.com/react-native-oh-library/react-native-audio-toolkit/issues/15)

## 其他

- Player的category、mixWithOthers属性 HarmonyOS不支持

- Recorder的quality属性 HarmonyOS不支持

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-audio-toolkit/react-native-audio-toolkit/tree/master?tab=MIT-1-ov-file#readme) ，请自由地享受和参与开源。

