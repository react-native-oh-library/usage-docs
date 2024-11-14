> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-vector-drawable</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/klarna-incubator/react-native-vector-drawable">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/klarna-incubator/react-native-vector-drawable/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-vector-drawable)

## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-library/react-native-vector-drawable Releases](https://github.com/react-native-oh-library/react-native-vector-drawable/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：



<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-vector-drawable
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-vector-drawable
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx

import React from "react";
import { View } from 'react-native';
import VectorDrawable from "react-native-vector-drawable";
export default function VectorDrawableDemo(): JSX.Element {
    return <View>
            <VectorDrawable
               resourceName="ic_drawable_name"
               style={{ width: 50, height: 50, tintColor: 'blue' }}
            />
    </View>
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-vector-drawable Releases](https://github.com/react-native-oh-library/react-native-vector-drawable/releases)


## 属性
原库中Android平台实现是通过android.graphics.drawable.Drawable方法加载[xml矢量图片](https://github.com/klarna-incubator/react-native-vector-drawable/blob/master/example/android/app/src/main/res/drawable/ic_klarna_logo.xml)文件，在iOS平台是通过[React-Native View](https://reactnative.cn/docs/view)来实现，HarmonyOS与iOS保持一致，属性见[React-Native View组件](https://reactnative.cn/docs/view)

> [!Tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!Tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| resourceName    | Name of the Android vector drawable resource. | string | true       | Android | No           |
| style    | See Style props. Note: border props are not supported. | object | false       | Android | No               |

style Props
| Name           | Description                   | Type | Required |Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | -------- | ----------------- |
| resizeMode    | 	Determines how to resize the image when the frame doesn't match the raw image dimensions. Possible values are cover, contain, stretch and center | string | false | Android | No        |
| tintColor    | Changes the color of all the non-transparent pixels to the tintColor. | string | false | Android | No   |
## 其他

## 开源协议

本项目基于 [The Apache License (Apache)](https://github.com/klarna-incubator/react-native-vector-drawable/blob/master/LICENSE) ，请自由地享受和参与开源。
