> Template version: v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-htmlview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jsdf/react-native-htmlview">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jsdf/react-native-htmlview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/jsdf/react-native-htmlview)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-htmlview@0.17.0
```

#### **yarn**

```bash
yarn add react-native-htmlview@0.17.0
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { StyleSheet, View, Linking } from "react-native";
import HTMLView from "react-native-htmlview";

const HtmlViewExample = () => {
  const htmlContent = `
      <h1>Hello, World!</h1>
      <p>This is a <a href="https://www.vmall.com">link</a></p>
      <p>Here is an image: <img src="https://res.vmallres.com/pimages/uomcdn/CN/pms/202404/displayProduct/10086102004921/428_428_a_mobileFF345C8650FF6E88771386A6433556D0.jpg" alt="Example Image" /></p>
  `;

  return (
    <View style={{ ...styles.container, backgroundColor: "white" }}>
      <HTMLView
        value={htmlContent}
        stylesheet={styles} // Optional: Pass custom styles for HTML elements
        onLinkPress={(url) => Linking.openURL(url)} // Optional: Handle link presses
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 16,
  },
  // Define custom styles for HTML elements
  a: {
    fontWeight: "bold",
    color: "blue",
    fontSize: 20,
    borderColor: "#000000",
    borderWidth: 2,
  },
  img: {
    width: 200,
    height: 100,
  },
});

export default HtmlViewExample;
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

> [!TIP] 该库为 UI 组件库，可以在该库的标签下，使原本无法在 RN 框架生效的 Html 写法，可以实现对应的功能。

| Name            | Description                                                                                                              | Type   | Required | Platform | HarmonyOS Support |
| --------------- | ------------------------------------------------------------------------------------------------------------------------ | ------ | -------- | -------- | ----------------- |
| value           | a string of HTML content to render                                                                                       | string | yes      | All      | yes               |
| onLinkPress     | a function which will be called with a url when a link is pressed. Passing this prop will override how links are handled | string | no       | All      | yes               |
| onLinkLongPress | a function which will be called with a url when a link is long pressed. The default is                                   | string | no       | All      | yes               |
| stylesheet      | a stylesheet object keyed by tag name, which will override the styles applied to those respective tags.                  | string | no       | All      | yes               |
| renderNode      | a custom function to render HTML nodes however you see fit.                                                              | string | no       | All      | yes               |
| bullet          | text which is rendered before every inside a ` li``ul `                                                                  | string | no       | All      | yes               |
| paragraphBreak  | text which appears after every element`p`                                                                                | string | no       | All      | yes               |
| lineBreak       | text which appears after text elements which create a new line                                                           | string | no       | All      | yes               |
| addLineBreaks   | when explicitly , effectively sets                                                                                       | string | no       | All      | yes               |

## License

This project is licensed under [The ISC License (ISC)](https://github.com/jsdf/react-native-htmlview/blob/master/LICENSE).
