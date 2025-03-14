> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qrcode-svg</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/awesomejerry/react-native-qrcode-svg">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE">
        <img src="https://img.shields.io/npm/l/react-native-qrcode-svg.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/awesomejerry/react-native-qrcode-svg)

## 安装与使用

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install react-native-qrcode-svg@6.2.0
```

#### **yarn**

```bash
yarn add react-native-qrcode-svg@6.2.0
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。
> [!TIP] 当报错信息为`Property 'TextEncoder' doesn't exist`[解决方案](https://github.com/awesomejerry/react-native-qrcode-svg/issues/199)


```js
import {  Text, View } from "react-native";
import QRCode from 'react-native-qrcode-svg';

export const SvgDemo = () => {
    return (
        <View style={{ flex: 1, backgroundColor: '#FFFFFF' }}>
            <QRCode
                size={300}
              
                value="http://awesome.link.qr"
            />
        </View>
    )
}
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg-capi 文档的 Link 章节](/zh-cn/react-native-svg-capi.md)进行引入

## 约束与限制

### 兼容性

在以下版本验证通过

1.RNOH：0.72.27; SDK：HarmonyOS-Next-DB1 5.0.0.29(SP1); IDE：DevEco Studio 5.0.3.400; ROM：3.0.0.25;

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                                                                               | Type     | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `size`                 | Size of rendered image in pixels                                                                                          | number   | No       | iOS,Android      | yes               |
| `value`                | String Value of the QR code                                                                                               | string   | yes      | iOS,Android      | yes               |
| `color`                | Color of the QR code                                                                                                      | string   | No       | iOS,Android      | yes               |
| `backgroundColor`      | Color of the background                                                                                                   | string   | No       | iOS,Android      | yes               |
| `enableLinearGradient` | enables or disables linear gradient                                                                                       | boolean  | No       | iOS,Android      | yes                |
| `linearGradient`       | array of 2 rgb colors used to create the linear gradient                                                                  | string[] | No       | iOS,Android      | yes                |
| `gradientDirection`    | the direction of the linear gradient                                                                                      | string   | No       | iOS,Android      | yes                |
| `logo`                 | Image source object. Ex. {uri: 'base64string'} or {require('pathToImage')}                                                | object   | No       | iOS,Android      | yes               |
| `logoSize`             | Size of the imprinted logo. Bigger logo = less error correction in QR code                                                | number   | No       | iOS,Android      | yes               |
| `logoBackgroundColor`  | The logo gets a filled quadratic background with this color. Use 'transparent' if your logo already has its own backdrop. | string   | No       | iOS,Android      | yes               |
| `logoMargin`           | logo's distance to its wrapper                                                                                            | number   | No       | iOS,Android      | yes               |
| `logoBorderRadius`     | the border-radius of logo image (Android is not supported)                                                                | number   | No       | iOS      | yes                |
| `quietZone`            | quiet zone around the qr in pixels (useful when saving image to gallery)                                                  | number   | No       | iOS,Android      | yes                |
| `getRef`               | Get SVG ref for further usage                                                                                             | callback | No       | iOS,Android      | yes            |
| `ecl`                  | Error correction level                                                                                                    | string   | No       | iOS,Android      | yes               |
| `onError(error)`       | Callback fired when exception happened during the code generating process                                                 | callback | No       | iOS,Android      | yes            |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE) ，请自由地享受和参与开源。
