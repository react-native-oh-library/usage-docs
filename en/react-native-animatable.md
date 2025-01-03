> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-animatable</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/oblador/react-native-animatable">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/oblador/react-native-animatable/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/oblador/react-native-animatable)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-animatable@1.4.0
```

#### **yarn**

```bash
yarn add react-native-animatable@1.4.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { useState } from "react";
import { TouchableOpacity } from "react-native";
import * as Animatable from "react-native-animatable";

export default function ExampleView() {
  const [textFontSize, setTextFontSize] = useState(10);
  return (
    <Animatable.View style={{ padding: 50, backgroundColor: "#333333" }}>
      <Animatable.Text
        animation="slideInDown"
        iterationCount={5}
        direction="reverse"
        style={{ color: "white", textAlign: "center" }}
        duration={2000}
        onAnimationBegin={() => {
          console.log("test onAnimationBegin");
        }}
        onAnimationEnd={() => {
          console.log("test onAnimationEnd");
        }}
      >
        Up and down you go
      </Animatable.Text>
      <Animatable.Text
        animation="bounce"
        easing="ease-out"
        iterationCount="infinite"
        iterationDelay={1500}
        style={{ textAlign: "center" }}
        useNativeDriver={true}
        isInteraction={true}
      >
        ❤️
      </Animatable.Text>
      <Animatable.Text
        animation="fadeIn"
        delay={2000}
        style={{ textAlign: "center", marginTop: 50, color: "white" }}
      >
        (*^▽^*)
      </Animatable.Text>
      <TouchableOpacity onPress={() => setTextFontSize(textFontSize + 5)}>
        <Animatable.Text
          transition="fontSize"
          style={{
            textAlign: "center",
            marginTop: 50,
            color: "white",
            fontSize: textFontSize || 10,
          }}
          onTransitionBegin={() => {
            console.log("test onTransitionBegin");
          }}
          onTransitionEnd={() => {
            console.log("test onTransitionEnd");
          }}
        >
          O(∩_∩)O
        </Animatable.Text>
      </TouchableOpacity>
    </Animatable.View>
  );
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 2.0.0.18;
2. RNOH: 0.72.33; SDK: OpenHarmony 5.0.0.71 (API Version 12 Release); IDE: DevEco Studio 5.0.3.900; ROM: NEXT.0.0.71;

## Properties

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name              | Description                                                  | Type                   | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------ | ---------------------- | -------- | -------- | ----------------- |
| animation         | Animation name. For details, see the following available animations.                            | string/undefined       | /        | all      | yes               |
| duration          | Animation duration, in milliseconds.                                    | number/undefined       | /        | all      | yes               |
| delay             | (Optional) Animation delay, in milliseconds.                                    | number/undefined       | /        | all      | yes               |
| direction         | Animation direction, particularly suitable for animation repeating. Valid values are **normal**, **reverse**, **alternate**, and **alternate-reverse**.| string/undefined       | /        | all      | yes               |
| easing            | Easing function. Valid values are **custom**, **linear**, **ease-in**, **ease-out**, and **ease-in-out**.  | string/undefined       | /        | all      | yes               |
| iterationCount    | Number of times an animation should be played. Set it to **infinite** for animations to be looped.                    | number/undefined       | /        | all      | yes               |
| iterationDelay    | Time between animation iterations, in milliseconds.                          | number/undefined       | /        | all      | yes               |
| transition        | Style property to be converted, such as opacity, rotation, or font size. Use an array if there are multiple properties to be converted.| string/array/undefined | /        | all      | yes               |
| onAnimationBegin  | Function called when the animation is started.                                      | Function/undefined     | /        | all      | yes               |
| onAnimationEnd    | Function called when the animation is successfully completed or canceled. The function is called with the **endState** parameter. Check **endState.finished** to see if the animation is complete.| Function/undefined     | /        | all      | yes               |
| onTransitionBegin | Function called when the style conversion starts. Use property parameters to call functions to distinguish styles.| Function/undefined     | /        | all      | yes               |
| onTransitionEnd   | Function called when the style conversion is successfully completed or canceled. Use property parameters to call functions to distinguish styles.| Function/undefined     | /        | all      | yes               |
| useNativeDriver   | Whether to use the native or JavaScript animation driver. The native driver can help improve performance, but cannot handle all types of styles.| Function/undefined     | /        | all      | yes               |
| isInteraction     | Whether the animation creates an interaction handle on the interaction manager.                  | Boolean                | /        | all      | yes               |

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/oblador/react-native-animatable/blob/master/LICENSE).
