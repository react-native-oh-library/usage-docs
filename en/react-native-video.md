> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-video</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-video/react-native-video/tree/support/5.2.X">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-video/react-native-video/blob/support/5.2.X/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-video)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-video Releases](https://github.com/react-native-oh-library/react-native-video/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-video@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-video@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useRef } from "react";
import { View, ScrollView, StyleSheet, Text, TextInput } from "react-native";
import RNCVideo from "react-native-video";

function RNCVideoDemo() {
  const [muted, setMuted] = useState(true);
  const [paused, setPaused] = useState(false);
  const [repeat, setRepeat] = useState(true);
  const [disableFocus, setDisableFocus] = useState(false);
  const [uri, setUri] = useState(
    "https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4"
  );
  const [txt, setTxt] = useState("empty");
  const [resizeMode, setResizeMode] = useState("none");
  const [posterResizeMode, setPosterResizeMode] = useState("cover");
  const [seekSec, setSeekSec] = useState(5000);

  const [onVideoLoad, setOnVideoLoad] = useState("onVideoLoad");
  const [onVideoLoadStart, setOnVideoLoadStart] = useState("onVideoLoadStart");
  const [onVideoError, setOnVideoError] = useState("onVideoError");
  const [onVideoProgress, setOnVideoProgress] = useState("onVideoProgress");
  const [onVideoEnd, setOnVideoEnd] = useState("onVideoEnd");
  const [onVideoBuffer, setOnVideoBuffer] = useState("onVideoBuffer");
  const [onPlaybackStalled, setOnPlaybackStalled] = useState("onPlaybackStalled");
  const [onPlaybackResume, setOnPlaybackResume] = useState("onPlaybackResume");

  const videoRef = React.useRef<typeof RNCVideo>();

  const toggleMuted = () => {
    setMuted((prevMuted) => !prevMuted);
  };

  const togglePaused = () => {
    setPaused((prevPaused) => !prevPaused);
  };

  const toggleRepeat = () => {
    setRepeat((prevRepeat) => !prevRepeat);
  };

  const toggleDisableFocus = () => {
    setDisableFocus((prevDisableFocus) => !prevDisableFocus);
  };

  const firstVideo = () => {
    setUri((prevRepeat) => "https://vjs.zencdn.net/v/oceans.mp4");
  };

  const secondVideo = () => {
    // setUri((prevRepeat) => 'http://clips.vorwaerts-gmbh.de/big_buck_bunny.mp4');
    setUri(
      (prevRepeat) =>
        "https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4"
    );
  };

  const changeResizeMode = (resizeMode) => {
    setResizeMode((prevResizeMode) => resizeMode);
  };

  return (
    <ScrollView style={styles.container}>
      <View style={styles.container}>
        <Text style={styles.title}>网络视频demo</Text>
        <Text style={styles.labelB}>{onVideoLoad}</Text>
        <Text style={styles.label}>{onVideoError}</Text>
        <Text style={styles.label}>{onVideoLoadStart}</Text>
        <Text style={styles.labelB}>{onVideoProgress}</Text>
        <Text style={styles.label}>{onVideoEnd}</Text>
        <Text style={styles.label}>{onVideoBuffer}</Text>
        <Text style={styles.label}>{onPlaybackStalled}</Text>
        <Text style={styles.label}>{onPlaybackResume}</Text>
        <Text style={styles.title}>update source </Text>
        <View
          style={{
            flexDirection: "row",
            height: 40,
            padding: 0,
          }}
        >
          <Text
            style={{ backgroundColor: "blue", flex: 0.25 }}
            onPress={() => {
              setUri(
                "https://res.vmallres.com//uomcdn/CN/cms/202210/C75C7E20060F3E909F2998E13C3ABC03.mp4"
              );
              setPosterResizeMode("stretch");
            }}
          >
            切换net:vmallres
          </Text>
          <Text
            style={{ backgroundColor: "red", flex: 0.25 }}
            onPress={() => {
              setUri("https://vjs.zencdn.net/v/oceans.mp4");
              setPosterResizeMode("contain");
            }}
          >
            切换net:oceans
          </Text>
        </View>
        <Text style={styles.title}>set resizeMode </Text>
        <View
          style={{
            flexDirection: "row",
            height: 40,
            padding: 0,
          }}
        >
          <Text
            style={{ backgroundColor: "blue", flex: 0.25 }}
            onPress={() => {
              setResizeMode("none");
            }}
          >
            none
          </Text>
          <Text
            style={{ backgroundColor: "red", flex: 0.25 }}
            onPress={() => {
              setResizeMode("contain");
            }}
          >
            contain
          </Text>
          <Text
            style={{ backgroundColor: "yellow", flex: 0.25 }}
            onPress={() => {
              setResizeMode("stretch");
            }}
          >
            stretch
          </Text>
          <Text
            style={{ backgroundColor: "green", flex: 0.25 }}
            onPress={() => {
              setResizeMode("cover");
            }}
          >
            cover
          </Text>
        </View>
        <View
          style={{
            flexDirection: "row",
            flexWrap: "wrap",
            padding: 0,
          }}
        >
          <Text style={styles.title}>操作 </Text>
          <TextInput
            style={styles.prop_input}
            placeholder="input seek sec number:"
            multiline={false}
            maxLength={30}
            keyboardType="numeric"
            onChangeText={(text) => {
              const newText = text.replace(/[^\d]+/, "");
              setSeekSec(Number(newText));
            }}
            autoFocus={false}
          />
        </View>
        <View
          style={{
            flexDirection: "row",
            flexWrap: "wrap",
            padding: 0,
          }}
        >
          <Text
            style={styles.button_b}
            onPress={() => {
              videoRef.current?.seek(seekSec);
            }}
          >
            seek:{seekSec.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              togglePaused();
            }}
          >
            paused:{paused.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              toggleMuted();
            }}
          >
            muted:{muted.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              toggleRepeat();
            }}
          >
            repeat:{repeat.toString()}
          </Text>
          <Text
            style={styles.button_b}
            onPress={() => {
              toggleDisableFocus();
            }}
          >
            disableFocus:{disableFocus.toString()}
          </Text>
          <Text style={styles.button_b}>
            ReSizeMode:{resizeMode.toString()}
          </Text>
        </View>
        <RNCVideo
          style={styles.video}
          ref={videoRef}
          source={{ uri: uri, isNetwork: true }}
          paused={paused}
          muted={muted}
          resizeMode={resizeMode}
          repeat={repeat}
          volume={1}
          disableFocus={disableFocus}
          poster={
            "https://res.vmallres.com/pimages/uomcdn/CN/pms/202304/sbom/4002010007801/group/800_800_9B1356F1330EADDCB20D35D2AE1F46E0.jpg"
          }
         posterResizeMode={posterResizeMode}
          onLoad={(e) => {
            setOnVideoLoad(
              "onVideoLoad currentTime =" +
                e.currentPosition +
                "s duration =" +
                e.duration +
                "s width =" +
                e.naturalSize.width +
                " orientation =" +
                e.naturalSize.orientation
            );
            setOnVideoError("onVideoError error = ok");
          }}
          onLoadStart={(e) => {
            setOnVideoLoadStart(
              "onVideoLoadStart isNetwork =" +
                e.isNetwork +
                " type=" +
                e.type +
                " uri=" +
                e.uri
            );
          }}
          onProgress={(e) => {
            setOnVideoProgress(
              "onVideoProgress currentTime =" +
                e.currentTime +
                " playableDuration=" +
                e.playableDuration +
                " seekableDuration=" +
                e.seekableDuration
            );
          }}
          onError={(e) => {
            setOnVideoError("onVideoError error =" + e.error);
          }}
          onEnd={() => {
            setOnVideoEnd("onVideoEnd completed");
          }}
          onBuffer={(e) => {
            setOnVideoBuffer("onVideoBuffer :" + e.isBuffering);
          }}
          onPlaybackStalled={() => {
            setOnPlaybackStalled("onPlaybackStalled : true");
            setOnPlaybackResume("onPlaybackResume :false");
          }}
          onPlaybackResume={() => {
            setOnPlaybackStalled("onPlaybackStalled :false");
            setOnPlaybackResume("onPlaybackResume :true");
          }}
          onReadyForDisplay={() => {
            console.log(`onReadyForDisplay :setShowPoster(false)`);
          }}
        />
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  video: {
    width: "100%",
    height: 260,
  },
  container: {
    width: "100%",
    height: "100%",
    backgroundColor: "#f8f8f8",
  },
  title: {
    color: "white",
    width: "30%", // hack
    height: 30, // hack
  },
  label: {
    color: "gray",
    width: "100%", // hack
    minHeight: 20,
  },
  labelB: {
    color: "gray",
    width: "100%", // hack
    minHeight: 40,
  },
  button: {
    width: 160,
    height: 36,
    backgroundColor: "hsl(190, 50%, 70%)",
    paddingHorizontal: 16,
    paddingVertical: 8,
    borderRadius: 8,
  },
  buttonText: {
    width: "100%",
    height: "100%",
    fontWeight: "bold",
  },
  button_b: {
    paddingHorizontal: 8,
    paddingVertical: 6,
    borderRadius: 4,
    backgroundColor: "oldlace",
    alignSelf: "flex-start",
    marginHorizontal: "1%",
    marginBottom: 6,
    minWidth: "25%",
    minHeight: 20,
    textAlign: "center",
  },
  prop_input: {
    width: 160,
    height: 40,
    borderWidth: 1,
    backgroundColor: "white",
    color: "black",
    borderRadius: 8,
  },
});

