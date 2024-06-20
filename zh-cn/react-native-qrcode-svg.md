> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-qrcode-svg</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-qrcode-svg">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE">
        <img src="https://img.shields.io/npm/l/react-native-qrcode-svg.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-qrcode-svg)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-qrcode-svg Releases](https://github.com/react-native-oh-library/react-native-qrcode-svg/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-qrcode-svg@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-qrcode-svg@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import QRCode from 'react-native-qrcode-svg';

// Simple usage, defaults for all but the value
render() {
  return (
    <QRCode
      value="react-native-qrcode-svg"
    />
  );
};
```

## Link

本库 HarmonyOS 侧实现依赖@react-native-oh-tpl/react-native-svg 的原生端代码，如已在 HarmonyOS 工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-svg 文档的 Link 章节](/zh-cn/react-native-svg.md#link)进行引入

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-qrcode-svg Releases](https://github.com/react-native-oh-library/react-native-qrcode-svg/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description                                                                                                               | Type     | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| `size`                 | Size of rendered image in pixels                                                                                          | number   | No       | All      | yes               |
| `value`                | String Value of the QR code                                                                                               | string   | yes      | All      | yes               |
| `color`                | Color of the QR code                                                                                                      | string   | No       | All      | yes               |
| `backgroundColor`      | Color of the background                                                                                                   | string   | No       | All      | yes               |
| `enableLinearGradient` | enables or disables linear gradient                                                                                       | boolean  | No       | All      | no                |
| `linearGradient`       | array of 2 rgb colors used to create the linear gradient                                                                  | string[] | No       | All      | no                |
| `gradientDirection`    | the direction of the linear gradient                                                                                      | string   | No       | All      | no                |
| `logo`                 | Image source object. Ex. {uri: 'base64string'} or {require('pathToImage')}                                                | object   | No       | All      | yes               |
| `logoSize`             | Size of the imprinted logo. Bigger logo = less error correction in QR code                                                | number   | No       | All      | yes               |
| `logoBackgroundColor`  | The logo gets a filled quadratic background with this color. Use 'transparent' if your logo already has its own backdrop. | string   | No       | All      | yes               |
| `logoMargin`           | logo's distance to its wrapper                                                                                            | number   | No       | All      | yes               |
| `logoBorderRadius`     | the border-radius of logo image (Android is not supported)                                                                | number   | No       | ios      | no                |
| `quietZone`            | quiet zone around the qr in pixels (useful when saving image to gallery)                                                  | number   | No       | All      | no                |
| `getRef`               | Get SVG ref for further usage                                                                                             | callback | No       | All      | 不涉及            |
| `ecl`                  | Error correction level                                                                                                    | string   | No       | All      | yes               |
| `onError(error)`       | Callback fired when exception happened during the code generating process                                                 | callback | No       | All      | 不涉及            |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/awesomejerry/react-native-qrcode-svg/blob/master/LICENSE) ，请自由地享受和参与开源。
