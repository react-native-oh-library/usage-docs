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

| Dependcies         | Version |
| :----------------- | :------ |
| react-native-video | >=2.0.0 |
| lodash             | ^4.16.4 |

本库依赖[@react-native-oh-tpl/react-native-video文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-video.md#link)以及简化开发的JS工具[lodash](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/lodash.md)

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
      		style = {styles.container}
         	videoStyle = {styles.video}
            source={{ uri: 'https://vjs.zencdn.net/v/oceans.mp4' }}
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

| Name                         | Description                                                  |     Type     | Required |  Platform   | HarmonyOS Support |
| ---------------------------- | ------------------------------------------------------------ | :----------: | :------: | :---------: | :---------------: |
| toggleResizeModeOnFullscreen | 如果为真，点击全屏按钮将使 `<Video />` 组件在覆盖/包含模式之间切换；如果您想自定义全屏行为，请设置为假。 |     Bool     |    no    | iOS/Android |        yes        |
| controlAnimationTiming       | 对控件进行动画处理的时间量（以毫秒为单位）。                 |     Int      |    no    | iOS/Android |        yes        |
| doubleTapTime                | 在此时间内点击两次（以毫秒为单位）被视为两次点击。在此时间到期之前，不会执行单击操作。 |     Int      |    no    | iOS/Android |        yes        |
| controlTimeout               | 在一段时间后隐藏控件（以毫秒为单位）                         |     Int      |    no    | iOS/Android |        yes        |
| scrubbing                    | 如果大于0，则在移动进度条时启用实时拖动。提供的值是拖动的最小时间步长，单位为毫秒。 |     Int      |    no    | iOS/Android |        yes        |
| showOnStart                  | 首次渲染时显示或隐藏控件。                                   |     Bool     |    no    | iOS/Android |        yes        |
| videoStyle                   | 附加到 `<Video>` 组件的 React Native StyleSheet 对象。       |  StyleSheet  |    no    | iOS/Android |        yes        |
| navigator                    | 当使用默认的 React Native 导航器并且没有覆盖 `onBack` 函数时，您需要将导航器传递给 VideoPlayer，以使其正常工作。 |  Navigator   |    no    | iOS/Android |        yes        |
| seekColor                    | 进度条的填充/处理颜色。                                      | String(#HEX) |    no    | iOS/Android |        yes        |
| style                        | 附加到视频父 `<View>` 的 React Native StyleSheet 对象。      |  StyleSheet  |    no    | iOS/Android |        yes        |
| tapAnywhereToPause           | 如果为真，则在视频上单击任意地方（控制区域以外）会在播放和暂停之间切换。 |     Bool     |    no    | iOS/Android |        yes        |
| disableFullscreen            | 是否隐藏全屏按钮图标                                         |     Bool     |    no    | iOS/Android |        yes        |
| disablePlayPause             | 是否隐藏播放暂停图标                                         |     Bool     |    no    | iOS/Android |        yes        |
| disableSeekbar               | 是否隐藏进度条图标                                           |     Bool     |    no    | iOS/Android |        yes        |
| disableVolume                | 是否隐藏音量控制图标                                         |     Bool     |    no    | iOS/Android |        yes        |
| disableTimer                 | 是否隐藏视频时间                                             |     Bool     |    no    | iOS/Android |        yes        |
| disableBack                  | 是否隐藏返回按钮图标                                         |     Bool     |    no    | iOS/Android |        yes        |
| onEnterFullscreen            | 当点击全屏按钮后，视频进入全屏时触发。                       |    event     |    no    | iOS/Android |        yes        |
| onExitFullscreen             | 当点击全屏按钮后，视频退出全屏时触发。                       |    event     |    no    | iOS/Android |        yes        |
| onHideControls               | 当控制组件消失时触发。                                       |    event     |    no    | iOS/Android |        yes        |
| onShowControls               | 当控制组件出现时触发。                                       |    event     |    no    | iOS/Android |        yes        |
| onError                      | 当加载视频时遇到错误时触发。                                 |    event     |    no    | iOS/Android |        yes        |
| onPause                      | 当点击播放/暂停按钮后，视频暂停时触发。                      |    event     |    no    | iOS/Android |        yes        |
| onPlay                       | 当点击播放/暂停按钮后，视频开始播放时触发。                  |    event     |    no    | iOS/Android |        yes        |
| onBack                       | 当点击返回按钮时触发，如果使用自定义导航，可以重写该功能。   |    event     |    no    | iOS/Android |        yes        |
| onEnd                        | 当视频播放完毕时触发。                                       |    event     |    no    | iOS/Android |        yes        |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/itsnubix/react-native-video-controls/blob/master/LICENSE) ，请自由地享受和参与开源。