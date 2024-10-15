<!-- {% raw %} -->

> 模板版本：v0.2.2

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


> [!TIP] [Github 地址](https://github.com/kazuhikoarase/qrcode-generator)

## 安装与使用

<!-- tabs:start -->

进入到工程目录并输入以下命令：

#### **npm**

```bash
npm install qrcode-generator@1.4.4
```

#### **yarn**

```bash
yarn add qrcode-generator@1.4.4
```

下面的代码展示了这个库的基本使用场景：

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

## 约束与限制

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Preview2; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;
2. RNOH：0.72.33; SDK：OpenHarmony 5.0.0.71(API Version 12 Release); IDE：DevEco Studio 5.0.3.900; ROM：NEXT.0.0.71;

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS或 Android 的效果。

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

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/kazuhikoarase/qrcode-generator/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->