export default RNCVideoDemo;
```

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
   ...
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-video": "file:../../node_modules/@react-native-oh-tpl/react-native-video/harmony/rn_video.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing RNCVideoPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-video/src/main/cpp" ./video)
# RNOH_BEGIN: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_video)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNCVideoPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNCVideoPackage>(ctx)
    };
}
```

### 4.Introducing RNCVideo Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

```diff
  ...
+ import { RNCVideo, RNC_VIDEO_TYPE } from "@react-native-oh-tpl/react-native-video"

@Builder
function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNC_VIDEO_TYPE) {
+   RNCVideo({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
 ...
}
...
```

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  ...
+ RNC_VIDEO_TYPE
  ];
```

### 5.Introducing RNCVideoPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNCVideoPackage } from '@react-native-oh-tpl/react-native-video/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCVideoPackage(ctx)
  ];
}
```

### 6.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-video Releases](https://github.com/react-native-oh-library/react-native-video/releases)

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

详情请查看[react-native-video 官方文档](https://github.com/react-native-video/react-native-video/blob/support/5.2.X/README.md)

| Name | Descriptio                 | Type   | Required  | Platform | HarmonyOS Support |
| ---- | -------------------------- | :----- | --------- | -------- |------------------ |
| `source`| Sets the media source. You can pass an asset loaded via require or an object with a uri.| object | Yes      | All                                                      | yes |
| `disableFocus`     | Determines whether video audio should override background music/audio in Android and HarmonyOS devices.<br/>**false (default)**                                                                                                                                                                                                             | boolean   | No       | Android Exoplayer                                        | yes                            |
| `muted`            | Controls whether the audio is muted.<br/>**false (default)** - Don't mute audio                                                                                                                                                                                                                                                             | boolean   | No       | All                                                      | yes                            |
| `paused`           | Controls whether the media is paused.<br/>**false (default)** - Don't pause the media                                                                                                                                                                                                                                                       | boolean   | No       | All                                                      | yes                            |
| `repeat`           | Determine whether to repeat the video when the end is reached.<br/>**false (default)** - Don't repeat the video                                                                                                                                                                                                                             | boolean   | No       | All                                                      | yes                            |
| `resizeMode`       | Determines how to resize the video when the frame doesn't match the raw video dimensions.<br/>**"none" (default)** - Don't apply resize                                                                                                                                                                                                     | string | No       | Android ExoPlayer, Android MediaPlayer, iOS, Windows UWP | yes                            |
| `volume`           | Adjust the volume.<br/>**1.0 (default)** - Play at full volume                                                                                                                                                                                                                                                                              | number | No       | All                                                      | yes                            |
| `poster`           | An image to display while the video is loading<br/>Value: string with a URL for the poster, e.g. "<https://baconmockup.com/300/200/>"                                                                                                                                                                                                       | string | No       | All                                                      | yes                            |
| `posterResizeMode` | Determines how to resize the poster image when the frame doesn't match the raw video dimensions..<br/>**"contain" (default)**- Scale the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or less than the corresponding dimension of the view (minus padding). | string | No       | All                                                      | yes                            |
| `allowsExternalPlayback` | Indicates whether the player allows switching to external playback mode such as AirPlay or HDMI.              | boolean   | No  | iOS | No |
| `audioOnly` | Indicates whether the player should only play the audio track and instead of displaying the video track, show the poster instead.  | boolean   | No  | All | No |
| `onPlaybackStalled` | The callback when the buffer starts caching, controls the display of the loading view  | boolean   | No  | Android | No |
| `onPlaybackResume` | The callback when the buffer ends caching, controlling the hiding of the loading view  | boolean   | No  | Android | No |
| `automaticallyWaitsToMinimizeStalling` | A Boolean value that indicates whether the player should automatically delay playback in order to minimize stalling. For clients linked against iOS 10.0 and later  | boolean   | No  | iOS | No |
| `bufferConfig` | Adjust the buffer settings. This prop takes an object with one or more of the properties listed below.  | object   | No  | Android | No |
| `controls` |Determines whether to show player controls.  | boolean   | No  | All | No |
| `currentPlaybackTime` |When playing an HLS live stream with a EXT-X-PROGRAM-DATE-TIME tag configured, then this property will contain the epoch value in msec.| string | No  | All | No |
| `filter` |Add video filter| string | No  | iOS | No |
| `filterEnabled` |Enable video filter.| string | No  | iOS | No |
| `fullscreen` |Controls whether the player enters fullscreen on play.| boolean | No  | iOS | No |
| `fullscreenAutorotate` |If a preferred fullscreenOrientation is set, causes the video to rotate to that orientation but permits rotation of the screen to orientation held by user. Defaults to TRUE.| boolean | No  | iOS | No |
| `fullscreenOrientation` |Full screen orientation is set.| string | No  | iOS | No |
| `headers` |Pass headers to the HTTP client. Can be used for authorization. Headers must be a part of the source object.| object | No  | Android | No |
| `hideShutterView` |Controls whether the ExoPlayer shutter view (black screen while loading) is enabled.| boolean | No  | Android | No |
| `id` |Set the DOM id element so you can use document.getElementById on web platforms. Accepts string values.| string | No  | All | No |
| `ignoreSilentSwitch` |Controls the iOS silent switch behavior| string | No  | iOS | No |
| `maxBitRate` |Sets the desired limit, in bits per second, of network bandwidth consumption when multiple video streams are available for a playlist.| number | No  | All | No |
| `minLoadRetryCount` |Sets the minimum number of times to retry loading data before failing and reporting an error to the application. Useful to recover from transient internet failures.| number | No  | Android | No |
| `mixWithOthers` |Controls how Audio mix with other apps.| string | No  | iOS | No |
| `pictureInPicture` |Determine whether the media should played as picture in picture.| boolean | No  | iOS | No |
| `playInBackground` |Determine whether the media should continue playing while the app is in the background. This allows customers to continue listening to the audio.| boolean | No  | All | No |
| `playWhenInactive` |Determine whether the media should continue playing when notifications or the Control Center are in front of the video.| boolean | No  | iOS | No |
| `preferredForwardBufferDuration` |The duration the player should buffer media from the network ahead of the playhead to guard against playback disruption. Sets the preferredForwardBufferDuration instance property on AVPlayerItem.| number | No  | iOS | No |
| `preventsDisplaySleepDuringVideoPlayback` |Controls whether or not the display should be allowed to sleep while playing the video. Default is not to allow display to sleep.| boolean | No  | All | No |
| `progressUpdateInterval` |Delay in milliseconds between onProgress events in milliseconds.| number | No  | iOS | No |
| `rate` |Speed at which the media should play.| number | No  | All | No |
| `reportBandwidth` |Determine whether to generate onBandwidthUpdate events. This is needed due to the high frequency of these events on ExoPlayer.| boolean | No  | Android | No |
| `selectedAudioTrack` |Configure which audio track, if any, is played.| object | No  | All | No |
| `selectedTextTrack` |Configure which text track (caption or subtitle), if any, is shown.| object | No  | All | No |
| `selectedVideoTrack` |Configure which video track should be played. By default, the player uses Adaptive Bitrate Streaming to automatically select the stream it thinks will perform best based on available bandwidth.| object | No  | Android | No |
| `stereoPan` |Adjust the balance of the left and right audio channels. Any value between –1.0 and 1.0 is accepted.| number | No  | Android | No |
| `textTracks` |Load one or more "sidecar" text tracks. This takes an array of objects representing each track. | object | No  | All | No |
| `trackId` |Configure an identifier for the video stream to link the playback context to the events emitted. | string | No  | Android | No |
| `useTextureView` |Controls whether to output to a TextureView or SurfaceView. | boolean | No  | Android | No |

## 事件回调

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                                                                                                          | Type     | Required | Platform                                         | HarmonyOS Support |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------ | :------- | -------- | ------------------------------------------------ | ----------------- |
| `onLoad`            | Callback function that is called when the media is loaded and ready to play.                                                         | function | No       | All                                              | yes               |
| `onLoadStart`       | Callback function that is called when the media starts loading.                                                                      | function | No       | All                                              | yes               |
| `onReadyForDisplay` | Callback function that is called when the first video frame is ready for display. This is when the poster is removed.                | function | No       | Android ExoPlayer, Android MediaPlayer, iOS, Web | yes               |
| `onProgress`        | Callback function that is called every progressUpdateInterval seconds with info about which position the media is currently playing. | function | No       | All                                              | yes               |
| `onEnd`             | Callback function that is called when the player reaches the end of the media.                                                       | function | No       | All                                              | yes               |
| `onError`           | Callback function that is called when the player experiences a playback error.                                                       | function | No       | All                                              | yes               |
| `onBuffer`          | Callback function that is called when the player buffers.                                                                            | function | No       | Android, iOS                                     | yes               |
| `onPlaybackStalled` | Callback function that is MediaPlayer MEDIA_INFO_BUFFERING_START     | function | No       | Android MediaPlayer                              | yes               |
| `onPlaybackResume`  | Callback function that is MediaPlayer MEDIA_INFO_BUFFERING_END | function | No    | Android MediaPlayer  | yes  |
| `onAudioBecomingNoisy`  | Callback function that is called when the audio is about to become 'noisy' due to a change in audio outputs. Typically this is called when audio output is being switched from an external source like headphones back to the internal speaker. It's a good idea to pause the media when this happens so the speaker doesn't start blasting sound. | function | No    | All  | No  |
| `onBandwidthUpdate` | Callback function that is called when the available bandwidth changes.     | function | No       | Android   | No  |
| `onExternalPlaybackChange` | Callback function that is called when external playback mode for current playing video has changed. Mostly useful when connecting/disconnecting to Apple TV – it's called on connection/disconnection.    | function | No       | iOS   | No  |
| `onFullscreenPlayerWillPresent` | Callback function that is called when the player is about to enter fullscreen mode.    | function | No       | All   | No  |
| `onFullscreenPlayerDidPresent` |Callback function that is called when the player has entered fullscreen mode.   | function | No       | All   | No  |
| `onFullscreenPlayerWillDismiss` |Callback function that is called when the player is about to exit fullscreen mode.   | function | No       | All   | No  |
| `onFullscreenPlayerDidDismiss` |Callback function that is called when the player has exited fullscreen mode.  | function | No       | All   | No  |
| `onLoadStart` |Callback function that is called when the media starts loading.  | function | No       | All   | No  |
| `onReadyForDisplay` |Callback function that is called when the first video frame is ready for display. This is when the poster is removed.  | function | No       | All   | No  |
| `onPictureInPictureStatusChanged` |Callback function that is called when picture in picture becomes active or inactive.  | function | No       | IOS   | No  |
| `onPlaybackRateChange` |Callback function that is called when the rate of playback changes - either paused or starts/resumes. | function | No       | All   | No  |
| `onSeek` |Callback function that is called when a seek completes. | function | No       | All   | No  |
| `onRestoreUserInterfaceForPictureInPictureStop` |Callback function that corresponds to Apple's restoreUserInterfaceForPictureInPictureStopWithCompletionHandler. Call restoreUserInterfaceForPictureInPictureStopCompleted inside of this function when done restoring the user | function | No       | iOS   | No  |
| `onTimedMetadata` |Callback function that is called when timed metadata becomes available | function | No       | All   | No  |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name     | Description                                                                      | Type     | Required | Platform | HarmonyOS Support |
| -------- | -------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `seek()` | Seek to the specified position represented by seconds. seconds is a float value. | function | No       | All      | yes               |
| `dismissFullscreenPlayer()` | Take the player out of fullscreen mode. | function | No       | All      | No              |
| `presentFullscreenPlayer()` | Put the player in fullscreen mode. | function | No       | All      | No              |
| `save()` | Save video to your Photos with current filter prop. Returns promise.| function | No       | iOS      | No              |
| `restoreUserInterfaceForPictureInPictureStop()` | This function corresponds to the completion handler in Apple's recovery user interface ForPictureInPictureStop. IMPORTANT: This function must be called after calling onRestoreUserInterfaceForPictureInPictureStop.| function | No       | iOS      | No              |

## Known Issues

- [x] source 暂时只支持在线 URL 资源问题： [issue#34](https://github.com/react-native-oh-library/react-native-video/issues/34)。
- [ ] react-native-video 部分属性和方法未实现 HarmonyOS 化： [issue#60](https://github.com/react-native-oh-library/react-native-video/issues/60)。

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/TheWidlarzGroup/react-native-video/blob/master/LICENSE).
