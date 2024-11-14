> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-track-player)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-track-player Releases](https://github.com/react-native-oh-library/react-native-track-player/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-track-player
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-track-player
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useEffect } from "react";
import { ScrollView, Text, Button, View, StyleSheet } from "react-native";
import TrackPlayer from "react-native-track-player";

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
        duration: 237,
      },
      {
        url: "https://ting8.yymp3.com/new18/fhzq4/8.mp3",
        title: "最炫民族风",
        artist: "凤凰传奇",
        artwork: "https://rntp.dev/example/Rhythm%20City%20(Demo).jpeg",
        duration: 283,
      },
      {
        url: "https://ting8.yymp3.com/new27/jinzhiwen3/1.mp3",
        title: "远走高飞",
        artist: "金志文",
        artwork: "https://rntp.dev/example/Rhythm%20City%20(Demo).jpeg",
        duration: 235,
      },
    ]);
  };

  const startExample = () => {
    // Start playing it
    TrackPlayer.play();
  };

  const pauseExample = () => {
    TrackPlayer.pause();
  };
  return (
    <ScrollView>
      <View>
        <Text style={styles.text}>TrackPlayerDemo </Text>
        <View>
          <Text style={styles.text}>添加Track</Text>
          <Button title="add" color="#9a73ef" onPress={addExample} />
        </View>

        <View>
          <Text style={styles.text}>播放Track</Text>
          <Button title="play" color="#9a73ef" onPress={startExample} />
        </View>

        <View>
          <Text style={styles.text}>暂停Track</Text>
          <Button title="pause" color="#9a73ef" onPress={pauseExample} />
        </View>
      </View>
    </ScrollView>
  );
};

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: "red",
  },
});
export default TrackPlayerDemo;
```

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-track-player": "file:../../node_modules/@react-native-oh-tpl/react-native-track-player/harmony/track_player.har"
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

### 3. Introducing RNTrackPlayerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-track-player Releases](https://github.com/react-native-oh-library/react-native-track-player/releases)

### Permission Requirements

#### Include applicable permissions in the module.json5 file within the entry directory.

Open the `entry/src/main/module.json5` file and add the following code:

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

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                                                                                                                                                               | Type    | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| setupPlayer              | Initializes the player with the specified options.                                                                                                                        | promise | yes      | Android/iOS | partially         |
| isServiceRunning         | This method should not be used, most methods reject when service is not bound.                                                                                            | promise | no       | Android/iOS | yes               |
| add                      | Adds a track to the queue.                                                                                                                                                | promise | no       | Android/iOS | yes               |
| load                     | Replaces the current track or loads the track as the first in the queue.                                                                                                  | promise | no       | Android/iOS | yes               |
| move                     | Move a track within the queue.                                                                                                                                            | promise | no       | Android/iOS | yes               |
| remove                   | Removes multiple tracks from the queue by their indexes.                                                                                                                  | promise | no       | Android/iOS | yes               |
| removeUpcomingTracks     | Clears any upcoming tracks from the queue.                                                                                                                                | promise | no       | Android/iOS | yes               |
| skip                     | Skips to a track in the queue.                                                                                                                                            | promise | no       | Android/iOS | yes               |
| skipToNext               | Skips to the next track in the queue.                                                                                                                                     | promise | no       | Android/iOS | yes               |
| skipToPrevious           | Skips to the previous track in the queue.                                                                                                                                 | promise | no       | Android/iOS | yes               |
| updateOptions            | Updates the configuration for the components.                                                                                                                             | promise | no       | Android/iOS | no                |
| updateMetadataForTrack   | Updates the metadata of a track in the queue. If the current track is updated, the notification and the Now Playing Center will be updated accordingly.                   | promise | no       | Android/iOS | partially         |
| clearNowPlayingMetadata  | clear the metadata of a track in the Now Playing.                                                                                                                         | promise | no       | Android/iOS | partially         |
| updateNowPlayingMetadata | Updates the metadata content of the Now Playing Center without affecting the data stored for the current track.                                                           | promise | no       | Android/iOS | partially         |
| reset                    | Resets the player stopping the current track and clearing the queue.                                                                                                      | promise | no       | Android/iOS | yes               |
| play                     | Plays or resumes the current track.                                                                                                                                       | promise | no       | Android/iOS | yes               |
| pause                    | Pauses the current track.                                                                                                                                                 | promise | no       | Android/iOS | yes               |
| stop                     | Stops the current track.                                                                                                                                                  | promise | no       | Android/iOS | yes               |
| setPlayWhenReady         | Sets wether the player will play automatically when it is ready to do so.                                                                                                 | promise | no       | Android/iOS | yes               |
| getPlayWhenReady         | Gets wether the player will play automatically when it is ready to do so.                                                                                                 | promise | no       | Android/iOS | yes               |
| seekTo                   | Seeks to a specified time position in the current track.                                                                                                                  | promise | no       | Android/iOS | yes               |
| seekBy                   | Seeks by a relative time offset in the current track.                                                                                                                     | promise | no       | Android/iOS | yes               |
| setVolume                | Sets the volume of the player.                                                                                                                                            | promise | no       | Android/iOS | yes               |
| setRate                  | Sets the playback rate.                                                                                                                                                   | promise | no       | Android/iOS | partially         |
| setQueue                 | Sets the queue.                                                                                                                                                           | promise | no       | Android/iOS | yes               |
| setRepeatMode            | Sets the queue repeat mode.                                                                                                                                               | promise | no       | Android/iOS | yes               |
| getVolume                | Gets the volume of the player as a number between 0 and 1.                                                                                                                | promise | no       | Android/iOS | yes               |
| getRate                  | Gets the playback rate where 0.5 would be half speed, 1 would be regular speed and 2 would be double speed etc.                                                           | promise | no       | Android/iOS | yes               |
| getTrack                 | Gets a track object from the queue.                                                                                                                                       | promise | no       | Android/iOS | yes               |
| getQueue                 | Gets the whole queue.                                                                                                                                                     | promise | no       | Android/iOS | yes               |
| getActiveTrackIndex      | Gets the index of the active track in the queue or undefined if there is no current track.                                                                                | promise | no       | Android/iOS | yes               |
| getActiveTrack           | Gets the active track or undefined if there is no current track.                                                                                                          | promise | no       | Android/iOS | yes               |
| getDuration              | Gets the duration of the current track in seconds.                                                                                                                        | promise | no       | Android/iOS | yes               |
| getBufferedPosition      | Gets the buffered position of the current track in seconds.                                                                                                               | promise | no       | Android/iOS | yes               |
| getPosition              | Gets the playback position of the current track in seconds.                                                                                                               | promise | no       | Android/iOS | yes               |
| getProgress              | Gets information on the progress of the currently active track, including its current playback position in seconds, buffered position in seconds and duration in seconds. | promise | no       | Android/iOS | yes               |
| getPlaybackState         | Gets the playback state of the player.                                                                                                                                    | promise | no       | Android/iOS | partially         |
| getRepeatMode            | Gets the queue repeat mode.                                                                                                                                               | promise | no       | Android/iOS | yes               |
| retry                    | Retries the current item when the playback state is `State.Error`.                                                                                                        | promise | no       | Android/iOS | yes               |

**setupPlayer 方法参数**

| Name    | Description                                | Type          | Required | Platform    | HarmonyOS Support |
| ------- | ------------------------------------------ | ------------- | -------- | ----------- | ----------------- |
| options | The options to initialize the player with. | PlayerOptions | no       | iOS/Android | no                |

**add 方法参数**

| Name              | Description                           | Type               | Required | Platform    | HarmonyOS Support |
| ----------------- | ------------------------------------- | ------------------ | -------- | ----------- | ----------------- |
| track             | The track to add to the queue.        | AddTrack\|ATrack[] | yes      | iOS/Android | yes               |
| insertBeforeIndex | The index to insert the track before. | number             | no       | iOS/Android | yes               |

**load 方法参数**

| Name  | Description        | Type  | Required | Platform    | HarmonyOS Support |
| ----- | ------------------ | ----- | -------- | ----------- | ----------------- |
| track | The track to load. | Track | Yes      | iOS/Android | Yes               |

**move 方法参数**

| Name      | Description                         | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ----------------------------------- | ------ | -------- | ----------- | ----------------- |
| fromIndex | The index of the track to be moved. | number | Yes      | iOS/Android | Yes               |
| toIndex   | The index to move the track to.     | number | Yes      | iOS/Android | Yes               |

**remove 方法参数**

| Name           | Description                           | Type             | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------- | ---------------- | -------- | ----------- | ----------------- |
| indexOrIndexes | The index of the track to be removed. | number\|number[] | Yes      | iOS/Android | Yes               |

**skip 方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| index           | The index of the track to skip to.          | number | Yes      | iOS/Android | Yes               |
| initialPosition | The initial position to seek to in seconds. | number | no       | iOS/Android | Yes               |

**skipToNext 方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| initialPosition | The initial position to seek to in seconds. | number | no       | iOS/Android | Yes               |

**skipToPrevious 方法参数**

| Name            | Description                                 | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| initialPosition | The initial position to seek to in seconds. | number | no       | iOS/Android | Yes               |

**updateOptions 方法参数**

| Name                      | Description                 | Type          | Required | Platform    | HarmonyOS Support |
| ------------------------- | --------------------------- | ------------- | -------- | ----------- | ----------------- |
| alwaysPauseOnInterruption | always Pause OnInterruption | boolean       | no       | Android     | no                |
| options                   | The options to update.      | UpdateOptions | no       | iOS/Android | no                |

**updateMetadataForTrack 方法参数**

| Name       | Description                                            | Type              | Required | Platform    | HarmonyOS Support |
| ---------- | ------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| trackIndex | The index of the track whose metadata will be updated. | number            | Yes      | iOS/Android | Yes               |
| metadata   | The metadata to update.                                | TrackMetadataBase | Yes      | iOS/Android | partially         |

**updateNowPlayingMetadata 方法参数**

| Name     | Description             | Type               | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------- | ------------------ | -------- | ----------- | ----------------- |
| metadata | The metadata to update. | NowPlayingMetadata | Yes      | iOS/Android | partially         |

**setPlayWhenReady 方法参数**

| Name          | Description                                                                                                                               | Type    | Required | Platform    | HarmonyOS Support |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| playWhenReady | This is the equivalent of calling `TrackPlayer.play()` when `playWhenReady = true` or `TrackPlayer.pause()` when `playWhenReady = false`. | boolean | Yes      | iOS/Android | Yes               |

**seekTo 方法参数**

| Name     | Description                         | Type   | Required | Platform    | HarmonyOS Support |
| -------- | ----------------------------------- | ------ | -------- | ----------- | ----------------- |
| position | The position to seek to in seconds. | number | Yes      | iOS/Android | Yes               |

**seekBy 方法参数**

| Name   | Description                            | Type   | Required | Platform    | HarmonyOS Support |
| ------ | -------------------------------------- | ------ | -------- | ----------- | ----------------- |
| offset | The time offset to seek by in seconds. | number | Yes      | iOS/Android | Yes               |

**setVolume 方法参数**

| Name  | Description                             | Type   | Required | Platform    | HarmonyOS Support |
| ----- | --------------------------------------- | ------ | -------- | ----------- | ----------------- |
| level | The volume as a number between 0 and 1. | number | Yes      | iOS/Android | Yes               |

**setRate 方法参数**

| Name | Description                                                                                                           | Type   | Required | Platform    | HarmonyOS Support |
| ---- | --------------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| rate | The playback rate to change to, where 0.5 would be half speed, 1 would be regular speed, 2 would be double speed etc. | number | Yes      | iOS/Android | partially         |

**setQueue 方法参数**

| Name   | Description                     | Type    | Required | Platform    | HarmonyOS Support |
| ------ | ------------------------------- | ------- | -------- | ----------- | ----------------- |
| tracks | The tracks to set as the queue. | Track[] | Yes      | iOS/Android | Yes               |

**setRepeatMode 方法参数**

| Name | Description             | Type       | Required | Platform    | HarmonyOS Support |
| ---- | ----------------------- | ---------- | -------- | ----------- | ----------------- |
| mode | The repeat mode to set. | RepeatMode | Yes      | iOS/Android | Yes               |

**getTrack 方法参数**

| Name  | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| index | The index of the track. | number | Yes      | iOS/Android | Yes               |

## Known Issues

- [ ] 目前 harmonyOS 设置 metadata 仅支持现有 API 中参数，对于 genre、rating、isLiveStream、elapsedTime 四个参数均未适配 harmonyOS Next。[issue#3](https://github.com/react-native-oh-library/react-native-track-player/issues/3)
- [ ] 目前仅支持 setupPlayer 接口的调用，不支持该接口携带的参数对播放器进行相关的设置，该接口参数均未适配 harmonyOS Next。[issue#4](https://github.com/react-native-oh-library/react-native-track-player/issues/4)
- [ ] 目前 harmonyOS 中不支持获取 buffering 状态。[issue#5](https://github.com/react-native-oh-library/react-native-track-player/issues/5)
- [ ] 目前 harmonyOS 中支持九种固定的播放速率，其他播放速率均未问题适配 harmonyOS Next。[issue#6](https://github.com/react-native-oh-library/react-native-track-player/issues/6)
- [ ] 目前 harmonyOS 不支持对播控中心的更新设置，updateOptions 接口未适配 harmonyOS Next。[issue#7](https://github.com/react-native-oh-library/react-native-track-player/issues/7)

## Others

## License

This project is licensed under [The Apache License(Apache)](https://github.com/doublesymmetry/react-native-track-player/blob/main/LICENSE).
