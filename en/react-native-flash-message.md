> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-flash-message</code> </h1>
</p>
<p align="center">
   <a href="https://github.com/lucasferreira/react-native-flash-message">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lucasferreira/react-native-flash-message/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!Tip] [GitHub address](https://github.com/lucasferreira/react-native-flash-message)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-flash-message@0.4.2
```

#### **yarn**

```bash
yarn add react-native-flash-message@0.4.2
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

```js
import React from "react";
import { SafeAreaView, View } from "react-native";
import FlashMessage from "react-native-flash-message";
function App() {
  return (
    <View style={{ backgroundColor: "white" }}>
      <SafeAreaView></SafeAreaView>
      <FlashMessage position="top" />
    </View>
  );
}
export default App;
```

```js
import { StyleSheet, Text, View, Image, TouchableOpacity } from "react-native";
import { showMessage, hideMessage } from "react-native-flash-message";

export function FlashMessageTest() {
  return (
    <View style={styles.container}>
      <TouchableOpacity
        style={styles.button}
        onPress={() => {
          showMessage({
            message: "show message",
            type: "info",
            onPress: () => {
              hideMessage();
            },
            autoHide: false,
            renderAfterContent: (e) => {
              return (
                <View>
                  <Text>renderAfterContent</Text>
                </View>
              );
            },
          });
        }}
      >
        <Text>renderAfterContent</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    justifyContent: "center",
    alignItems: "center",
    padding: 10,
    margin: 25,
    borderRadius: 5,
    borderWidth: 3,
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: "red",
    borderRadius: 5,
  },
});
```

## Compatibility

This document is verified based on the following versions:

1.RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## Static Methods

> [!Tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!Tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

For details, see [react-native-flash-message](https://github.com/lucasferreira/react-native-flash-message/blob/v0.4.0/README.md)

| Name                   | Description                                                  | Required | Platform    | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | -------- | ----------- | ----------------- |
| hideOnPress            | Controls if the flash message can be closed on press         | NO       | iOS/Android | YES               |
| onPress                | onPress callback for flash message press                     | NO       | iOS/Android | YES               |
| onLongPress            | onLongPress callback for flash message press                 | NO       | iOS/Android | YES               |
| animated               | Controls if the flash message will be shown with animation or not | NO       | iOS/Android | YES               |
| animationDuration      | Animations duration/speed                                    | NO       | iOS/Android | YES               |
| autoHide               | Controls if the flash message can hide itself after some duration time | NO       | iOS/Android | YES               |
| duration               | How many milliseconds the flash message will be shown if the autoHide it's true | NO       | iOS/Android | YES               |
| hideStatusBar          | Controls if the flash message will auto hide the native status bar. Note: Works OK in iOS, not all Android versions support this. | NO       | iOS/Android | YES               |
| statusBarHeight        | Use this prop to set a custom status bar height that will be add in flash message padding top calc | NO       | iOS/Android | YES               |
| floating               | The floating prop unstick the message from the edges and applying some border radius to component | NO       | iOS/Android | YES               |
| position               | The position prop set the position of a flash message. Expected options: "top" (default), "bottom", "center" or a custom object with { top, left, right, bottom } position | NO       | iOS/Android | YES               |
| icon                   | The icon prop could be a render function that return a new JSX Element to be placed in icon position OR a definition of the graphical icon of a flash message. Expected options: "none" (default), "auto" (guided by type), "success", "info", "warning", "danger", a custom icon (render function) or a custom object with icon type/name and position (left or right) attributes, e.g.: { icon: "success", position: "right" } | NO       | iOS/Android | YES               |
| style                  | Apply a custom style object in flash message container       | NO       | iOS/Android | YES               |
| textStyle              | Apply a custom style object in flash message descript/text text label | NO       | iOS/Android | YES               |
| titleStyle             | Apply a custom style object in flash message title text label | NO       | iOS/Android | YES               |
| titleProps             | Set a custom props object in flash message title text label  | NO       | iOS/Android | YES               |
| textProps              | Set a custom props object in flash message all text components | NO       | iOS/Android | YES               |
| iconProps              | Set a custom props object to use inside the renderFlashMessageIcon method as third argument | NO       | iOS/Android | YES               |
| renderBeforeContent    | Render custom JSX before title in flash message.             | NO       | iOS/Android | YES               |
| renderCustomContent    | Render custom JSX below title in flash message.              | NO       | iOS/Android | YES               |
| renderAfterContent     | Render custom JSX after the title (or description) of a flash message. | NO       | iOS/Android | YES               |
| renderFlashMessageIcon | Set a custom render function for inside message icons        | NO       | iOS/Android | YES               |
| transitionConfig       | Set the transition config function used in shown/hide anim interpolations | NO       | iOS/Android | YES               |
| canRegisterAsDefault   | Use to handle if the instance can be registed as default/global instance | NO       | iOS/Android | YES               |
| MessageComponent       | Set the default flash message render component used to show all the messages | NO       | iOS/Android | YES               |

## Known Issues

- [ ] The effect on iOS is different from that on HarmonyOS. The **StatusBar.setHidden()** method in the **StatusBar** component of the RN framework is used to hide the status bar of the mobile phone. The specific effect varies and this issue has not been resolved. The reason is that on HarmonyOS smartphones, the bottom of the system non-safe area at the top of the phone is not consistent in height with the bottom of the front camera cutout area. During the process of showing and hiding the status bar, the height of the system non-safe area will be 0 or 136, varying by device. This causes the top of the window where the content component is located to align either with the bottom of the front camera cutout area or the bottom of the system non-safe area in the two states, resulting in jitter. The visibility state of the status bar and the size of the non-safe area of types like **SystemAvoidView** are not strongly correlated. Compared with HarmonyOS, iOS does not have a non-safe area at the top of the screen, which does not require the avoidance design.

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lucasferreira/react-native-flash-message/blob/master/LICENSE).
