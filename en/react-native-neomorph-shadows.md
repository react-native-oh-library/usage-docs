> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-neomorph-shadows</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tokkozhin/react-native-neomorph-shadows">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/tokkozhin/react-native-neomorph-shadows/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-neomorph-shadows)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-neomorph-shadows Releases](https://github.com/react-native-oh-library/react-native-neomorph-shadows/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-neomorph-shadows
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-neomorph-shadows
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```tsx
import React from 'react';
import { View, StyleSheet, Text } from 'react-native';
import { Shadow } from 'react-native-neomorph-shadows';

export default function () {
    return (
        <View style={styles.container}>
            <Shadow
                style={{
                    // shadowOffset: { width: 0, height: 5 },
                    fillOpacity: 0.6,
                    // borderRadius: 25,
                    stopColor:"#f0f0f0",
                    startColor:"#FF3A3A",
                    width: 110,
                    height: 110,
                    alignItems: "center",
                    justifyContent: "center"
                }}>
                <View
                    style={{
                        borderRadius: 25,
                        backgroundColor: "#FF3A3A",
                        width: 110,
                        height: 44,
                        alignItems: "center",
                        justifyContent: "center",
                        // shadowColor: "#FFC0C0",
                        // shadowOffset: {
                        //     width: 0,
                        //     height: 20
                        // },
                        // shadowOpacity: 1,
                        // shadowRadius: 3.84,
                        // elevation: 5 
                    }}>
                    <Text
                        style={{
                            color: "#ffffff",
                            fontWeight: "bold",
                            textAlign: "center",
                            fontSize: 16
                        }}>
                        Login/Register
                    </Text>
                </View>
            </Shadow>
        </View>
    );
};

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
        alignItems: 'center',
        backgroundColor: '#f0f0f0',
    },
});


```
## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-svg. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

If it is not included, follow the guide provided in @react-native-oh-tpl/react-native-svg to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-neomorph-shadows Releases](https://github.com/react-native-oh-library/react-native-neomorph-shadows/releases)

## Properties

### This component has the following properties:
## **API（Shadow）**
>[!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **style**      |       Style object        |                         Object                           |    No    | iOS/Android |        Yes        |
|        **fillOpacity**        |                   shadow transparency                    |                         String                           |    YES   | iOS/Android |        Yes        |
|     **stopColor**      |                  Shadow Gradient End Color              |                         String                           |    No    | iOS/Android |        Yes        |
| **startColor**  |       Shadow Gradient Start Color       |                         String                           |    No    | iOS/Android |        Yes        |


## Known Issues

Currently, only the shadow effect for the Shadow component is designed. The Neomorph component is not yet involved.[issue#5](https://github.com/react-native-oh-library/react-native-neomorph-shadows/issues/5)

## Others

## License

This project is licensed under [MIT License](https://github.com/tokkozhin/react-native-neomorph-shadows/blob/master/LICENSE). 