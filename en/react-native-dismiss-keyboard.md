> Template version: v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-dismiss-keyboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/DanielMSchmidt/react-native-dismiss-keyboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/DanielMSchmidt/react-native-dismiss-keyboard/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/DanielMSchmidt/react-native-dismiss-keyboard)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-dismiss-keyboard@1.0.0
```

#### **yarn**

```bash
yarn add react-native-dismiss-keyboard@1.0.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { Component } from "react";
import {
  AppRegistry,
  StyleSheet,
  TextInput,
  View,
  Text,
  Keyboard,
} from "react-native";

export default class ReactNativeDismissKeyboardExample extends Component {
  keyboardDidShowListener = null;
  keyboardDidHideListener = null;
  state = { KeyboardShown: false };

  constructor(props) {
    super(props);
    this.keyboardDidShowListener = null;
    this.keyboardDidHideListener = null;
    this.state = { KeyboardShown: false };
  }

  keyboardDidShowHandler(event) {
    this.setState({ KeyboardShown: true });
    console.log(event.endCoordinates.height);
  }

  keyboardDidHideHandler(event) {
    this.setState({ KeyboardShown: false });
  }

  dissmissKeyboard() {
    Keyboard.dismiss();
    console.log("the current focus state of the input box" + this.refs.bottomInput.isFocused());
  }

  render() {
    return (
      <View style={[styles.container]}>
        <View style={[styles.flexDirection, styles.inputHeight]}>
          <TextInput style={styles.textInputStyle} ref="bottomInput" />
          <Text
            style={styles.buttonStyle}
            onPress={this.dissmissKeyboard.bind(this)}
          >
            close keyboard
          </Text>
        </View>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    paddingTop: 15,
    backgroundColor: "#ffffff",
  },
  flexDirection: {
    flexDirection: "row",
  },
  inputHeight: {
    height: 35,
    alignItems: "center",
  },
  textInputStyle: {
    flex: 1,
    height: 35,
    fontSize: 18,
    borderWidth: 1,
    borderColor: "#4CAF50",
    borderRadius: 8,
    marginRight: 8,
  },
  buttonStyle: {
    fontSize: 20,
    color: "white",
    width: 100,
    textAlign: "center",
    backgroundColor: "#4CA300",
  },
});
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Prop                      | Description                                                                                                                     | Type     | Required | Platform | HarmonyOS Support |
| ------------------------- | ------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `addListener`             | Register a JavaScript function that listens to handle native keyboard notification events.                                      | function | no       | All      | yes               |
| `dismiss`                 | Retract the pop-up keyboard and make the current text box lose focus.                                                           | function | no       | All      | yes               |
| `scheduleLayoutAnimation` | Used to synchronize changes in the size or position of a TextInput (or other keyboard attachment view) with keyboard movements. | function | no       | All      | yes               |
| `isVisible`               | Whether the keyboard is currently displayed.                                                                                    | function | no       | All      | yes               |
| `metrics`                 | If a soft keyboard is displayed, return the size of the soft keyboard.                                                          | function | no       | All      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/DanielMSchmidt/react-native-dismiss-keyboard/blob/master/LICENSE).

