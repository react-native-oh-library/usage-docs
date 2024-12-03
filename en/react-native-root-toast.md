> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-root-toast</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/magicismight/react-native-root-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/magicismight/react-native-root-toast/blob/master/LICENSE.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/magicismight/react-native-root-toast)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-root-toast@3.5.1
```

#### **yarn**

```bash
yarn add react-native-root-toast@3.5.1
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React, { useState } from "react";
import { View, Button } from "react-native";
import Toast from "react-native-root-toast";

export function ReactNativeRootToastExample() {
  let PToast: any = null;
  function startPToast() {
    PToast = Toast.show("Ultra Long standby pop-up instance", {
      duration: 99999999,
      position: 20,
      shadow: true,
      animation: true,
      hideOnPress: false,
      delay: 0,
      onHidden: () => {
        PToast.destroy();
        PToast = null;
      },
    });
  }

  function hidePToast() {
    Toast.hide(PToast);
  }
  return (
    <View>
      <Button title="Open a pop-up window" onPress={startPToast} />
      <Button title="Close this pop-up window" onPress={hidePToast} />
    </View>
  );
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20-CAPI; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                                                                           | Type     | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| duration        | Toast.durations.SHORT Number The duration of the toast. (Only for api calling method) | Number   | no       | All      | yes               |
| visible         | The visibility of toast. (Only for Toast Component)                                   | Bool     | no       | All      | yes               |
| position        | The position of toast showing on screen (A negative number represents the distance from the bottom of screen. A positive number represents the distance form the top of screen.)| Number   | no       | All      | yes               |
| animation       | Should preform an animation on toast appearing or disappearing.                       | Bool     | no       | All      | yes               |
| shadow          | Should drop shadow around Toast element.                                              | Bool     | no       | All      | yes               |
| backgroundColor | The background color of the toast.                                                    | string   | no       | All      | yes               |
| shadowColor     | The shadow color of the toast.                                                        | string   | no       | All      | yes               |
| textColor       | The text color of the toast.                                                          | string   | no       | All      | yes               |
| delay           | The delay duration before toast start appearing on screen.                            | Number   | no       | All      | yes               |
| hideOnPress     | Should hide toast that appears by pressing on the toast.                              | Bool     | no       | All      | yes               |
| opacity         | The Toast opacity.                                                                    | Number   | no       | All      | yes               |
| onShow          | Callback for toast`s appear animation start                                           | function | no       | All      | yes               |
| onShown         | Callback for toast`s appear animation end                                             | function | no       | All      | yes               |
| onHide          | Callback for toast`s hide animation start                                             | function | no       | All      | yes               |
| onHidden        | Callback for toast`s hide animation end                                               | function | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/magicismight/react-native-root-toast/blob/master/LICENSE.txt).