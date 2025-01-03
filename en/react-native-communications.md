> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-communications</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/davebeehively/react-native-communications">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/davebeehively/react-native-communications/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/davebeehively/react-native-communications)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-communications@2.2.1
```

#### **yarn**

```bash
yarn add react-native-communications@2.2.1
```

<!-- tabs:end -->

> [!WARNING] The name of the imported repository remains unchanged.

```js
var React = require("react-native");
var { StyleSheet, View, TouchableOpacity, Text } = React;

import {
  phonecall,
  text,
  textWithoutEncoding,
  email,
  web,
} from "react-native-communications";

const RNCommunications = () => {
  const handleButton1Press = () => {
    phonecall("0123456789", false);
  };
  const handleButton2Press = () => {
    email(["email@xxx.com"], null, null, "My Subject", "My body text");
  };
  const handleButton3Press = () => {
    text("0123456789");
  };
  const handleButton4Press = () => {
    web("https://www.baidu.com");
  };
  const handleButton5Press = () => {
    textWithoutEncoding("0123456789", "9999999");
  };

  return (
    <View style={styles.container}>
      <TouchableOpacity style={styles.button} onPress={handleButton1Press}>
        <Text>Make phonecall</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton2Press}>
        <Text>Send an email</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton3Press}>
        <Text>Send a text only phonenumber</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton4Press}>
        <Text>web to baidu</Text>
      </TouchableOpacity>
      <TouchableOpacity style={styles.button} onPress={handleButton5Press}>
        <Text>Send a text with body</Text>
      </TouchableOpacity>
    </View>
  );
};

var styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: "center",
    alignItems: "center",
  },
  button: {
    padding: 10,
    margin: 5,
    backgroundColor: "white",
    borderRadius: 5,
  },
});

export default RNCommunications;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1.RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25; IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.25;

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                      | Type     | Required | Platform | HarmonyOS Support |
| ------------------- | -------------------------------- | -------- | -------- | -------- | ----------------- |
| phonecall           | Initiates a call.                        | function | yes      | All      | yes               |
| email               | Sends an email.                    | function | yes      | All      | no                |
| text                | Sends a text message.                    | function | yes      | All      | yes               |
| textWithoutEncoding | Send a text message without encoding it.| function | yes      | All      | yes               |
| web                 | Opens a specified web page.              | function | yes      | All      | yes               |

## Known Issues

- [ ] There is no email application on HarmonyOS. As a result, the email method cannot open the email sending page.
- [ ] After body is added to text, the text input box cannot be split on the SMS page. This is not supported by the framework API **Linking.canOpenURL**.

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/davebeehively/react-native-communications/blob/master/LICENSE).
