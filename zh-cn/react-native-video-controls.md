> 模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/itsnubix/react-native-video-controls)

## 安装与使用

> [!TIP] 需要配套的服务和三方依赖

react-native-video-controls依赖于以下三方库

| Dependencies       | Version |
| :----------------- | :------ |
| react-native-video | >=2.0.0 |
| lodash             | ^4.16.4 |

本库依赖[@react-native-oh-tpl/react-native-video](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-video.md#link)以及简化开发的JS工具[lodash](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/lodash.md)

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install --save react-native-video-controls
```

#### **yarn**

```bash
yarn add react-native-video-controls
```

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-video代码以及简化开发工具lodash，如已在 HarmonyOS 工程中引入过这些库，且版本无误则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-video文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-video.md#link)和[lodash文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/lodash.md)进行引入。安装完成后请在终端使用`npm list react-native-video`和`npm list lodash`查看video组件版本和lodash工具版本是否正确

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.28; SDK: HarmonyOS NEXT Developer Beta3 5.0.0.36(12 Beta3); IDE: DevEco Studio 5.0.3.535; ROM: 5.0.0.31;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!tip] "Name"列属性navigator在使用时，请参考本文档其他

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

## 遗留问题

## 其他

+ 源库未提供navigator属性功能实现也未提及该属性的依赖，但可由navigation相关库提供该属性的功能，在使用时请参照[react-navigation-stack文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-navigation-stack.md)和[react-navigation-native文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-navigation-native.md)引入navigation相关库。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/itsnubix/react-native-video-controls/blob/master/LICENSE) ，请自由地享受和参与开源。