> 模板版本：v0.1.3

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

>  [Github 地址](https://github.com/react-native-oh-library/react-native-image-editor)

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
import ImageEditor from '@react-native-community/image-editor';

ImageEditor.cropImage(uri, cropData).then((result) => {
  console.log('Cropped image uri:', result);
});
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

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

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/image-editor": "file:../../node_modules/@react-native-oh-tpl/image-editor/harmony/image_editor"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```



### 在 ArkTs 侧引入 ImageEditorPackage

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

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：[react-native-image-editor.md](react-native-image-editor.md)

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

本文档内容基于以下版本验证通过：

RNOH：0.72.20; SDK：HarmonyOS-NEXT-DB1; IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.13;

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[Releases](https://github.com/react-native-oh-library/react-native-image-editor/releases)

## API

| Name      | Description                                                  | Platform    | HarmonyOS Support |
| --------- | ------------------------------------------------------------ | ----------- | ----------------- |
| cropImage | Crop the image specified by the URI param. If URI points to a remote image, it will be downloaded automatically. If the image cannot be loaded/downloaded, the promise will be rejected.<br/><br/>If the cropping process is successful, the resultant cropped image will be stored in the cache path, and the CropResult returned in the promise will point to the image in the cache path. ⚠️ Remember to delete the cropped image from the cache path when you are done with it. | ios/Android | yes               |

cropData

| 名称          | 类型                              | 说明                                                         | 是否必填 | 原库平台 | 鸿蒙支持 |
| ------------- | --------------------------------- | ------------------------------------------------------------ | -------- | -------- | -------- |
| `offset`      | { x: number, y: number }          | The top-left corner of the cropped image, specified in the original image's coordinate space | yes      | All      | yes      |
| `size`        | { width: number, height: number } | Size (dimensions) of the cropped image                       | yes      | All      | yes      |
| `displaySize` | { width: number, height: number } | Size to which you want to scale the cropped image            | no       | All      | yes      |
| `resizeMode`  | 'contain' \| 'cover' \| 'stretch' | Resizing mode to use when scaling the image**Default value**: `'cover'` | no       | All      | yes      |
| `quality`     | number                            | A value in range `0.0` - `1.0` specifying compression level of the result image. `1` means no compression (highest quality) and `0` the highest compression (lowest quality)<br/>**Default value**: `0.9` | no       | All      | yes      |
| `format`      | 'jpeg' \| 'png'  \| 'webp'        | The format of the resulting image.<br/>**Default value**: based on the provided image;<br/>if value determination is not possible, `'jpeg'` will be used as a fallback. | no       | All      | yes      |

## 

## 遗留问题

## 其他

## 开源协议

本项目基于 [ [The MIT License (MIT)]](https://github.com/callstack/react-native-image-editor/blob/master/LICENSE) ，请自由地享受和参与开源。

