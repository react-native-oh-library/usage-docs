<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-base64</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/SnappFr/react-native-image-base64">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/SnappFr/react-native-image-base64/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-base64)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-base64 Releases](https://github.com/react-native-oh-library/react-native-image-base64/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-base64@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-base64@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { StyleSheet, View, Button, Image } from "react-native";
import React from "react";
import ImgToBase64 from "react-native-image-base64";
import { isSourceFile } from "typescript";

export default function PermissionsExample() {
  const viewPer = React.useRef < View > null;
  const ref = React.useRef(null);
  const onCapture = (uri: any) => {
    console.info("onCapture callback");
    setTxt(JSON.stringify(uri));
  };
  const onCaptureFailure = (err: any) => {
    console.info("onCaptureFailure " + JSON.stringify(err));
    setTxt(JSON.stringify(err));
  };
  const [txt, setTxt] = React.useState("");
  return (
    <View style={styles.sectionContainer}>
      <Button
        title="获取网络图片的Base64编码"
        onPress={async () => {
          let base64Str = await ImgToBase64.getBase64String(
            "https://img0.baidu.com/it/u=2303734322,1592927702&fm=253&fmt=auto&app=138&f=PNG?w=500&h=500"
          );
          console.info("Image's Base64:", base64Str);
        }}
        style={styles.button}
      />
      {/* 两按钮之间的垂直距离 */}
      <View style={styles.buttonSpacing} />
      <Button
        title="获取本地图片的Base64编码"
        onPress={async () => {
          let base64Str = await ImgToBase64.getBase64String("");
          console.info("Image's Base64:", base64Str);
        }}
        style={styles.button}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 100,
    paddingHorizontal: 24,
  },
  view: {
    width: "100%",
    display: "flex",
    flexDirection: "row",
    justifyContent: "space-evenly",
    flexWrap: "wrap",
    margin: 50,
  },
  button: {
    matiginVertical: 10, // 垂直间距
  },
  buttonSpacing: {
    height: 20,
    width: "100%",
  },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-base64": "file:../../node_modules/@react-native-oh-tpl/react-native-image-base64/harmony/ImageBase64.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 引入 RNImageBase64Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNImageBase64Package } from "@react-native-oh-tpl/react-native-image-base64/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageBase64Package(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.27; SDK: HarmonyOS-NEXT-DB1(api12) 5.0.0.22; IDE: DevEco Studio 5.0.3.300SP2;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                                                   | Type     | Required | Platform | HarmonyOS Support |
| ------------------- | ----------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| getBase64String     | Retrieve the base64 encoding of the specified image. Return a string type.    | function | no       | All      | yes               |
| getPixelMapFromURL  | Convert network images to PixelMap format.                                    | function | no       | All      | yes               |
| getPixelMapFromFile | Convert local images to PixelMap format.                                      | function | no       | All      | yes               |
| pixelMapToBase64    | Convert PixelMap format images to their corresponding base64 encoding format. | function | no       | All      | yes               |

## 遗留问题


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/SnappFr/react-native-image-base64/blob/master/LICENSE.md) ，请自由地享受和参与开源。

<!-- {% endraw %} -->