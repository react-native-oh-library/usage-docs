> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-indicators</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-indicators">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-indicators/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-BSD-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/n4kz/react-native-indicators)

## Installation and Usage

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-indicators@0.17.0
```

#### **yarn**

```bash
yarn add react-native-indicators@0.17.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from 'react';
import { AppRegistry, StatusBar, View, Platform, Dimensions } from 'react-native';
import {
  BallIndicator,
  BarIndicator,
  DotIndicator,
  MaterialIndicator,
  PacmanIndicator,
  PulseIndicator,
  SkypeIndicator,
  UIActivityIndicator,
  WaveIndicator,
} from 'react-native-indicators';
const { width, height } = Dimensions.get('window');


 export class IndicatorsTestExample extends Component {
    render() {
      return (
        <View style={styles.container}>
          <View style={styles.row}>
            <View style={styles.flex}>
              <BallIndicator color='white' animationDuration={800} />
            </View>

            <View style={styles.flex}>
              <PulseIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <SkypeIndicator color='white' />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <WaveIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <WaveIndicator color='white' waveMode='outline' />
            </View>

            <View style={styles.flex}>
              <WaveIndicator color='white' count={2} waveFactor={0.1} />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <UIActivityIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <MaterialIndicator color='white' />
            </View>

            <View style={styles.flex}>
              <PacmanIndicator color='white' />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <BarIndicator color='white' count={5} />
            </View>
          </View>

          <View style={styles.row}>
            <View style={styles.flex}>
              <DotIndicator
                count={3}
                color='white'
                animationDuration={800}
              />
            </View>

            <View style={styles.flex}>
              <DotIndicator
                style={styles.reverse}
                count={3}
                color='white'
                animationDuration={800}
              />
            </View>
          </View>
        </View>
      );
    }
  }


const styles = {
  container: {
  height: height-100,
    backgroundColor: '#01579B',
    padding: 20,
  },

  row: {
    flex: 1,
    flexDirection: 'row',
  },

  reverse: {
    transform: [{
      rotate: '180deg',
    }],
  },

  flex: {
    flex: 1,
  },
};
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


### Common properties

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| animationEasing  | Animation easing function	   | Function  | NO | ALL      | YES |
| animationDuration  | 	Animation duration in ms     | Number | NO | ALL      | YES |
| animating  | 	Animation toggle    | Boolean | NO | ALL      | YES |
| interaction  | Animation is interaction  | Boolean | NO | ALL      | YES |
| hidesWhenStopped  | Hide when not animating   | Boolean | NO | ALL      | YES |

### BallIndicator

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |


### BarIndicator 

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### DotIndicator  

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### MaterialIndicator   

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| trackWidth  | Indicator track width    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### PacmanIndicator    

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### PulseIndicator     

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### SkypeIndicator    

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |
| minScale  | Minimum component scale    | Number  | NO | ALL      | YES |
| maxScale  | Maximum component scale    | Number  | NO | ALL      | YES |

### UIActivityIndicator    

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |

### WaveIndicator     

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| color  | Component color    | String  | NO | ALL      | YES |
| count  | Component count    | Number  | NO | ALL      | YES |
| size  | Base component size    | Number  | NO | ALL      | YES |
| waveFactor  | Wave base number   | Number  | NO | ALL      | YES |
| waveMode  | Wave appearance    | String  | NO | ALL      | YES |

## Known Issues

## Others

## License

This project is licensed under [The BSD License (BSD)](https://github.com/n4kz/react-native-indicators/blob/master/license.txt).