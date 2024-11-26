> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-community-hooks</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-community/hooks">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-community/hooks/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-community/hooks)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-community/hooks@3.0.0
```

#### yarn

```bash
yarn add @react-native-community/hooks@3.0.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```jsx

import React, { useState } from 'react';
import {
    Text,
    View,
    ScrollView,
    StyleSheet,
    RefreshControl
} from 'react-native';

import {  useAppState, useLayout, useKeyboard, useDeviceOrientation, useRefresh, useInteractionManager } from '@react-native-community/hooks'
export const HooksUnTester = () => {
    const [backText, setBackText] = useState('')
    const [refreshText, setRefreshText] = useState('Pull down refresh')
    const fetch = () => {
        return new Promise((resolve) => setTimeout(() => { resolve(setRefreshText('Refresh successful')) }, 500))
    }
    const { isRefreshing, onRefresh } = useRefresh(fetch);
    return (
        <View style={{ flex: 1 }}>
            <ScrollView refreshControl={
                <RefreshControl
                    refreshing={isRefreshing}
                    onRefresh={onRefresh}
                />
            }>
                {/* hooks-useRefresh-demo */}
                <View style={styles.testSuite}>
                    <Text style={styles.titles}>useRefresh</Text>
                    <View style={styles.textCase}>
                        <Text> {refreshText} </Text>
                    </View>
                </View>
                {/* hooks-useDeviceOrientation-demo */}
                <View style={styles.testSuite}>
                    <Text style={styles.titles}>useDeviceOrientation</Text>
                    <View style={styles.textCase}>
                        <Text>Determine whether it is landscape or portrait:{useDeviceOrientation()} </Text>
                    </View>
                </View>
            </ScrollView>
        </View>
    );
}
const styles = StyleSheet.create({
    useBackHandlerBtn: {
        borderRadius: 6,
        height: 36,
        display: 'flex',
        justifyContent: 'center',
        alignItems: 'center',
        margin: 10,
        backgroundColor: 'rgb(61, 176, 236)',
    },
    TextInput: {
        height: 40,
        borderColor: '#fff',
        borderWidth: 1,
        borderRadius: 4,
        width: '90%',
        backgroundColor: '#fff'
    },
    testSuite: { backgroundColor: "#fff", margin: 10 },
    titles: {
        marginLeft: 6,
        fontWeight: '600'
    },
    textCase: {
        margin: 5,
    },
    btnText: { fontWeight: 'bold', color: '#fff', fontSize: 20 },
    container: { flex: 1 },
    ball: {
        width: 100,
        height: 100,
        backgroundColor: "salmon",
        borderRadius: 100,
    },
});


```

## Constraints

### Compatibility

This document is verified based on the following versions:

1.RNOH: 0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.25; IDE：DevEco Studio 5.0.3.400SP7; ROM：3.0.0.25;
2.RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.


| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| useAccessibilityInfo    | Check whether some configurations of the device are enabled.See useAccessibilityInfo Api | Function | False       | Android / iOS | Yes           |
| useAppState    | Tells you whether the application is in the foreground or background | Function | False       | Android / iOS | Yes           |
| useBackHandler  | Used to listen for the back button event on the device. You can call your own function to handle the back behavior. | Function | False       | Android / iOS | Yes               |
| useImageDimensions  | Used to listen for the back button event on the device. You can call your own function to handle the back behavior. | Function | False       | Android / iOS | Yes     |
| useKeyboard  | Return whether the keyboard is invoked and the keyboard width and height. | Function | False       | Android / iOS | Yes       |
| useInteractionManager  | Schedule some of the more time-consuming tasks for after all the interactions or animations have been completed. | Function | False       | Android / iOS | Yes       |
| useDeviceOrientation  | Check whether the device is in landscape or portrait mode. | Function | False       | Android / iOS | Yes       |
| useLayout  | Returns the x-axis and y-axis coordinates of an element and the width and height of the element. | Function | False       | Android / iOS | Yes       |
| useRefresh  | pull down to refresh. | Function | False       | Android / iOS | Yes       |

useAccessibilityInfo 方法返回值
| Name           | Description                   | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -------- | ----------------- |
| isBoldTextEnabled  | whether bold text is enabled | iOS | Yes        |
| isScreenReaderEnabled    | Whether the Screen Reading Function Is Enabled | Android / iOS | Yes   |
| isGrayscaleEnabled  | Whether grayscale mode is enabled | iOS | Yes        |
| isInvertColorsEnabled  | Whether color inversion is enabled | iOS | Yes        |
| isReduceMotionEnabled  | Whether reduction animation is enabled | Android / iOS | Yes        |
| isReduceTransparencyEnabled  | Whether reduce transparency is enabled | iOS | Yes        |

## Known Issues

## Others

## License

This project is licensed under [The ISC License (ISC)](https://github.com/react-native-community/hooks/blob/main/LICENSE).
