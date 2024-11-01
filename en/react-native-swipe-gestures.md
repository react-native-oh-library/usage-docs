> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-swipe-gestures</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/glepur/react-native-swipe-gestures">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/glepur/react-native-swipe-gestures?tab=MIT-1-ov-file">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>




> [!TIP] [Github 地址](https://github.com/glepur/react-native-swipe-gestures)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

####  npm

```bash
npm install react-native-swipe-gestures@^1.0.5
```

#### yarn

```bash
yarn add react-native-swipe-gestures@^1.0.5
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
'use strict';

import React, {Component} from 'react';
import {View, Text} from 'react-native';
import GestureRecognizer, {swipeDirections} from 'react-native-swipe-gestures';

class SomeComponent extends Component {

  constructor(props) {
    super(props);
    this.state = {
      myText: 'I\'m ready to get swiped!',
      gestureName: 'none',
      backgroundColor: '#fff'
    };
  }

  onSwipeUp(gestureState) {
    this.setState({myText: 'You swiped up!'});
  }

  onSwipeDown(gestureState) {
    this.setState({myText: 'You swiped down!'});
  }

  onSwipeLeft(gestureState) {
    this.setState({myText: 'You swiped left!'});
  }

  onSwipeRight(gestureState) {
    this.setState({myText: 'You swiped right!'});
  }

  onSwipe(gestureName, gestureState) {
    const {SWIPE_UP, SWIPE_DOWN, SWIPE_LEFT, SWIPE_RIGHT} = swipeDirections;
    this.setState({gestureName: gestureName});
    switch (gestureName) {
      case SWIPE_UP:
        this.setState({backgroundColor: 'red'});
        break;
      case SWIPE_DOWN:
        this.setState({backgroundColor: 'green'});
        break;
      case SWIPE_LEFT:
        this.setState({backgroundColor: 'blue'});
        break;
      case SWIPE_RIGHT:
        this.setState({backgroundColor: 'yellow'});
        break;
    }
  }

  render() {

    const config = {
      velocityThreshold: 0.3,
      directionalOffsetThreshold: 80
    };

    return (
      <GestureRecognizer
        onSwipe={(direction, state) => this.onSwipe(direction, state)}
        onSwipeUp={(state) => this.onSwipeUp(state)}
        onSwipeDown={(state) => this.onSwipeDown(state)}
        onSwipeLeft={(state) => this.onSwipeLeft(state)}
        onSwipeRight={(state) => this.onSwipeRight(state)}
        config={config}
        style={{
          flex: 1,
          backgroundColor: this.state.backgroundColor
        }}
        >
        <Text>{this.state.myText}</Text>
        <Text>onSwipe callback received gesture: {this.state.gestureName}</Text>
      </GestureRecognizer>
    );
  }
}

export default SomeComponent;
```

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

Can be passed within optional `config` property.

| Params                     | Default | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| velocityThreshold          | 0.3     | Velocity that has to be breached in order for swipe to be triggered (`vx` and `vy` properties of `gestureState`) | Number | No       | IOS/Android | yes               |
| directionalOffsetThreshold | 80      | Absolute offset that shouldn't be breached for swipe to be triggered (`dy` for horizontal swipe, `dx` for vertical swipe) | Number | No       | IOS/Android | yes               |
| gestureIsClickThreshold    | 5       | Absolute distance that should be breached for the gesture to not be considered a click (`dx` or `dy` properties of `gestureState`) | Number | No       | IOS/Android | yes               |

## Methods

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| name         | Params       | Description                              | Type   | Required | Platform    | HarmonyOS Suppor |
| ------------ | ------------ | ---------------------------------------- | ------ | -------- | ----------- | ---------------- |
| onSwipe      | gestureState | gestureState received from PanResponder  | Object | No       | IOS/Android | yes              |
| onSwipeUp    | gestureState | Received up gesture from PanResponder    | Object | No       | IOS/Android | yes              |
| onSwipeDown  | gestureState | Received down gesture from PanResponder  | Object | No       | IOS/Android | yes              |
| onSwipeLeft  | gestureState | Received left gesture from PanResponder  | Object | No       | IOS/Android | yes              |
| onSwipeRight | gestureState | Received right gesture from PanResponder | Object | No       | IOS/Android | yes              |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/glepur/react-native-swipe-gestures?tab=MIT-1-ov-file) ，请自由地享受和参与开源。