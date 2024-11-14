> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-typography</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hectahertz/react-native-typography">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/hectahertz/react-native-typography/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/react-native-oh-library/react-native-typography)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-typography Releases](https://github.com/react-native-oh-library/react-native-typography/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-typography
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-typography
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { View, Text } from "react-native";
import React from "react";
import { iOSUIKit, material, systemWeights } from "react-native-typography";

export function TypographyExample1() {
  return (
    <View style={{ backgroundColor: "white" }}>
      <Text style={iOSUIKit.largeTitleEmphasized}>Hello iOS UI Kit!</Text>
      <Text style={material.title}>Title</Text>
      <Text style={systemWeights.light}>Title</Text>
    </View>
  );
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-typography Releases](https://github.com/react-native-oh-library/react-native-typography/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                                                                                                                                                                                                                                                                                                                                                  | Type   | Required | Platform | HarmonyOS Support |
| ------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| material            | Includes all the styles defined in the [Material Design Guidelines](https://material.io/guidelines/style/typography.html#typography-styles).Defines size, weight and color.                                                                                                                                                                                                  | object | no       | All      | yes               |
| materialDense       | material`s Dense scripts                                                                                                                                                                                                                                                                                                                                                     | object | no       | All      | yes               |
| materialTall        | material`s Tall scripts                                                                                                                                                                                                                                                                                                                                                      | object | no       | All      | yes               |
| human               | Defined in the [Human Interface Guidelines](https://developer.apple.com/ios/human-interface-guidelines/visual-design/typography/).Defines size, weight and color.                                                                                                                                                                                                            | object | no       | All      | yes               |
| humanDense          | human`s Dense scripts                                                                                                                                                                                                                                                                                                                                                        | object | no       | All      | yes               |
| humanTall           | human`s Tall scripts                                                                                                                                                                                                                                                                                                                                                         | object | no       | All      | yes               |
| iOSUIKit            | Extracted from [the official Apple sketch file](https://developer.apple.com/design/resources/) These are the text styles that fall under the category of iOS UIKit, and are used to build the UI components of iOS Apps. They build on top of the Human Interface styles, customizing some properties such as weight or letter spacing.                                      | object | no       | iOS      | yes               |
| iOSUIKitDense       | iOSUIKit`s Dense scripts                                                                                                                                                                                                                                                                                                                                                     | object | no       | iOS      | yes               |
| iOSUIKitTall        | iOSUIKit`s Tall scripts                                                                                                                                                                                                                                                                                                                                                      | object | no       | iOS      | yes               |
| systemWeights       | A font weight in React Native is sometimes formed by a pair of a fontFamily and a fontWeight, but not always! It depends on the typeface, sometimes it's just. defined by the fontFamily. With these helpers, you don't have to worry about those inconsistencies. To combine them with a collection style (or your own styles) just spread them, as they are plain objects. | object | no       | All      | yes               |
| systemDenseWeights  | systemWeights`s Dense scripts                                                                                                                                                                                                                                                                                                                                                | object | no       | All      | yes               |
| systemTallWeights   | systemWeights`s Tall scripts                                                                                                                                                                                                                                                                                                                                                 | object | no       | All      | yes               |
| sanFranciscoWeights | San Francisco typeface                                                                                                                                                                                                                                                                                                                                                       | object | no       | iOS      | yes               |
| robotoWeights       | These weights are **only intended for Android**, as they directly reference the native Roboto typeface.                                                                                                                                                                                                                                                                      | object | no       | Android  | yes               |
| webWeights          | These weights are **only intended for the web**, and render [react-native-web](https://github.com/necolas/react-native-web)'s system font stack.                                                                                                                                                                                                                             | object | no       | Web      | yes               |
| iOSColors           | Colors iOS                                                                                                                                                                                                                                                                                                                                                                   | object | no       | iOS      | yes               |
| materialColors      | Colors Material                                                                                                                                                                                                                                                                                                                                                              | object | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/hectahertz/react-native-typography/blob/master/LICENSE).
