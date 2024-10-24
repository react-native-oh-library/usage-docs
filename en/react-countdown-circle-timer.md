> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-countdown-circle-timer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vydimitrov/react-countdown-circle-timer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vydimitrov/react-countdown-circle-timer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/vydimitrov/react-countdown-circle-timer)

## Installation and Usage

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-countdown-circle-timer@3.2.1
```

#### **yarn**

```bash
yarn add react-native-countdown-circle-timer@3.2.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { View, StyleSheet, Button, Text, ScrollView } from "react-native";
import { CountdownCircleTimer } from "react-native-countdown-circle-timer";

export function SwitchDemo() {
  const [isPlaying, setIsPlaying] = useState(true);
  const [count, setCount] = useState(15);

  return (
    <View style={styles.container}>
      <CountdownCircleTimer
        isPlaying={isPlaying}
        duration={count}
        initialRemainingTime={6}
        isSmoothColorTransition={false}
        colors="#aabbcc"
        onUpdate={(remainingTime) => {
          console.log("Counter is ", count);
          console.log("Remaining time is ", remainingTime);
        }}
        onComplete={() => ({ shouldRepeat: true })}
      >
        {({ remainingTime }) => remainingTime}
      </CountdownCircleTimer>
      <Button
        onPress={() => setIsPlaying((prev) => !prev)}
        title={"Toggle Playing"}
      ></Button>
      <Button
        onPress={() => setCount((prev) => (prev += 5))}
        title={"Count"}
      ></Button>
    </View>
  );
}
const styles = StyleSheet.create({
  container: {
    alignItems: "center",
    justifyContent: "center",
    backgroundColor: "#fff",
  },
});
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-svg](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-svg-capi.md#link) to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                                                                                         Description                                                                                         |              Type               | Required |  Platform   | HarmonyOS Support |
| :---------------------: | :-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------: | :-----------------------------: | :------: | :---------: | :---------------: |
|         colors          |                      colors prop is either:(Single valid color in any format or URL to a gradient;Array of colors in HEX format. At least 2 colors should be provided)                      |       `string & string[]`       |    No    | Android/iOS |        Yes        |
|       colorsTime        | Indicates the time when a color should switch to the next color. The first number is the countdown duration and the last one is 0 or goal. Works only when colors is an array of HEX colors |            number[]             |    No    | Android/iOS |        Yes        |
|        isPlaying        |                                                                                   Play or pause animation                                                                                   |             boolean             |    No    | Android/iOS |        Yes        |
|  initialRemainingTime   |                                                             Set the initial remaining time if it is different than the duration                                                             |             number              |    No    | Android/iOS |        Yes        |
|     updateInterval      |                                  Update interval in seconds. Determines how often the timer updates. When set to 0 the value will update on each key frame                                  |             number              |    No    | Android/iOS |        Yes        |
|          size           |                                                                             Width and height of the SVG element                                                                             |             number              |    No    | Android/iOS |        Yes        |
|       strokeWidth       |                                                                                      Path stroke width                                                                                      |             number              |    No    | Android/iOS |        Yes        |
|    trailStrokeWidth     |                                                                                     Trail stroke width                                                                                      |             number              |    No    | Android/iOS |        Yes        |
|      strokeLinecap      |                                                                                    Path stroke line cap                                                                                     |    `round 、 square 、 butt`    |    No    | Android/iOS |        Yes        |
|        rotation         |                                                                              Progress path rotation direction                                                                               | `clockwise 、 counterclockwise` |    No    | Android/iOS |        Yes        |
|        isGrowing        |                                                            Indicated if the progress path should be growing instead of shrinking                                                            |             boolean             |    No    | Android/iOS |        Yes        |
|       trailColor        |                                                                      Circle trail color - takes any valid color format                                                                      |             string              |    No    | Android/iOS |        Yes        |
| isSmoothColorTransition |                                                            Indicates if the colors should smoothly transition to the next color                                                             |             boolean             |    No    | Android/iOS |        Yes        |
|        children         |                                                          Render function to customize the time/content in the center of the circle                                                          |            function             |    No    | Android/iOS |        Yes        |
|       onComplete        |                                                                             On animation complete event handler                                                                             |            function             |    No    | Android/iOS |        Yes        |
|        onUpdate         |                                                                           On remaining time update event handler                                                                            |            function             |    No    | Android/iOS |        Yes        |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vydimitrov/react-countdown-circle-timer/blob/master/LICENSE).
