> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-vector-drawable</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/klarna-incubator/react-native-vector-drawable">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/klarna-incubator/react-native-vector-drawable/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-vector-drawable)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-library/react-native-vector-drawable Releases](https://github.com/react-native-oh-library/react-native-vector-drawable/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-vector-drawable
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-vector-drawable
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```tsx

import React from "react";
import { View } from 'react-native';
import VectorDrawable from "react-native-vector-drawable";
export default function VectorDrawableDemo(): JSX.Element {
    return <View>
            <VectorDrawable
               resourceName="ic_drawable_name"
               style={{ width: 50, height: 50, tintColor: 'blue' }}
            />
    </View>
}
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-vector-drawable Releases](https://github.com/react-native-oh-library/react-native-vector-drawable/releases)


## Properties
In the original library, the Android platform implements the loading of[xml vector images](https://github.com/klarna-incubator/react-native-vector-drawable/blob/master/example/android/app/src/main/res/drawable/ic_klarna_logo.xml) through the android.graphics.drawable.Drawable method，On the iOS platform,it is achieved through the[React-Native View](https://reactnative.cn/docs/view)HarmonyOS aligns with iOS in this regard, and the properties are the same as those described in the[React-Native View](https://reactnative.cn/docs/view)

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| resourceName    | Name of the Android vector drawable resource. | string | true       | Android | No           |
| style    | See Style props. Note: border props are not supported. | object | false       | Android | No               |

style Props
| Name           | Description                   | Type | Required |Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | -------- | ----------------- |
| resizeMode    | 	Determines how to resize the image when the frame doesn't match the raw image dimensions. Possible values are cover, contain, stretch and center | string | false | Android | No        |
| tintColor    | Changes the color of all the non-transparent pixels to the tintColor. | string | false | Android | No   |
## Others

## License

This project is licensed under [The Apache License (Apache)](https://github.com/klarna-incubator/react-native-vector-drawable/blob/master/LICENSE).
