> Template version: v0.2.1

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




> [!TIP] [GitHub address](https://github.com/glepur/react-native-swipe-gestures)

## Installation and Usage

Go to the project directory and execute the following instruction:

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

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

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

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## Properties (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

Can be passed within optional `config` property.

| Params                     | Default | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| -------------------------- | ------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| velocityThreshold          | 0.3     | Velocity that has to be breached in order for swipe to be triggered (`vx` and `vy` properties of `gestureState`) | Number | No       | IOS/Android | yes               |
| directionalOffsetThreshold | 80      | Absolute offset that shouldn't be breached for swipe to be triggered (`dy` for horizontal swipe, `dx` for vertical swipe) | Number | No       | IOS/Android | yes               |
| gestureIsClickThreshold    | 5       | Absolute distance that should be breached for the gesture to not be considered a click (`dx` or `dy` properties of `gestureState`) | Number | No       | IOS/Android | yes               |

## Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| name         | Params       | Description                              | Type   | Required | Platform    | HarmonyOS Suppor |
| ------------ | ------------ | ---------------------------------------- | ------ | -------- | ----------- | ---------------- |
| onSwipe      | gestureState | gestureState received from PanResponder  | Object | No       | IOS/Android | yes              |
| onSwipeUp    | gestureState | Received up gesture from PanResponder    | Object | No       | IOS/Android | yes              |
| onSwipeDown  | gestureState | Received down gesture from PanResponder  | Object | No       | IOS/Android | yes              |
| onSwipeLeft  | gestureState | Received left gesture from PanResponder  | Object | No       | IOS/Android | yes              |
| onSwipeRight | gestureState | Received right gesture from PanResponder | Object | No       | IOS/Android | yes              |

## Known Issues

## Others

## License
This project is licensed under [The MIT License (MIT)](https://github.com/glepur/react-native-swipe-gestures?tab=MIT-1-ov-file).