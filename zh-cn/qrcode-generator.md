> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>qrcode-generator</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/kazuhikoarase/qrcode-generator)

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

快速使用：

```js
import React,{useState,useEffect} from "react";
import{View,Text,Image} from "react-native"
import QRCode from 'qrcode-generator'

export const CustomQrCode = ({text,style}) => {
    const [base64Img,setBase64Img] = useState('hello word')
    useEffect(() => {
        const typeNumber = 4
        const errorCorrectionLevel = 'L'
        const qr = QRCode(typeNumber,errorCorrectionLevel)
        qr.addData(text)
        qr.make()
        setBase64Img(qr.createDataURL(4,10))
    },[text])

    return(
        base64Img ? <Image source={{uri:base64Img}} style={style} resizeMode="contain"></Image> : null
    )
}
```

约束与限制
-------------------------------------------------------------------------------------------------------------------------------

### 兼容性

在下述版本验证通过:

1. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.59;

API列表
-------------------------------------------------------------------------------------------------------

**以下 `QRCode` 均为qrcode-generator导出的对象，即：**

```js
import QRCode from 'qrcode-generator';
```

#### Base

**静态方法**

"HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name                                    | Description             | Type     | Required | HarmonyOS Support |
| --------------------------------------- | ----------------------- | -------- | -------- | ----------------- |
| QRCode(typeNumber,errorCorrectionLevel) | Create a QRCode Object. | function | Yes      | Yes               |

**api**

| Name                 | Description                                    | Type   | Required | HarmonyOS Support |
| -------------------- | ---------------------------------------------- | ------ | -------- | ----------------- |
| typeNumber           | Type number (1 ~ 40), or 0 for auto detection. | number | Yes      | Yes               |
| errorCorrectionLevel | Error correction level ('L', 'M', 'Q', 'H')    | string | Yes      | Yes               |

**静态方法**

| Name                    | Description                                                                                                                                                       | Type     | Required | HarmonyOS Support |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| QRCode.stringToBytes(s) | Encodes a string into an array of number(byte) using any charset. This function is used by internal. Overwrite this function to encode using a multibyte charset. | function | Yes      | Yes               |

api

| Name | Description      | Type   | Required | HarmonyOS Support |
| ---- | ---------------- | ------ | -------- | ----------------- |
| s    | string to encode | string | Yes      | Yes               |

**静态方法**

| Name                      | Description           | Type     | Required | HarmonyOS Support |
| ------------------------- | --------------------- | -------- | -------- | ----------------- |
| QRCode.addData(data,mode) | Add a data to encode. | function | Yes      | Yes               |

api

| Name | Description                                                | Type   | Required | HarmonyOS Support |
| ---- | ---------------------------------------------------------- | ------ | -------- | ----------------- |
| data | string to encode                                           | string | Yes      | Yes               |
| mode | Mode ('Numeric', 'Alphanumeric', 'Byte'(default), 'Kanji') | Yes    |          |                   |

**静态方法**

| Name                    | Description                                                                                 | Type     | Required | HarmonyOS Support |
| ----------------------- | ------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| QRCode.make()           | Make a QR Code.                                                                             | function | Yes      | Yes               |
| QRCode.getModuleCount() | The number of modules(cells) for each orientation. [Note] call make() before this function. | function | Yes      | Yes               |
| QRCode.isDark(row,col)  | The module at row and col is dark or not. [Note] call make() before this function.          | function | Yes      | Yes               |

**api**

| Name | Description         | Type   | Required | HarmonyOS Support |
| ---- | ------------------- | ------ | -------- | ----------------- |
| row  | 0 ~ moduleCount - 1 | number | Yes      | Yes               |
| col  | 0 ~ moduleCount - 1 | number | Yes      | Yes               |



**静态方法**

| Name                                      | Description                                                                                            | Type     | Required | HarmonyOS Support |
| ----------------------------------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | ----------------- |
| QRCode.createDataURL(cellSize, margin)    | Generate base64 links,Helper functions for HTML. [Note] call make() before these functions.            | function | Yes      | Yes               |
| QRCode.createImgTag(cellSize, margin,alt) | Generate img tag QR code,Helper functions for HTML. [Note] call make() before these functions.         | function | Yes      | Yes               |
| QRCode.createSvgTag(cellSize, margin)     | Generate QR codes for svg tags,Helper functions for HTML. [Note] call make() before these functions.   | function | Yes      | Yes               |
| QRCode.createTableTag(cellSize, margin)   | Generate QR codes for table tags,Helper functions for HTML. [Note] call make() before these functions. | function | Yes      | Yes               |
| QRCode.createASCII(cellSize, margin)      | Generate ASCII code,Helper functions for HTML. [Note] call make() before these functions.              | function | Yes      | Yes               |

**api**

| Name     | Description           | Type     | Required | HarmonyOS Support |
| -------- | --------------------- | -------- | -------- | ----------------- |
| cellSize | default: 2            | function | No       | Yes               |
| margin   | default: cellSize * 4 | function | No       | Yes               |
| alt      | (optional)            | function | No       | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/facebook/prop-types/blob/v15.8.1/LICENSE) ，请自由地享受和参与开源。
