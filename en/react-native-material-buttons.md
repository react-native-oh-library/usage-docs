> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-material-buttons</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/n4kz/react-native-material-buttons">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/n4kz/react-native-material-buttons/blob/master/license.txt">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-material-buttons)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-material-buttons Releases](https://github.com/react-native-oh-library/react-native-material-buttons/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-material-buttons
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-material-buttons
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```tsx
import React, { Component } from 'react';
import { AppRegistry, Text, ScrollView, View, SafeAreaView } from 'react-native';
import { TextButton, RaisedTextButton } from 'react-native-material-buttons';

interface Styles {
  scroll: object;
  container: object;
  safeContainer: object;
  column: object;
  row: object;
  card: object;
  button: object;
  display: object;
  text: object;
  content: object;
  bold: object;
}

let styles: Styles = {
  scroll: {
    padding: 4,
    paddingTop: 24,
    backgroundColor: '#E8EAF6',
  },
  container: {
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 8,
    backgroundColor: 'rgba(0,0,0,.05)',
  },
  safeContainer: {
    flex: 1,
    backgroundColor: '#E8EAF6',
  },
  column: {
    justifyContent: 'center',
    marginBottom: 8,
    backgroundColor: 'rgba(0,0,0,.05)',
  },
  row: {
    marginBottom: 8,
  },
  card: {
    borderRadius: 2,
    padding: 8,
    margin: 4,
    backgroundColor: 'rgba(255, 255, 255, 1)',
    minHeight: 76,
    justifyContent: 'space-between',
    shadowOpacity: 0.54,
    shadowRadius: 1,
    shadowOffset: { width: 0, height: 1 },
    elevation: 1,
  },
  button: {
    margin: 4,
  },
  display: {
    paddingHorizontal: 8,
    fontSize: 17,
    fontWeight: '500',
    color: 'rgba(0, 0, 0, .87)',
  },
  text: {
    padding: 8,
    fontSize: 15,
    color: 'rgba(0, 0, 0, .54)',
  },
  content: {
    flex: 1,
    paddingVertical: 16,
  },
  bold: {
    fontWeight: 'bold',
  },
};

/* eslint-disable react/prop-types */
let Strong: React.FC<{ children: React.ReactNode }> = ({ children, ...props }) => (
  <Text style={styles.bold} {...props}>
    {children}
  </Text>
);
/* eslint-enable */

const  MaterialButtons = () => {
      return (
        <SafeAreaView style={styles.safeContainer}>
          <ScrollView style={styles.scroll}>
            <View style={styles.card}>
              <View style={styles.content}>
                <Text style={styles.display}>default</Text>
                <Text style={styles.text}>
                  Buttons with default props, raised or flat, enabled or <Strong>disabled</Strong>
                </Text>
              </View>
              <RaisedTextButton style={{ marginVertical: 4 }} title="default button" />
              <RaisedTextButton style={{ marginVertical: 4 }} titleStyle={{ fontWeight: 'bold' }} title="disabled button" disabled />
              <TextButton style={{ marginVertical: 4 }} title="default flat button" />
              <TextButton style={{ marginVertical: 4 }}  disabledTitleColor="red" title="disabled flat button" disabled />
            </View>

            <View style={styles.card}>
              <View style={styles.content}>
                <Text style={styles.display}>raised</Text>
                <Text style={styles.text}>
                  Buttons with custom <Strong>color</Strong>, <Strong>titleColor</Strong>, increased{' '}
                  <Strong>rippleDuration</Strong> and <Strong>rippleOpacity</Strong>
                </Text>
              </View>
              <View style={{ flexDirection: 'row', justifyContent: 'flex-end' }}>
                <RaisedTextButton
                  style={styles.button}
                  rippleDuration={600}
                  rippleOpacity={0.54}
                  title="flat"
                  color="#039BE5"
                  titleColor="white"
                />
                <RaisedTextButton
                  style={styles.button}
                  rippleDuration={1000}
                  rippleOpacity={0.64}
                  title="is"
                  color="#0288D1"
                  titleColor="white"
                />
                <RaisedTextButton
                  style={styles.button}
                  titleStyle={{ fontWeight: 'bold' }}
                  rippleDuration={1500}
                  rippleOpacity={0.74}
                  title="boring"
                  color="#0277BD"
                  titleColor="white"
                />
              </View>
            </View>

            <View style={styles.card}>
              <View style={styles.content}>
                <Text style={styles.display}>flat</Text>
                <Text style={styles.text}>Buttons with custom <Strong>titleColor</Strong> and <Strong>color</Strong></Text>
              </View>
              <View style={{ flexDirection: 'row', justifyContent: 'flex-start' }}>
                <TextButton style={{ margin: 4, marginLeft: 0 }} titleColor="black" title="decline" />
                <TextButton titleStyle={{ fontWeight: 'bold' }} titleColor="pink" title="accept" />
              </View>
            </View>
          </ScrollView>
        </SafeAreaView>
      );
}

export default MaterialButtons;


```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-material-buttons Releases](https://github.com/react-native-oh-library/react-native-material-buttons/releases)

## Properties

### This component has the following properties:
## **API（TextButton ）**
>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|     **titleStyle**      |       Style object for the button's title         |                         Object                           |    No    | iOS/Android |        Yes        |
|        **title**        |                   Button title                    |                         String                           |    YES   | iOS/Android |        Yes        |
|     **titleColor**      |                  Button title color               |                         String                           |    No    | iOS/Android |        Yes        |
| **disabledTitleColor**  |       Button title color for disabled state       |                         String                           |    No    | iOS/Android |        Yes        |

## **API（RaisedTextButton）**
>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|    **rippleOpacity**    |           Opacity of the ripple effect            |                         Number                           |    No    | iOS/Android |        Yes        |
|   **rippleDuration**    |   Duration of the ripple effect in milliseconds   |                         Number                           |    No    | iOS/Android |        Yes        |

## **API（Common）**
>[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

>[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

|          Name           |                    Description                    |                           Type                           | Required |  Platform   | HarmonyOS Support |
|:-----------------------:| :-----------------------------------------------: | :------------------------------------------------------: | :------: | :---------: | :---------------: |
|    **color**    |           Button color            |                         String                           |    No    | iOS/Android |        Yes        |
|   **disabledColor**    |   Button color for disabled state   |                         String                           |    No    | iOS/Android |        Yes        |
|   **shadeColor**    |   Button shade color for focused state   |                         String                           |    No    | iOS/Android |        Yes        |
|   **shadeOpacity**    |   Button shade opacity for focused state   |                         Number                           |    No    | iOS/Android |        Yes        |
|   **shadeBorderRadius**    |   Button shade border radius   |                         Number                           |    No    | iOS/Android |        Yes        |
|   **focusAnimation**    |   Focus animation state   |                         Animated.Value                           |    No    | iOS/Android |        Yes        |
|   **disableAnimation**    |   Disable animation state   |                         Animated.Value                           |    No    | iOS/Android |        Yes        |
|   **focusAnimationDuration**    |   Focus animation duration in ms   |                         Number                           |    No    | iOS/Android |        Yes        |
|   **disableAnimationDuration**    |   Disable animation duration in ms   |                         Number                           |    No    | iOS/Android |        Yes        |
|   **disabled**    |   	Button availability   |                         Boolean                           |    No    | iOS/Android |        Yes        |
|   **onPress**    |   Touch up callback   |                         Function                           |    No    | iOS/Android |        Yes        |
|   **payload**    |   Payload object for onPress callback   |                         Any                           |    No    | iOS/Android |        Yes        |

## Known Issues

## Others

## License

This project is licensed under [MIT License](https://github.com/n4kz/react-native-material-buttons/blob/master/license.txt). 