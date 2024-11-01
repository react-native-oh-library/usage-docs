> 模板版本：V0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/image-editor</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/callstack/react-native-image-editor">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/callstack/react-native-image-editor/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [Github 地址](https://github.com/react-native-oh-library/react-native-image-editor)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/image-editor Releases](https://github.com/react-native-oh-library/react-native-image-editor/releases)，并下载适用版本的 tgz 包。

#### **npm**

```bash
npm install @react-native-oh-tpl/image-editor@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/image-editor@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!TIP] 使用时 import 的库名不变。

```js
import React, { Component } from "react";
import {
  Image,
  ScrollView,
  Text,
  View,
  StyleSheet,
  Button,
  Alert,
  KeyboardAvoidingView,
} from "react-native";

import ImageEditor from "@react-native-community/image-editor";

export interface Props {
  // noop
}

interface Size {
  width: number;
  height: number;
}

interface State {
  photoUri: any;
  photoWidth: number;
  photoHeight: number;
  croppedImageURI: string | null;
  targetSize?: Size;
  cropHorizontal: boolean;
}

export default class ImageEditor extends Component<Props, State> {
  constructor(props: Props) {
    super(props);
    this.state = {
      photoUri: "https://octodex.github.com/images/OctoAsians_dex_Full.png",
      photoWidth: 896,
      photoHeight: 896,
      croppedImageURI: null,
      targetSize: {
        width: 0,
        height: 0,
      },
      cropHorizontal: false,
    };
  }

  _crop = async () => {
    let cropData = {
      offset: { x: 100, y: 100 },
      size: { width: 300, height: 300 },
      quality: 1,
      format: "jpeg",
    };
    if (
      cropData.size.width + cropData.offset.x > this.state.photoWidth ||
      cropData.size.height + cropData.offset.y > this.state.photoHeight
    ) {
      Alert.alert("The cropped size exceeds the original size");
      return;
    }
    const croppedImageURI = await ImageEditor.cropImage(
      this.state.photoUri,
      cropData
    );
    if (croppedImageURI) {
      this.setState({
        croppedImageURI,
        targetSize: {
          width: cropData.size.width,
          height: cropData.size.height,
        },
      });

      if (this.state.targetSize.width >= this.state.targetSize.height) {
        this.setState({
          cropHorizontal: true,
        });
      } else {
        this.setState({
          cropHorizontal: false,
        });
      }
    }
  };

  render() {
    const {
      photoUri,
      photoWidth,
      photoHeight,
      croppedImageURI,
      targetSize,
      cropHorizontal,
    } = this.state;
    return (
      <KeyboardAvoidingView behavior="position">
        <ScrollView>
          <ScrollView style={{ height: photoHeight }} horizontal={true}>
            <Image
              source={{ uri: photoUri }}
              style={{ width: photoWidth, height: photoHeight }}
            />
          </ScrollView>
          {croppedImageURI ? (
            <ScrollView
              style={{ height: targetSize?.height }}
              horizontal={cropHorizontal}
            >
              <Image
                source={{ uri: croppedImageURI }}
                style={{ width: targetSize?.width, height: targetSize?.height }}
              />
            </ScrollView>
          ) : (
            <Text>未生成图片</Text>
          )}
          <View style={styles.button}>
            <Text>{croppedImageURI}</Text>
            <Button title="确定" onPress={() => this._crop()} />
          </View>
        </ScrollView>
      </KeyboardAvoidingView>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
  },
  button: {
    padding: 10,
  },
  flex: {
    display: "flex",
    flexDirection: "row",
    justifyContent: "flex-start",
    alignItems: "center",
  },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/image-editor": "file:../../node_modules/@react-native-oh-tpl/image-editor/harmony/image_editor.har"
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

### 3.在 ArkTs 侧引入 ImageEditorPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ImageEditorPackage} from "@react-native-oh-tpl/image-editor/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageEditorPackage(ctx)
  ];
}
```

### 4.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[Releases](https://github.com/react-native-oh-library/react-native-image-editor/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Type    | Description                                                  | Platform    | HarmonyOS Support |
| --------- | -------- | ------------------------------------------------------------ | ----------- | ----------------- |
| cropImage | function | Crop the image specified by the URI param. If URI points to a remote image, it will be downloaded automatically. If the image cannot be loaded/downloaded, the promise will be rejected.<br/><br/>If the cropping process is successful, the resultant cropped image will be stored in the cache path, and the CropResult returned in the promise will point to the image in the cache path. ⚠️ Remember to delete the cropped image from the cache path when you are done with it. | ios/Android | yes               |

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**cropData**

| Name          | Value                             | Type   | Description                                                                                                                                                                                               | Required | Platform | HarmonyOS Support |
| ------------- | --------------------------------- | ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------------- |
| `offset`      | { x: number, y: number }          | object | The top-left corner of the cropped image, specified in the original image's coordinate space                                                                                                              | yes      | All      | yes               |
| `size`        | { width: number, height: number } | object | Size (dimensions) of the cropped image                                                                                                                                                                    | yes      | All      | yes               |
| `displaySize` | { width: number, height: number } | object | Size to which you want to scale the cropped image                                                                                                                                                         | no       | All      | yes               |
| `resizeMode`  | 'contain' \| 'cover' \| 'stretch' | string | Resizing mode to use when scaling the image**Default value**: `'cover'`                                                                                                                                   | no       | All      | yes               |
| `quality`     | 0.0 - 1.0                         | number | A value in range `0.0` - `1.0` specifying compression level of the result image. `1` means no compression (highest quality) and `0` the highest compression (lowest quality)<br/>**Default value**: `0.9` | no       | All      | yes               |
| `format`      | 'jpeg' \| 'png' \| 'webp'         | string | The format of the resulting image.<br/>**Default value**: based on the provided image;<br/>if value determination is not possible, `'jpeg'` will be used as a fallback.                                   | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [ [The MIT License (MIT)]](https://github.com/callstack/react-native-image-editor/blob/master/LICENSE) ，请自由地享受和参与开源。