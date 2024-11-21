Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-hyperlink</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/obipawan/react-native-hyperlink">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/obipawan/react-native-hyperlink/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [ GitHub address](https://github.com/obipawan/react-native-hyperlink)

## Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-hyperlink@0.0.22
```

#### **yarn**

```bash
yarn add react-native-hyperlink@0.0.22
```

When using it, you also need to configure querySchemes in the module.json5 under the project.

```diff
{
  "module": {
    ...
+   "querySchemes": ["maps","http","https","customDomain"],
  }
}
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState } from "react";
import { View, Text } from "react-native";
import Hyperlink from "react-native-hyperlink";

export default function App() {
  return (
    <Hyperlink
      linkDefault
      injectViewProps={(url) => ({
        testID: url === "http://link.com" ? "id1" : "id2",
        style:
          url === "https://link.com" ? { color: "red" } : { color: "blue" },
        //any other props you wish to pass to the component
      })}
    >
      <Text>
        You can pass props to clickable components matched by url.
        <Text>This url looks red https://link.com</Text> and this url looks blue
        https://link2.com{" "}
      </Text>
    </Hyperlink>
  );
}
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH: 0.72.27; SDK: HarmonyOS-Next-DB1 5.0.0.25 (API Version 12 Canary4); IDE: DevEco Studio 5.0.3.400SP7; ROM: 3.0.0.29;
2. RNOH: 0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description                                                                       | Type                   | Required | Platform | HarmonyOS Support |
| --------------- | --------------------------------------------------------------------------------- | ---------------------- | -------- | -------- | ----------------- |
| linkify         | linkify-it object, for custom schema                                              | object                 | no       | all      | yes               |
| linkStyle       | highlight clickable text with styles                                              | object                 | no       | all      | yes               |
| linkText        | A string or a func to replace parsed text                                         | string &#124; function | no       | all      | yes               |
| onPress         | Func to handle click over a clickable text with parsed text as arg                | function               | no       | all      | yes               |
| onLongPress     | Func to handle long click over a clickable text with parsed text as arg           | function               | no       | all      | yes               |
| linkDefault     | A platform specific fallback to handle onPress. Uses Linking. Disabled by default | boolean                | no       | all      | yes               |
| injectViewProps | Func with url as a param to inject props to the clickable component               | function               | no       | all      | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/obipawan/react-native-hyperlink/blob/master/LICENSE).
