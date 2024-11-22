> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-walkthrough-tooltip</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jasongaare/react-native-walkthrough-tooltip">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jasongaare/react-native-walkthrough-tooltip/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/jasongaare/react-native-walkthrough-tooltip)

## Installation and Usage

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install react-native-walkthrough-tooltip@1.6.0
```

#### **yarn**

```bash
yarn add react-native-walkthrough-tooltip@1.6.0
```

The following code shows the basic use scenario of the repository:

```js
import React, { useState } from "react";
import { View, Text, } from "react-native";
import Tooltip from 'react-native-walkthrough-tooltip';

export const TestTooltip = ({ text, style }) => {
  const [toolTipVisible, setToolTipVisible] = useState(false);

  return (
   <Tooltip
   isVisible={toolTipVisible}
   content={<Text>Check this out!</Text>}
   placement="top"
   onClose={() => setToolTipVisible(false)}
    >
  <TouchableHighlight onPress={() => setToolTipVisible(!toolTipVisible)}>
    <Text>Press me</Text>
  </TouchableHighlight>
</Tooltip>
};
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.5; SDK: HarmonyOS-NEXT-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.403; ROM: 3.0.0.25;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

### Properties

[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.。

[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                      | Description                                                                                                                                                                                                                                                                                                                        | Type             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| accessible                | Set this to false if you do not want the root touchable element to be accessible. [See docs on accessible here](https://reactnative.dev/docs/accessibility#accessibility-properties)                                                                                                                                               | bool             | No       | All      | No               |
| allowChildInteraction     | By default, the user can touch and interact with the child element. When this prop is false, the user cannot interact with the child element while the tooltip is visible.                                                                                                                                                         | bool             | No       | All      | Yes               |
| arrowSize                 | The dimensions of the arrow on the bubble pointing to the highlighted element                                                                                                                                                                                                                                                      | Size             | No       | All      | Yes               |
| backgroundColor           | Color of the fullscreen background beneath the tooltip. Overrides the backgroundStyle prop                                                                                                                                                                                                                                         | string           | No       | All      | Yes               |
| childContentSpacing       | The distance between the tooltip-rendered child and the arrow pointing to it                                                                                                                                                                                                                                                       | number           | No       | All      | Yes               |
| closeOnChildInteraction   | When child interaction is allowed, this prop determines if onClose should be called when the user interacts with the child element. Default is true (usually means the tooltip will dismiss once the user touches the element highlighted)                                                                                         | bool             | No       | All      | Yes               |
| closeOnContentInteraction | this prop determines if onClose should be called when the user interacts with the content element. Default is true (usually means the tooltip will dismiss once the user touches the content element)                                                                                                                              | bool             | No       | All      | Yes               |
| content                   | This is the view displayed in the tooltip popover bubble                                                                                                                                                                                                                                                                           | function/Element | Yes      | All      | Yes               |
| displayInsets             | The number of pixels to inset the tooltip on the screen (think of it like padding). The tooltip bubble should never render outside of these insets, so you may need to adjust your content accordingly                                                                                                                             | object           | No       | All      | Yes               |
| disableShadow             | When true, tooltips will not appear elevated. Disabling shadows will remove the warning: RCTView has a shadow set but cannot calculate shadow efficiently on IOS devices.                                                                                                                                                          | bool             | No       | All      | Yes               |
| isVisible                 | When true, tooltip is displayed                                                                                                                                                                                                                                                                                                    | bool             | Yes      | All      | Yes               |
| onClose                   | Callback fired when the user taps the tooltip background overlay                                                                                                                                                                                                                                                                   | function         | Yes      | All      | Yes               |
| placement                 | Where to position the tooltip - options: top, bottom, left, right, center. Default is top for tooltips rendered with children Default is center for tooltips rendered without children.NOTE: center is only available with a childless placement, and the content will be centered within the bounds defined by the displayInsets. | string           | Yes      | All      | Yes               |
| showChildInTooltip        | Set this to false if you do NOT want to display the child alongside the tooltip when the tooltip is visible                                                                                                                                                                                                                        | bool             | No       | All      | Yes               |
| supportedOrientations     | This prop allows you to control the supported orientations the tooltip modal can be displayed. It correlates directly with [the prop for React Native's Modal component](https://reactnative.dev/docs/modal#supportedorientations) (has no effect if useReactNativeModal is false)                                                 | bool             | No       | iOS      | No                |
| topAdjustment             | Value which provides additional vertical offest for the child element displayed in a tooltip. Commonly set to: Platform.OS === 'android' ? -StatusBar.currentHeight : 0 due to an issue with React Native's measure function on Android                                                                                            | number           | No       | All      | Yes               |
| horizontalAdjustment      | Value which provides additional horizontal offest for the child element displayed in a tooltip. This is useful for adjusting the horizontal positioning of a highlighted child element if needed                                                                                                                                   | number           | No       | All      | Yes               |
| useInteractionManager     | Set this to true if you want the tooltip to wait to become visible until the callback for InteractionManager.runAfterInteractions is executed. Can be useful if you need to wait for navigation transitions to complete, etc.[ See docs on InteractionManager here](https://reactnative.dev/docs/interactionmanager)               | bool             | No       | All      | Yes               |
| useReactNativeModal       | By default, this library uses a <Modal> component from React Native. If you need to disable this, and simply render an absolutely positioned full-screen view, set useReactNativeModal={false}. This is especially useful if you desire to render a Tooltip while you have a different Modal rendered.                             | bool             | No       | All      | Yes               |

## Known Issues

- [ ] supportedOrientations 在 HarmonyOS 不支持
- [ ] accessible 在 HarmonyOS 不支持
## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/jasongaare/react-native-walkthrough-tooltip/blob/master/LICENSE).
