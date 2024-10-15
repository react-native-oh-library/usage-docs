<!-- {% raw %} -->

> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>qrcode-generator</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/kazuhikoarase/qrcode-generator">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/kazuhikoarase/qrcode-generator/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github address](https://github.com/kazuhikoarase/qrcode-generator)

## Installation and Usage

<!-- tabs:start -->

Go to the project directory and execute the following instruction:

#### **npm**

```bash
npm install qrcode-generator@1.4.4
```

#### **yarn**

```bash
yarn add qrcode-generator@1.4.4
```

The following code shows the basic use scenario of the repository:

```js
import React, { useState, useEffect } from "react";
import { View, Text, Image } from "react-native";
import QRCode from "qrcode-generator";

export const CustomQrCode = ({ text, style }) => {
  const [base64Img, setBase64Img] = useState("hello word");
  useEffect(() => {
    const typeNumber = 4;
    const errorCorrectionLevel = "L";
    const qr = QRCode(typeNumber, errorCorrectionLevel);
    qr.addData(text);
    qr.make();
    setBase64Img(qr.createDataURL(4, 10));
  }, [text]);

  return base64Img ? (
    <Image
      source={{ uri: base64Img }}
      style={style}
      resizeMode="contain"
    ></Image>
  ) : null;
};
```

## Constraints

### Compatibility

This document is verified based on the following versions:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                 | Description                                                | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | ---------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| typeNumber           | Type number (1 ~ 40), or 0 for auto detection.             | number   | Yes      | iOS/Android | Yes               |
| errorCorrectionLevel | Error correction level ('L', 'M', 'Q', 'H')                | string   | Yes      | iOS/Android | Yes               |
| s                    | string to encode                                           | string   | Yes      | iOS/Android | Yes               |
| data                 | string to encode                                           | string   | Yes      | iOS/Android | Yes               |
| mode                 | Mode ('Numeric', 'Alphanumeric', 'Byte'(default), 'Kanji') | function | Yes      | iOS/Android | Yes               |
| row                  | 0 ~ moduleCount - 1                                        | number   | Yes      | iOS/Android | Yes               |
| col                  | 0 ~ moduleCount - 1                                        | number   | Yes      | iOS/Android | Yes               |
| cellSize             | default: 2                                                 | function | No       | iOS/Android | Yes               |
| margin               | default: cellSize \* 4                                     | function | No       | iOS/Android | Yes               |
| alt                  | (optional)                                                 | function | No       | iOS/Android | Yes               |

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                      | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| QRCode(typeNumber,errorCorrectionLevel)   | Create a QRCode Object.                                      | function | Yes      | iOS/Android | Yes               |
| QRCode.stringToBytes(s)                   | Encodes a string into an array of number(byte) using any charset. This function is used by internal. Overwrite this function to encode using a multibyte charset. | function | Yes      | iOS/Android | Yes               |
| QRCode.make()                             | Make a QR Code.                                              | function | Yes      | iOS/Android | Yes               |
| QRCode.getModuleCount()                   | The number of modules(cells) for each orientation. [Note] call make() before this function. | function | Yes      | iOS/Android | Yes               |
| QRCode.isDark(row,col)                    | The module at row and col is dark or not. [Note] call make() before this function. | function | Yes      | iOS/Android | Yes               |
| QRCode.addData(data,mode)                 | Add a data to encode.                                        | function | Yes      | iOS/Android | Yes               |
| QRCode.createDataURL(cellSize, margin)    | Generate base64 links,Helper functions for HTML. [Note] call make() before these functions. | function | Yes      | iOS/Android | Yes               |
| QRCode.createImgTag(cellSize, margin,alt) | Generate img tag QR code,Helper functions for HTML. [Note] call make() before these functions. | function | Yes      | iOS/Android | Yes               |
| QRCode.createSvgTag(cellSize, margin)     | Generate QR codes for svg tags,Helper functions for HTML. [Note] call make() before these functions. | function | Yes      | iOS/Android | Yes               |
| QRCode.createTableTag(cellSize, margin)   | Generate QR codes for table tags,Helper functions for HTML. [Note] call make() before these functions. | function | Yes      | iOS/Android | Yes               |
| QRCode.createASCII(cellSize, margin)      | Generate ASCII code,Helper functions for HTML. [Note] call make() before these functions. | function | Yes      | iOS/Android | Yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/kazuhikoarase/qrcode-generator/blob/master/LICENSE).

<!-- {% endraw %} -->