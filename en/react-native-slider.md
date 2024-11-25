> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-slider</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jeanregisser/react-native-slider">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jeanregisser/react-native-slider/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/jeanregisser-react-native-slider/tree/sig)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/jeanregisser-react-native-slider Releases](https://github.com/react-native-oh-library/jeanregisser-react-native-slider/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm i @react-native-oh-tpl/react-native-slider
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-slider
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState} from 'react';
import {Button, View, StyleSheet, Text } from 'react-native';
import Slider from 'react-native-slider';


export function SliderExample() {
    const [isCheckerboardVisible, setIsCheckerboardVisible] = useState(false);
    const [value, setValue] = useState(0.200);
    return (
        <View style={styles.sectionContainer}>
        <Text>default style</Text>
        <Slider value={0.2}/>

        <Text>with min,max and custom tints</Text>
        <Slider
         value={0.2}
         minimumTrackTintColor = '#1A9274'
         maximumTrackTintColor = '#D3D3D3'
         thumbTintColor = '#1A9274'
         />

        <Text>with style,thumbStyle,thumbStyle</Text>
        <Slider
         value={0.2}
         minimumTrackTintColor = '#1073FF'
         thumbTintColor = '#FFFFFF'
         style = {styles.style}
         trackStyle = {styles.trackStyle}
         thumbStyle = {styles.thumbStyle}
         />

        <Text>with thumbTouchSize,event</Text>
        <Slider
            value={0.2}
            thumbTintColor = '#1A9FF4'
            thumbTouchSize = {{width: 40, height: 40}}
            onValueChange={(val: number) => {
                console.log('===Slider onValueChange: ' + value);
            }}

            onSlidingStart={() => {
                console.log('===Slider onSlidingStart');
            }}

            onSlidingComplete={() => {
                console.log('===Slider onSlidingComplete');
            }}
        />

        <Text>with thumbImage</Text>
        <Slider
            value={0.2}
            thumbTouchSize = {{width: 40, height: 40}}
            thumbStyle = {styles.thumbStyle}
            thumbImage = {require('./resources/slider.png')}
        />

        <Text>with animateTransitions</Text>
        <Slider
            value={value}
            thumbTouchSize = {{width: 40, height: 40}}
            trackStyle = {styles.trackStyle}
            thumbStyle = {styles.thumbStyle}
          // thumbImage = {{uri: 'https://developer.harmonyos.com/assets/image/diqiu.png'}}
            animateTransitions = {true}
            animationType = 'timing'
            animationConfig = {{
              toValue: 1,
              duration: 1500,
              useNativeDriver: false,
            }}
        />

        <Button onPress={()=>{
            setValue(0.9);
        }}
        title="Animation test"
        color="#841584"
        />
        </View>
    );
}

const styles = StyleSheet.create({
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
    style: {
        backgroundColor: '#EECBA8',
    },
    trackStyle: {
        backgroundColor: '#D2D2D2',
        height:3
    },
    thumbStyle: {
        backgroundColor: '#F3F3F3',
        width: 30,
        height: 30,
        borderRadius: 15,
    }
  });
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/jeanregisser-react-native-slider Releases](https://github.com/react-native-oh-library/jeanregisser-react-native-slider/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                                                                                                                                   | Type                                                                    | Required | Platform    | HarmonyOS Support |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------|----------|-------------|-------------------|
| value                 | Initial value of the slider.                                                                                                                                                                                  | number                                                                  | No       | iOS Android | yes               |
| disabled              | If true the user won't be able to move the slider.                                                                                                                                                            | bool                                                                    | No       | iOS Android | yes               |
| minimumValue          | Initial minimum value of the slider.                                                                                                                                                                          | number                                                                  | No       | iOS Android | yes               |
| maximumValue          | Initial maximum value of the slider.                                                                                                                                                                          | number                                                                  | No       | iOS Android | yes               |
| step                  | Step value of the slider. The value should be between 0 and maximumValue - minimumValue).                                                                                                                     | number                                                                  | No       | iOS Android | yes               |
| minimumTrackTintColor | The color used for the track to the left of the button.                                                                                                                                                       | string                                                                  | No       | iOS Android | yes               |
| maximumTrackTintColor | The color used for the track to the right of the button.                                                                                                                                                      | string                                                                  | No       | iOS Android | yes               |
| thumbTintColor        | The color used for the thumb.                                                                                                                                                                                 | string                                                                  | No       | iOS Android | yes               |
| thumbTouchSize        | The size of the touch area that allows moving the thumb. The touch area has the same center as the visible thumb. This allows to have a visually small thumb while still allowing the user to move it easily. | object                                                                  | No       | iOS Android | yes               |
| onValueChange         | Callback continuously called while the user is dragging the slider.                                                                                                                                           | function                                                                | No       | iOS Android | yes               |
| onSlidingStart        | Callback called when the user starts changing the value (e.g. when the slider is pressed).                                                                                                                    | function                                                                | No       | iOS Android | yes               |
| onSlidingComplete     | Callback called when the user finishes changing the value (e.g. when the slider is released).                                                                                                                 | function                                                                | No       | iOS Android | yes               |
| style                 | The style applied to the slider container.                                                                                                                                                                    | [style](http://facebook.github.io/react-native/docs/view.html#style)    | No       | iOS Android | yes               |
| trackStyle            | The style applied to the track.                                                                                                                                                                               | [style](http://facebook.github.io/react-native/docs/view.html#style)    | No       | iOS Android | yes               |
| thumbStyle            | The style applied to the thumb.                                                                                                                                                                               | [style](http://facebook.github.io/react-native/docs/view.html#style)    | No       | iOS Android | yes               |
| thumbImage            | Sets an image for the thumb.                                                                                                                                                                                  | [source](http://facebook.github.io/react-native/docs/image.html#source) | No       | iOS Android | yes               |
| debugTouchArea        | Set this to true to visually see the thumb touch rect in green.                                                                                                                                               | bool                                                                    | No       | iOS Android | yes               |
| animateTransitions    | Set to true if you want to use the default 'spring' animation.                                                                                                                                                | bool                                                                    | No       | iOS Android | yes               |
| animationType         | Set to 'spring' or 'timing' to use one of those two types of animations with the default [animation properties](https://facebook.github.io/react-native/docs/animations.html).                                | string                                                                  | No       | iOS Android | yes               |
| animationConfig       | Used to configure the animation parameters. These are the same parameters in the [Animated library](https://facebook.github.io/react-native/docs/animations.html).                                            | object                                                                  | No       | iOS Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jeanregisser/react-native-slider/blob/master/LICENSE).
