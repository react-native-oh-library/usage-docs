模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>qrcode-generator</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/aMarCruz/react-native-text-size">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-text-size/blob/sig/LICENSE>">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

[Github 地址](https://github.com/kazuhikoarase/qrcode-generator)
安装与使用
-------------------------------------------------------------------------------------------------------------------------------

进入到工程目录并输入以下命令：

**npm**

```bash
npm install qrcode-generator
```

**yarn**

```bash
yarn add qrcode-generator
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

#### 兼容性



在下述版本验证通过：



1. RNOH：0.72.11; SDK：OpenHarmony(api11) 4.1.0.53; IDE：DevEco Studio 4.1.3.412; ROM：2.0.0.52;
2. RNOH：0.72.13; SDK：HarmonyOS NEXT Developer Preview1; IDE：DevEco Studio 4.1.3.500; ROM：2.0.0.58;

API列表
-------------------------------------------------------------------------------------------------------

**以下 `QRCode` 均为qrcode-generator导出的对象，即：**

```js
import QRCode from 'qrcode-generator';
```

#### Base

**静态方法**

"HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。



| Name                                    | Description | Type     | Required | HarmonyOS Support |
| --------------------------------------- | ----------- | -------- | -------- | ----------------- |
| QRCode(typeNumber,errorCorrectionLevel) | 创建二维码对象     | function | Yes      | Yes               |

**api**

| Name                 | Description            | Type   | Required | HarmonyOS Support |
| -------------------- | ---------------------- | ------ | -------- | ----------------- |
| typeNumber           | 二维码类型（1~40，输入 0 以自动检测） | number | Yes      | Yes               |
| errorCorrectionLevel | 容错级别（L、M、Q、H）          | string | Yes      | Yes               |

**静态方法**

| Name                    | Description                                           | Type     | Required | HarmonyOS Support |
| ----------------------- | ----------------------------------------------------- | -------- | -------- | ----------------- |
| QRCode.stringToBytes(s) | 将任意字符集的字符串编译成字节序列。这个函数是internal的，重写这个函数可在多字节字符集下编译字符串 | function | Yes      | Yes               |

api

| Name | Description | Type   | Required | HarmonyOS Support |
| ---- | ----------- | ------ | -------- | ----------------- |
| s    | 待编译的字符串     | string | Yes      | Yes               |

**静态方法**

| Name                      | Description | Type     | Required | HarmonyOS Support |
| ------------------------- | ----------- | -------- | -------- | ----------------- |
| QRCode.addData(data,mode) | 添加二维码信息     | function | Yes      | Yes               |

api

| Name | Description                                                                                                       | Type   | Required | HarmonyOS Support |
| ---- | ----------------------------------------------------------------------------------------------------------------- | ------ | -------- | ----------------- |
| data | 二维码信息                                                                                                             | string | Yes      | Yes               |
| mode | 信息编译模式，可设置为：<br/>Numeric   数字<br/>Alphanumeric 文字数字混合<br/>Byte                字节（默认）<br/>Kanji               日语汉字 | string | No       | Yes               |

**静态方法**

| Name                    | Description                  | Type     | Required | HarmonyOS Support |
| ----------------------- | ---------------------------- | -------- | -------- | ----------------- |
| QRCode.make()           | 生成二维码对象（并不显示）                | function | Yes      | Yes               |
| QRCode.getModuleCount() | 获取二维码每行（orientation）的 cell 数 | function | Yes      | Yes               |
| QRCode.isDark(row,col)  | 返回指定行列上的 cell 是否有信息（黑色）      | function | Yes      | Yes               |

api

| Name | Description          | Type   | Required | HarmonyOS Support |
| ---- | -------------------- | ------ | -------- | ----------------- |
| row  | 行坐标（0~moduleCount-1） | number | Yes      | Yes               |
| col  | 列坐标（0~moduleCount-1） | number | Yes      | Yes               |



**静态方法**

| Name                                      | Description               | Type     | Required | HarmonyOS Support |
| ----------------------------------------- | ------------------------- | -------- | -------- | ----------------- |
| QRCode.createDataURL(cellSize, margin)    | 生成base64格式的二维码内容          | function | Yes      | Yes               |
| QRCode.createImgTag(cellSize, margin,alt) | 生成img标签格式的HTML Helper函数   | function | Yes      | Yes               |
| QRCode.createSvgTag(cellSize, margin)     | 生成svg标签格式的HTML Helper函数   | function | Yes      | Yes               |
| QRCode.createTableTag(cellSize, margin)   | 生成table标签格式的HTML Helper函数 | function | Yes      | Yes               |
| QRCode.createASCII(cellSize, margin)      | 生成ASCII码                  | function | Yes      | Yes               |

api

| Name     | Description           | Type     | Required | HarmonyOS Support |
| -------- | --------------------- | -------- | -------- | ----------------- |
| cellSize | cell 像素宽度，默认为 2       | function | No       | Yes               |
| margin   | 补白像素宽度，默认为 cellSize*4 | function | No       | Yes               |
| alt      | image 的提示             | function | No       | Yes               |

遗留问题
---------------------------------------------------------------------------------------------------------------------

其他
-------------------------------------------------------------------------------------------------

开源协议
---------------------------------------------------------------------------------------------------------------------

本项目基于 [MIT License](https://github.com/brix/crypto-js/blob/4.2.0/LICENSE) ，请自由地享受和参与开源。
