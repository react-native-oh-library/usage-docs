> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-track-player</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/doublesymmetry/react-native-track-player">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/doublesymmetry/react-native-track-player/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-track-player)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-track-player Releases](https://github.com/react-native-oh-library/react-native-track-player/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-track-player@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-track-player@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect } from "react";
import { ScrollView, Text, Button, View, StyleSheet } from 'react-native';
import TrackPlayer from 'react-native-track-player';

const TrackPlayerDemo = () => {
    useEffect(() => {
        // Set up the player
        TrackPlayer.setupPlayer();
    }, []);

    const addExample = () => {
        TrackPlayer.add([
            {
                url: "https://ting8.yymp3.com/new27/chengxiang10/1.mp3",
                title: "世界这么大还是遇见你",
                artist: "程响",
                artwork: "https://rntp.dev/example/Longing.jpeg",
                duration: 237
            },
            {
                url: "https://ting8.yymp3.com/new18/fhzq4/8.mp3",
                title: "最炫民族风",
                artist: "凤凰传奇",
                artwork: "https://rntp.dev/example/Rhythm%20City%20(Demo).jpeg",
                duration: 283
            }, {
                url: "https://ting8.yymp3.com/new27/jinzhiwen3/1.mp3",
                title: "远走高飞",
                artist: "金志文",
                artwork: "https://rntp.dev/example/Rhythm%20City%20(Demo).jpeg",
                duration: 235
            }]);
    }

    // 开始播放歌曲
    const startExample = () => {
        // Start playing it
        TrackPlayer.play();
    }
    // 暂停播放歌曲
    const pauseExample = () => {
        TrackPlayer.pause();
    }
    return (
        <ScrollView>
            <View>
                <Text style={styles.text}>TrackPlayerDemo </Text>
                <View>
                    <Text style={styles.text}>添加Track</Text>
                    <Button
                        title="add"
                        color="#9a73ef"
                        onPress={addExample}
                    />
                </View>

                <View>
                    <Text style={styles.text}>播放Track</Text>
                    <Button
                        title="play"
                        color="#9a73ef"
                        onPress={startExample}
                    />
                </View>

                <View>
                    <Text style={styles.text}>暂停Track</Text>
                    <Button
                        title="pause"
                        color="#9a73ef"
                        onPress={pauseExample}
                    />
                </View>
            </View>
        </ScrollView>
    )
};

const styles = StyleSheet.create({
    text: {
        fontSize: 18,
        marginBottom: 10,
        color: 'red',
    },
});
export default TrackPlayerDemo;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-track-player": "file:../../node_modules/@react-native-oh-tpl/react-native-track-player/harmony/track_player.har"
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

