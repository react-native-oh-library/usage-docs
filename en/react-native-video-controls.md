> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-video-controls</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/itsnubix/react-native-video-controls">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/itsnubix/react-native-video-controls/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/itsnubix/react-native-video-controls)

## Installation and Usage

> [!TIP] Need matching services and third-party dependencies.

react-native-video-controls depends on the follow third-party library:

| Dependencies       | Version |
| :----------------- | :------ |
| react-native-video | >=2.0.0 |
| lodash             | ^4.16.4 |

The library depends on [@react-native-oh-tpl/react-native-video](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-video.md#link) and simplify development JS tool [lodash](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/lodash.md)

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install --save react-native-video-controls
```

#### **yarn**

```bash
yarn add react-native-video-controls
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, StyleSheet } from "react-native";
import VideoPlayer from 'react-native-video-controls';

const App = () => {
  function handleOnBack() {
    alert("this is onBack event test,because navigator properties depends on others parity");
  }
  return(
      <View>
       <VideoPlayer
      		title = 'oceans'
      		style = {styles.container}
         	videoStyle = {styles.video}
            source = {{ uri: 'https://vjs.zencdn.net/v/oceans.mp4' }}
            toggleResizeModeOnFullscreen = {true}
            controlAnimationTiming = {3000}
            doubleTapTime = {10}
            controlTimeout = {4000}
            scrubbing = {5}
			onBack = {handleOnBack}
            showOnStart = {false}
            seekColor = {'#00FFFF'}
            tapAnywhereToPause = {true}
        />
     </View>
    );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#000',
  }, 
  video: {  
    width: '100%',  
    height: '100%',  
  },
});

export default App;
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-video. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-video to add it to your project.

If not introduce the library, please refer to [@react-native-oh-tpl/react-native-video document](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-video.md#link) and [lodash document](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/lodash.md) for introducing。After finished installation, please use command `npm list react-native-video` and `npm list lodash` in terminal, and check if the component video version and lodash tool version are correct.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.28; SDK: HarmonyOS NEXT Developer Beta3 5.0.0.36(12 Beta3); IDE: DevEco Studio 5.0.3.535; ROM: 5.0.0.31;

## Properties

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip]  If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!tip] While Name column property navigator is in usage, please refer to this document's others.

| Name                         | Description                                                  |     Type     | Required |  Platform   | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------ | :----------: | :------: | :---------: | :---------------: |
| toggleResizeModeOnFullscreen | If true, clicking the fullscreen button will toggle the `<Video />` component between cover/contain, set to false if you want to customize fullscreen behaviour |     Bool     |    no    | iOS/Android |        yes        |
| controlAnimationTiming       | The amountof time (in milliseconds) to animate the controls in and out. |     Int      |    no    | iOS/Android |        yes        |
| doubleTapTime                | Tapping twice within this amount of time in milliseconds is considered a double tap. Single taps will not be actioned until this time has expired. |     Int      |    no    | iOS/Android |        yes        |
| controlTimeout               | Hide controls after X amount of time in milliseconds         |     Int      |    no    | iOS/Android |        yes        |
| scrubbing                    | If > 0, enable live scrubbing when moving the seek bar. The provided value is the minimum time step of the scrubbing in milliseconds. |     Int      |    no    | iOS/Android |        yes        |
| showOnStart                  | Show or hide the controls on first render                    |     Bool     |    no    | iOS/Android |        yes        |
| videoStyle                   | React Native StyleSheet object that is appended to the `<Video>` component |  StyleSheet  |    no    | iOS/Android |        yes        |
| navigator                    | When using the default React Native navigator and do not override the `onBack` function, you'll need to pass the navigator to the VideoPlayer for it to function |  Navigator   |    no    | iOS/Android |        yes        |
| seekColor                    | Fill/handle colour of the seekbar                            | String(#HEX) |    no    | iOS/Android |        yes        |
| style                        | React Native StyleSheet object that is appended to the video's parent `<View>` |  StyleSheet  |    no    | iOS/Android |        yes        |
| tapAnywhereToPause           | If true, single tapping anywhere on the video (other than a control) toggles between playing and paused. |     Bool     |    no    | iOS/Android |        yes        |
| disableFullscreen            | Hide the fullscreen button                                   |     Bool     |    no    | iOS/Android |        yes        |
| disablePlayPause             | Hide the play/pause toggle                                   |     Bool     |    no    | iOS/Android |        yes        |
| disableSeekbar               | Hide the seekbar                                             |     Bool     |    no    | iOS/Android |        yes        |
| disableVolume                | Hide the Volume control                                      |     Bool     |    no    | iOS/Android |        yes        |
| disableTimer                 | Hide the timer                                               |     Bool     |    no    | iOS/Android |        yes        |
| disableBack                  | Hide the back button                                         |     Bool     |    no    | iOS/Android |        yes        |
| onEnterFullscreen            | Fired when the video enters fullscreen after the fullscreen button is pressed |    Event     |    no    | iOS/Android |        yes        |
| onExitFullscreen             | Fired when the video exits fullscreen after the fullscreen button is pressed |    Event     |    no    | iOS/Android |        yes        |
| onHideControls               | Fired when the controls disappear                            |    Event     |    no    | iOS/Android |        yes        |
| onShowControls               | Fired when the controls appear                               |    Event     |    no    | iOS/Android |        yes        |
| onError                      | Fired when an error is encountered when loading the video    |    Event     |    no    | iOS/Android |        yes        |
| onPause                      | Fired when the video is paused after the play/pause button is pressed |    Event     |    no    | iOS/Android |        yes        |
| onPlay                       | Fired when the video begins playing after the play/pause button is pressed |    Event     |    no    | iOS/Android |        yes        |
| onBack                       | Function fired when back button is pressed, override if using custom navigation |    Event     |    no    | iOS/Android |        yes        |
| onEnd                        | Fired when the video is complete                             |    Event     |    no    | iOS/Android |        yes        |

## Known Issues

## Others

+ If Source library doesn't offer navigator property function and not offer this property's dependency, navigation related library can offer this property functions. For the usage please refer to [react-navigation-stack document](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-navigation-stack.md) and [react-navigation-native document](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-navigation-native.md) introducing navigation related library.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/itsnubix/react-native-video-controls/blob/master/LICENSE).