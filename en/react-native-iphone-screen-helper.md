Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-iphone-screen-helper</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/chlee1001/react-native-iphone-screen-helper">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/chlee1001/react-native-iphone-screen-helper/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-iphone-screen-helper)


## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-iphone-screen-helper Releases](https://github.com/react-native-oh-library/react-native-iphone-screen-helper/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-iphone-screen-helper
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-iphone-screen-helper
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from 'react';
import { getStatusBarHeight } from 'react-native-iphone-screen-helper'
import { View } from 'react-native';

const ScreenHelperDemo: React.FC = (): JSX.Element => {
    const [currentHeight, setCurrentHeight] = useState<number>(0)

    useEffect(() => {
        const barHeight = getStatusBarHeight()
        setCurrentHeight(barHeight)
    }, [])

    return (
        <>
            <View style={{ height: currentHeight, borderBottomWidth: 1 }} />
        </>
    )
}

export default ScreenHelperDemo;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-iphone-screen-helper Releases](https://github.com/react-native-oh-library/react-native-iphone-screen-helper/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| :---  | :---------- | ---- | -------- | ---- | ------------ |
| isIphoneX         | **returns** - `true` if you're running on an iPhone X or a newer model with a notch or dynamic island. | boolean | No       | All      | Yes               |
| isDynamicIsland | **returns** - `true` if you're running on an iPhone X or dynamic island. | boolean | No       | All      | Yes               |
| ifIphoneX | This method is for creating stylesheets with the iPhone X and later models, including those with dynamic islands, in mind. | stylesheets | No       | All      | Yes               |
| getStatusBarHeight | **returns** - the height of the status bar | number | No | All | Yes |
| getBottomSpace | **returns** - the height of the bottom to fit the safe area: `34` for iPhone X and newer models with a notch or dynamic island, and `0` for other devices. | number | No | All | Yes |


## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/chlee1001/react-native-iphone-screen-helper/blob/master/LICENSE).