> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-segmented-control/segmented-control</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-segmented-control/segmented-control">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-segmented-control/segmented-control/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/segmented-control)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/segmented-control Releases](https://github.com/react-native-oh-library/segmented-control/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/segmented-control
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/segmented-control
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from "react";
import SegmentedControl from "@react-native-segmented-control/segmented-control";

const CustomValues = ["One", "Two"];

export const MSegmentedControl: React.FC = (): JSX.Element => {

    const [selectedIndex, setSelectedIndex] = useState(0);

    return <SegmentedControl
        values={["One", "Two"]}
        selectedIndex={selectedIndex}
        onChange={(event) => {
            setSelectedIndex(event.nativeEvent.selectedSegmentIndex);
        }}
    />;
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;
3. RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1) ; IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;
4. RNOH：0.72.29; SDK：HarmonyOS NEXT Developer Beta6 5.0.0.61; IDE：DevEco Studio 5.0.3.706; ROM：3.0.0.61;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

详情见 [react-native-community/segmented-control 源库地址](https://github.com/react-native-segmented-control/segmented-control)

| Name                      | Description                                                                                    | Type                                                                                                                                                             | Required | Platform | HarmonyOS Support |
| ------------------------- | ---------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| enabled         | If false the user won't be able to interact with the control. Default value is true.                                                                                                                                                             | boolean         | No       | All          | Yes               |
| momentary       | If true, then selecting a segment won't persist visually. The onValueChange callback will still work as expected.                                                                                                                                | boolean         | No       | iOS          | Yes               | 
| onChange        | Callback that is called when the user taps a segment; passes the event as an argument                                                                                                                                                            | function        | No       | All          | Yes               |
| onValueChange   | Callback that is called when the user taps a segment; passes the segment's value as an argument                                                                                                                                                  | function        | No       | All          | Yes               |
| selectedIndex   | The index in props.values of the segment to be (pre)selected.                                                                                                                                                                                    | number          | No       | All          | Yes               |
| tintColor       | Accent color of the control.                                                                                                                                                                                                                     | string          | No       | All          | Yes               |
| backgroundColor | Background color color of the control.                                                                                                                                                                                                           | string          | No       | All          | Yes               |
| values          | The labels for the control's segment buttons, in order.                                                                                                                                                                                          | string          | Yes      | All          | Yes               |
| appearance      | Overrides the control's appearance irrespective of the OS theme                                                                                                                                                                                  | 'dark', 'light' | No       | All          | Yes               |
| fontStyle       | An object container,color: color of segment;fontSize: font-size of segment text;fontFamily: font-family of segment text;fontWeight: font-weight of segment text                                                                                  | object          | No       | All          | Yes               | 
| activeFontStyle | An object container,color: overrides color of selected segment text;fontSize: overrides font-size of selected segment text;fontFamily: overrides font-family of selected segment text;fontWeight: overrides font-weight of selected segment text | object          | No       | All          | Yes               | 
| tabStyle        | Styles the clickable surface which is responsible to change tabs                                                                                                                                                                                 | object          | No       | Android, Web | Yes               |

## Known Issues

- [X] @react-native-segmented-control/segmented-control 的fontFamily属性未实现 HarmonyOS 化: [issue#858](https://github.com/react-native-segmented-control/segmented-control/issues/858)
- [X] @react-native-segmented-control/segmented-control 的momentary属性未实现 HarmonyOS 化: [issue#868](https://github.com/react-native-segmented-control/segmented-control/issues/868)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-segmented-control/segmented-control/blob/master/LICENSE).
