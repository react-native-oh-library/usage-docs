> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient-text </code> </h1>
</p>
<p align="center">
    <a href="https://github.com/HMDarkFir3/react-native-linear-gradient-text">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/HMDarkFir3/react-native-linear-gradient-text/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/HMDarkFir3/react-native-linear-gradient-text)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install react-native-linear-gradient-text@1.2.8
```

#### yarn

```bash
yarn add react-native-linear-gradient-text@1.2.8
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React from "react";
import { View, StyleSheet } from "react-native";
import { LinearGradientText } from "react-native-linear-gradient-text";

export const App = () => {
  return (
    <View style={styles.container}>
      <LinearGradientText
        colors={["#E76F00", "#EA374E"]}
        text="Hello World"
        start={{ x: 0.5, y: 0 }} // Optional
        end={{ x: 1, y: 1 }} // Optional
        textStyle={{ fontSize: 40 }} // Optional
        textProps={{ allowFontScaling: true }} // Optional
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    alignItems: "center",
    justifyContent: "center",
  },
});
```
## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/masked-view and @react-native-oh-tpl/react-native-linear-gradient. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/masked-view and @react-native-oh-tpl/react-native-linear-gradient to add it to your project.


## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.21;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-linear-gradient-text ReadMe](https://github.com/HMDarkFir3/react-native-linear-gradient-text/tree/main)

### Props:

| Name      | Description                                                                                                   | **Type**                                                         | Platform | Required | HarmonyOS Support |
| --------- | ------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | -------- | -------- | ----------------- |
| text      | An string that display text. Example: `text="Hello World"`                                                    | string                                                           | All      | Y        | Yes               |
| colors    | An array of at least two color values that represent gradient colors. Example: `colors={["black", "white"]}`. | string[]                                                         | All      | Y        | Yes               |
| start     | An optional prop. He declare the position that the gradient starts. Example `start={{ x: 0.5, y: 0 }}`.       | { x: number, y: number }                                         | All      | N        | Yes               |
| end       | Same as start, but for the of the gradient.                                                                   | { x: number, y: number }                                         | All      | N        | Yes               |
| textStyle | A property to change all styles that a text has.                                                              | [TextStyle](https://reactnative.dev/docs/text-style-props)       | All      | N        | Yes               |
| textProps | A property to apply native props to text.                                                                     | [TextProps](https://reactnative.dev/docs/text-style-props#props) | All      | N        | Yes               |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/HMDarkFir3/react-native-linear-gradient-text/blob/main/LICENSE).