### 3.在 ArkTs 侧引入 RNTrackPlayerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNTrackPlayerPackage } from "@react-native-oh-tpl/react-native-track-player/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTrackPlayerPackage(ctx)
  ];
}
```

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-track-player Releases](https://github.com/react-native-oh-library/react-native-track-player/releases)

### 权限要求

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"abilities": [
+  {
+    "backgroundModes": [
+      "audioPlayback"
+    ]
+  }
]

"requestPermissions": [
+  {
+    "name": "ohos.permission.KEEP_BACKGROUND_RUNNING",
+    "reason": "$string:app_name",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when": "always"
+    }
+  },
]
```


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                     | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| setupPlayer              | Initializes the player with the specified options.           | promise | yes      | Android/iOS | partially         |
| isServiceRunning         | This method should not be used, most methods reject when service is not bound. | promise | no       | Android/iOS | yes               |
| add                      | Adds a track to the queue.                                   | promise | no       | Android/iOS | yes               |
| load                     | Replaces the current track or loads the track as the first in the queue. | promise | no       | Android/iOS | yes               |
| move                     | Move a track within the queue.                               | promise | no       | Android/iOS | yes               |
| remove                   | Removes multiple tracks from the queue by their indexes.     | promise | no       | Android/iOS | yes               |
| removeUpcomingTracks     | Clears any upcoming tracks from the queue.                   | promise | no       | Android/iOS | yes               |
| skip                     | Skips to a track in the queue.                               | promise | no       | Android/iOS | yes               |
| skipToNext               | Skips to the next track in the queue.                        | promise | no       | Android/iOS | yes               |
| skipToPrevious           | Skips to the previous track in the queue.                    | promise | no       | Android/iOS | yes               |
| updateOptions            | Updates the configuration for the components.                | promise | no       | Android/iOS | no                |
| updateMetadataForTrack   | Updates the metadata of a track in the queue. If the current track is updated, the notification and the Now Playing Center will be updated accordingly. | promise | no       | Android/iOS | partially         |
| clearNowPlayingMetadata  | clear the metadata of a track in the  Now Playing.           | promise | no       | Android/iOS | partially         |
| updateNowPlayingMetadata | Updates the metadata content of  the Now Playing Center  without affecting the data stored for the current track. | promise | no       | Android/iOS | partially         |
| reset                    | Resets the player stopping the current track and clearing the queue. | promise | no       | Android/iOS | yes               |
| play                     | Plays or resumes the current track.                          | promise | no       | Android/iOS | yes               |
| pause                    | Pauses the current track.                                    | promise | no       | Android/iOS | yes               |
| stop                     | Stops the current track.                                     | promise | no       | Android/iOS | yes               |
| setPlayWhenReady         | Sets wether the player will play automatically when it is ready to do so. | promise | no       | Android/iOS | yes               |
| getPlayWhenReady         | Gets wether the player will play automatically when it is ready to do so. | promise | no       | Android/iOS | yes               |
| seekTo                   | Seeks to a specified time position in the current track.     | promise | no       | Android/iOS | yes               |
| seekBy                   | Seeks by a relative time offset in the current track.        | promise | no       | Android/iOS | yes               |
| setVolume                | Sets the volume of the player.                               | promise | no       | Android/iOS | yes               |
| setRate                  | Sets the playback rate.                                      | promise | no       | Android/iOS | partially         |
| setQueue                 | Sets the queue.                                              | promise | no       | Android/iOS | yes               |
| setRepeatMode            | Sets the queue repeat mode.                                  | promise | no       | Android/iOS | yes               |
| getVolume                | Gets the volume of the player as a number between 0 and 1.   | promise | no       | Android/iOS | yes               |
| getRate                  | Gets the playback rate where 0.5 would be half speed, 1 would be regular speed and 2 would be double speed etc. | promise | no       | Android/iOS | yes               |
| getTrack                 | Gets a track object from the queue.                          | promise | no       | Android/iOS | yes               |
| getQueue                 | Gets the whole queue.                                        | promise | no       | Android/iOS | yes               |
| getActiveTrackIndex      | Gets the index of the active track in the queue or undefined if there is no current track. | promise | no       | Android/iOS | yes               |
| getActiveTrack           | Gets the active track or undefined if there is no current track. | promise | no       | Android/iOS | yes               |
| getDuration              | Gets the duration of the current track in seconds.           | promise | no       | Android/iOS | yes               |
| getBufferedPosition      | Gets the buffered position of the current track in seconds.  | promise | no       | Android/iOS | yes               |
| getPosition              | Gets the playback position of the current track in seconds.  | promise | no       | Android/iOS | yes               |
| getProgress              | Gets information on the progress of the currently active track, including its current playback position in seconds, buffered position in seconds and duration in seconds. | promise | no       | Android/iOS | yes               |
| getPlaybackState         | Gets the playback state of the player.                       | promise | no       | Android/iOS | partially         |
| getRepeatMode            | Gets the queue repeat mode.                                  | promise | no       | Android/iOS | yes               |
| retry                    | Retries the current item when the playback state is `State.Error`. | promise | no       | Android/iOS | yes               |

**setupPlayer方法参数**

| Name    | Description                                | Type          | Required | Platform    | HarmonyOS Support |
| ------- | ------------------------------------------ | ------------- | -------- | ----------- | ----------------- |
| options | The options to initialize the player with. | PlayerOptions | no       | iOS/Android | no                |

**add方法参数**

| Name              | Description                           | Type               | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| track             | The track to add to the queue.        | AddTrack\|ATrack[] | yes      | iOS/Android | yes               |
| insertBeforeIndex | The index to insert the track before. | number             | no       | iOS/Android | yes               |

**load方法参数**

| Name  | Description        | Type  | Required | Platform    | HarmonyOS Support |
| ----- | ------------------ | ----- | -------- | ----------- | ----------------- |
| track | The track to load. | Track | Yes      | iOS/Android | Yes               |

**move方法参数**

| Name      | Description                         | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ----------------------------------- | ------ | -------- | ----------- | ----------------- |
| fromIndex | The index of the track to be moved. | number | Yes      | iOS/Android | Yes               |
| toIndex   | The index to move the track to.     | number | Yes      | iOS/Android | Yes               |

**remove方法参数**

| Name           | Description                           | Type             | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| indexOrIndexes | The index of the track to be removed. | number\|number[] | Yes      | iOS/Android | Yes               |

