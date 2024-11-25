> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qrcode</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cssivision/react-native-qrcode">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cssivision/react-native-qrcode/blob/master/LICENSE">
       <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-qrcode)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-qrcode](https://github.com/react-native-oh-library/react-native-qrcode/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-qrcode
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-qrcode
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import QRCode from "react-native-qrcode";
import { StyleSheet, View, TextInput, Button } from "react-native";
export const QrCodeExamle = () => {
  const [text, setText] = useState("");
  const [QRCodeValue, setQRCodeValue] = useState < any > null;
  const showQRCode = () => {
    setQRCodeValue(text);
  };
  const reset = () => {
    setQRCodeValue(null);
    setText("");
  };
  return (
    <View style={styles.container}>
      <TextInput
        placeholder="Please enter the text to generate the QR code."
        style={styles.input}
        onChangeText={(text) => setText(text)}
        value={text}
      />
      <View style={{ flexDirection: "row" }}>
        <Button title="Click to generate a QR code" onPress={showQRCode} />
        <Button title="reset" onPress={reset} />
      </View>

      {QRCodeValue && (
        <QRCode
          value={QRCodeValue}
          size={200}
          bgColor="black"
          fgColor="white"
        />
      )}
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    backgroundColor: "white",
    alignItems: "center",
  },

  input: {
    width: 300,
    height: 40,
    borderColor: "gray",
    borderWidth: 1,
    margin: 10,
    borderRadius: 5,
    padding: 5,
  },
});
```

## Link

The HarmonyOS implementation of this library depends on the native code from @react-native-oh-tpl/react-native-webview. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly.

If it is not included, follow the guide provided in [@react-native-oh-tpl/react-native-webview](/en/react-native-webview.md) to add it to your project.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-qrcode](https://github.com/react-native-oh-library/react-native-qrcode/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### QRCode

该库为 UI 组件库，通过配置属性标签，实现对应的功能。

| Name    | Type   | Description                 | Required | Platform    | HarmonyOS Support |
| ------- | ------ | --------------------------- | -------- | ----------- | ----------------- |
| value   | string | What the qrcode stands for. | no       | iOS/Android | yes               |
| size    | number | qrcode size                 | no       | iOS/Android | yes               |
| bgColor | string | backgroundColor             | no       | iOS/Android | yes               |
| fgColor | string | fgColor                     | no       | iOS/Android | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-qrcode/blob/master/LICENSE).
