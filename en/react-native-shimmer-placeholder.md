> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-shimmer-placeholder</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tomzaku/react-native-shimmer-placeholder">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tomzaku/react-native-shimmer-placeholder/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/tomzaku/react-native-shimmer-placeholder)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-shimmer-placeholder@2.0.9
```

#### **yarn**

```bash
yarn add react-native-shimmer-placeholder@2.0.9
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import { View, Image } from "react-native";
import { createShimmerPlaceholder } from "react-native-shimmer-placeholder";
import LinearGradient from "react-native-linear-gradient";

const ShimmerPlaceholder = createShimmerPlaceholder(LinearGradient);
export class ShimmerPlaceholderTest extends Component {
  constructor(props) {
    super(props);
    this.state = {
      visible: false,
    };
  }
  render() {
    return (
      <View>
        <ShimmerPlaceholder
          width={150}
          height={150}
          shimmerStyle={{ borderRadius: 100 }}
          visible={this.state.visible}
        >
          <Image
            style={{ width: 150, height: 150, borderRadius: 100 }}
            source={{ uri: "https://unsplash.it/150/150" }}
            onLoadEnd={() => {
              this.setState({ visible: true });
            }}
          />
        </ShimmerPlaceholder>
      </View>
    );
  }
}
```

## Link

> [!TIP] The version of @react-native-oh-tpl/react-native-linear-gradient that this library depends on is 3.0.0-0.4.5.

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-linear-gradient. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-linear-gradient to add it to your project.

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                                                            | Required | Type      | Platform | HarmonyOS Support |
| -------------------------- | ------------------------------------------------------------------------------------------------------ | -------- | --------- | -------- | ----------------- |
| **LinearGradient**         | Linear Gradient components ('react-native-linear-gradient' or 'expo-linear-gradient')                  | no       | Component | ALL      | yes               |
| **visible**                | Visible child components                                                                               | no       | boolean   | ALL      | yes               |
| **style**                  | Container Style                                                                                        | no       | Style     | ALL      | yes               |
| **shimmerStyle**           | Shimmer Style only                                                                                     | no       | Style     | ALL      | yes               |
| **contentStyle**           | Content Style when visible                                                                             | no       | Style     | ALL      | yes               |
| **location**               | Locations of shimmer                                                                                   | no       | number[]  | ALL      | yes               |
| **width**                  | Width of row                                                                                           | no       | number    | ALL      | yes               |
| **duration**               | Duration of shimmer over a row                                                                         | no       | number    | ALL      | yes               |
| **height**                 | Height of row                                                                                          | no       | number    | ALL      | yes               |
| **shimmerWidthPercent**    | Percent of shimmer width                                                                               | no       | number    | ALL      | yes               |
| **isReversed**             | Reverse direction of animation                                                                         | no       | boolean   | ALL      | yes               |
| **stopAutoRun**            | Stop running shimmer animation at beginning                                                            | no       | boolean   | ALL      | yes               |
| **isInteraction**          | Defines whether or not the shimmer animation creates an interaction handle on the `InteractionManager` | no       | boolean   | ALL      | yes               |
| **shimmerColors**          | Colors of the shimmer.                                                                                 | no       | string[]  | ALL      | yes               |
| **containerProps**         | Props passed to the outermost View                                                                     | no       | ViewProps | ALL      | yes               |
| **shimmerContainerProps**  | Props passed to the View which contains the loading animation                                          | no       | ViewProps | ALL      | yes               |
| **childrenContainerProps** | Props passed to the View which contains the children                                                   | no       | ViewProps | ALL      | yes               |

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Method          | Description                 | Type     | **Required** | Platform | HarmonyOS Support |
| --------------- | --------------------------- | -------- | ------------ | -------- | ----------------- |
| **getAnimated** | get Animated of Placeholder | Animated | no           | ALL      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/tomzaku/react-native-shimmer-placeholder/blob/master/LICENSE).