**skip方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| index           | The index of the track to skip to.          | number | Yes      | iOS/Android | Yes               |
| initialPosition | The initial position to seek to in seconds. | number | no       | iOS/Android | Yes               |

**skipToNext方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| initialPosition | The initial position to seek to in seconds. | number | no       | iOS/Android | Yes               |

**skipToPrevious方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| initialPosition | The initial position to seek to in seconds. | number | no       | iOS/Android | Yes               |

**updateOptions方法参数**

| Name                      | Description                 | Type          | Required | Platform    | HarmonyOS Support |
| ------------------------- | --------------------------- | ------------- | -------- | ----------- | ----------------- |
| alwaysPauseOnInterruption | always Pause OnInterruption | boolean       | no       | Android     | no                |
| options                   | The options to update.      | UpdateOptions | no       | iOS/Android | no                |

**updateMetadataForTrack方法参数**

| Name       | Description                                            | Type              | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| trackIndex | The index of the track whose metadata will be updated. | number            | Yes      | iOS/Android | Yes               |
| metadata   | The metadata to update.                                | TrackMetadataBase | Yes      | iOS/Android | partially         |

**updateNowPlayingMetadata方法参数**

| Name     | Description             | Type               | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------- | ------------------ | -------- | ----------- | ----------------- |
| metadata | The metadata to update. | NowPlayingMetadata | Yes      | iOS/Android | partially         |

**setPlayWhenReady方法参数**

| Name          | Description                                                  | Type    | Required | Platform    | HarmonyOS Support |
| ------------- | ------------------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| playWhenReady | This is the equivalent of calling `TrackPlayer.play()` when `playWhenReady = true` or `TrackPlayer.pause()` when `playWhenReady = false`. | boolean | Yes      | iOS/Android | Yes               |

**seekTo方法参数**

| Name     | Description                         | Type   | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------------- | ------ | -------- | ----------- | ----------------- |
| position | The position to seek to in seconds. | number | Yes      | iOS/Android | Yes               |

**seekBy方法参数**

| Name   | Description                            | Type   | Required | Platform    | HarmonyOS Support |
| ------ | -------------------------------------- | ------ | -------- | ----------- | ----------------- |
| offset | The time offset to seek by in seconds. | number | Yes      | iOS/Android | Yes               |

**setVolume方法参数**

| Name  | Description                             | Type   | Required | Platform    | HarmonyOS Support |
| ----- | --------------------------------------- | ------ | -------- | ----------- | ----------------- |
| level | The volume as a number between 0 and 1. | number | Yes      | iOS/Android | Yes               |

**setRate方法参数**

| Name | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| ---- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| rate | The playback rate to change to, where 0.5 would be half speed, 1 would be regular speed, 2 would be double speed etc. | number | Yes      | iOS/Android | partially         |

**setQueue方法参数**

| Name   | Description                     | Type    | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------- | ------- | -------- | ----------- | ----------------- |
| tracks | The tracks to set as the queue. | Track[] | Yes      | iOS/Android | Yes               |

**setRepeatMode方法参数**

| Name | Description             | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------------------- | ---------- | -------- | ----------- | ----------------- |
| mode | The repeat mode to set. | RepeatMode | Yes      | iOS/Android | Yes               |

**getTrack方法参数**

| Name  | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| index | The index of the track. | number | Yes      | iOS/Android | Yes               |

## 遗留问题

- [ ] 目前harmonyOS设置metadata仅支持现有API中参数，对于genre、rating、isLiveStream、elapsedTime四个参数均未适配harmonyOS Next。[issue#3](https://github.com/react-native-oh-library/react-native-track-player/issues/3)
- [ ] 目前仅支持setupPlayer接口的调用，不支持该接口携带的参数对播放器进行相关的设置，该接口参数均未适配harmonyOS Next。[issue#4](https://github.com/react-native-oh-library/react-native-track-player/issues/4)
- [ ] 目前harmonyOS中不支持获取buffering状态。[issue#5](https://github.com/react-native-oh-library/react-native-track-player/issues/5)
- [ ] 目前harmonyOS中支持九种固定的播放速率，其他播放速率均未问题适配harmonyOS Next。[issue#6](https://github.com/react-native-oh-library/react-native-track-player/issues/6)
- [ ] 目前harmonyOS不支持对播控中心的更新设置，updateOptions接口未适配harmonyOS Next。[issue#7](https://github.com/react-native-oh-library/react-native-track-player/issues/7)

## 其他

## 开源协议

本项目基于 [The Apache License(Apache)](https://github.com/doublesymmetry/react-native-track-player/blob/main/LICENSE) ，请自由地享受和参与开源。

