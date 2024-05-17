 
> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-qrcode</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/cssivision/react-native-qrcode">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/cssivision/react-native-qrcode/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/cssivision/react-native-qrcode)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-qrcode@0.2.7
```

#### **yarn**

```bash
yarn add react-native-qrcode@0.2.7
```

此库是一个React原生的生成二维码的组件，不仅仅支持英文。下面的代码展示了这个库的基本使用场景，更多详情请参考[使用教程](https://github.com/cssivision/react-native-qrcode/blob/master/README.md)：


```js
import React, { Component ,useState,useEffect } from 'react'
import { Image } from 'react-native';
import QRCode from 'react-native-qrcode';
import {Animated, Text, View} from 'react-native';

export function QRCodeExample() {

  const qrCodeSize = 128;
 
  const [codeString, setCodeString] = useState('');

  useEffect(() => {
    const qr = QRCode('#fff', '#000');
    qr.addQRCodeData("http://facebook.github.io/react-native/");
    qr.build();
    const qrUrl = qr.buildDataWithURL();
    setCodeString(qrUrl);
  }, ["http://facebook.github.io/react-native/"]);
  

return (
    
   <View style={{ flex: 1, backgroundColor:"#FFC0CB" }}>
 
     <Image source={{uri:codeString }}
            style={{
            width:qrCodeSize,
            height:qrCodeSize,
            resizeMode:'contain',
          }}/>

  </View>
);
}
```


## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/cssivision/react-native-qrcode/blob/master/LICENSE) ，请自由地享受和参与开源。

