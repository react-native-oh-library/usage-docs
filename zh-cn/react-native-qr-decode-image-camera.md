> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-qr-decode-image-camera</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-qr-decode-image-camera Releases](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-qr-decode-image-camera@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-qr-decode-image-camera@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> 示例中：launchImageLibrary 方法需引入 Harmony OS 的 react-native-image-picker 库，跳转 [react-native-image-picker](/zh-cn/react-native-image-picker.md)查看使用方法。

QRreader

```js
import React, {useState} from 'react';
import {Button, View, Text} from 'react-native';
import {QRreader} from 'react-native-qr-decode-image-camera';
import {launchImageLibrary} from 'react-native-image-picker';

export const qrExample = () => {
  const [reader, setReader] = useState<any>('');
  return (
    <View style={{flex: 1, justifyContent: 'center', alignItems: 'center'}}>
      <Button
        onPress={() => {
          launchImageLibrary({mediaType: 'photo', selectionLimit: 1}, data => {
            if (data.assets?.length) {
              const path = {
                uri: data.assets[0].originalPath,
              };
              QRreader(path)
                .then(res => {
                  setReader(res?.[0]?.originalValue);
                })
                .catch(error => {
                  console.log(error);
                });
            }
          });
        }}
        title="点击选择二维码照片 "
      />
      <Text style={{fontSize: 20}}>{reader}</Text>
    </View>
  );
};
```
QRscanner

```json
import React, {useState} from 'react';
import { View, Text, TouchableOpacity, StyleSheet} from 'react-native';
import { QRscanner} from 'react-native-qr-decode-image-camera';


export const qrExample = () => {

  const [flashMode, setflashMode] = useState(false);
  const onRead = res => {
    console.log(res);
  };
  return (
    <View style={styles.container}>
      <QRscanner
        onRead={onRead}
        renderBottomView={() => {
          return (
            <View
              style={{
                flex: 1,
                flexDirection: 'row',
                backgroundColor: '#0000004D',
              }}>
              <TouchableOpacity
                style={{
                  flex: 1,
                  alignItems: 'center',
                  justifyContent: 'center',
                }}
                onPress={() => {
                  if (flashMode) {
                    setflashMode(false);
                  } else {
                    setflashMode(true);
                  }
                }}>
                <Text style={{color: '#fff'}}>flashMode</Text>
              </TouchableOpacity>
            </View>
          );
        }}
        flashMode={flashMode}
        finderY={50}
      />
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#000',
  },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

本库鸿蒙侧实现依赖@react-native-oh-tpl/react-native-vision-camera 的原生端代码，如已在鸿蒙工程中引入过该库，则无需再次引入，可跳过本章节步骤，直接使用。

如未引入请参照[@react-native-oh-tpl/react-native-vision-camera](/zh-cn/react-native-vision-camera.md)进行引入

## 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-qr-decode-image-camera": "file:../../node_modules/@react-native-oh-tpl/react-native-qr-decode-image-camera/harmony/qr_decode_image_camera.har"
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

### 3.在 ArkTs 侧引入 RNQrDecodeImageCameraPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：


```diff
  ...
+ import {RNQrDecodeImageCameraPackage} from '@react-native-oh-tpl/react-native-qr-decode-image-camera/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNQrDecodeImageCameraPackage(ctx)
  ];
}
```

### 4.在 ArkTs 侧引入 Fabric 组件

找到 function buildCustomRNComponent()，一般位于 entry/src/main/ets/pages/index.ets 或 entry/src/main/ets/rn/LoadBundle.ets，添加：

```diff
  ...
+ import { NativeScan } from "@react-native-oh-tpl/react-native-qr-decode-image-camera"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === NativeScan.NAME) {
+   NativeScan({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

### 5.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-qr-decode-image-camera](https://github.com/react-native-oh-library/react-native-qr-decode-image-camera/releases)


## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

 | Name | Description | Type | Required | Platform | HarmonyOS Support |
 | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
 | QRreader | Invoke this method to invoke the gallery, select the QR code image for image decoding, and asynchronously return the result. | funtion | no | iOS/Android | yes |

## 属性

### QRscanner

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description                                      | Type    | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------------------------------ | ------- | -------- | ----------- | ----------------- |
| isRepeatScan       | whether to allow repeated scanning               | boolean | no       | iOS/Android | yes               |
| zoom               | Camera focal length range 0-1                    | number  | no       | iOS/Android | no                |
| flashMode          | Turn on the flashlight                           | boolean | no       | iOS/Android | yes               |
| onRead             | scan callback                                    | funtion | yes      | iOS/Android | yes               |
| maskColor          | mask layer color                                 | string  | no       | iOS/Android | yes               |
| borderColor        | border color                                     | string  | no       | iOS/Android | yes               |
| cornerColor        | Color of corner of scan frame                    | string  | no       | iOS/Android | yes               |
| borderWidth        | border width of scan frame                       | number  | no       | iOS/Android | yes               |
| cornerBorderWidth  | border width of scan frame corner                | number  | no       | iOS/Android | yes               |
| cornerBorderLength | width and height of the corner of the scan frame | number  | no       | iOS/Android | yes               |
| rectHeight         | Scan frame height                                | number  | no       | iOS/Android | yes               |
| rectWidth          | Scan Frame Width                                 | number  | no       | iOS/Android | yes               |
| finderX            | scan frame X axis offset                         | number  | no       | iOS/Android | yes               |
| finderY            | scan frame Y axis offset                         | number  | no       | iOS/Android | yes               |
| isCornerOffset     | whether the corners are offset                   | boolean | no       | iOS/Android | yes               |
| cornerOffsetSize   | offset                                           | number  | no       | iOS/Android | yes               |
| bottomHeight       | Reserved height at the bottom                    | number  | no       | iOS/Android | yes               |
| scanBarAnimateTime | scan line time                                   | number  | no       | iOS/Android | yes               |
| scanBarColor       | scan line color                                  | string  | no       | iOS/Android | yes               |
| scanBarImage       | scan line image                                  | any     | no       | iOS/Android | yes               |
| scanBarHeight      | scan line height                                 | number  | no       | iOS/Android | yes               |
| scanBarMargin      | scanline left and right margin                   | number  | no       | IOS/Android | yes               |
| hintText           | hintText                                         | string  | no       | IOS/Android | yes               |
| hintTextStyle      | hint string style                                | object  | no       | iOS/Android | yes               |
| hintTextPosition   | hintTextPosition                                 | number  | no       | iOS/Android | yes               |
| renderTopView      | render top View                                  | funtion | no       | iOS/Android | yes               |
| renderBottomView   | render bottom View                               | funtion | no       | iOS/Android | yes               |
| isShowScanBar      | whether to show scan lines                       | boolean | no       | iOS/Android | yes               |
| topViewStyle       | render top container style                       | object  | no       | iOS/Android | yes               |
| bottomViewStyle    | render bottom container style                    | object  | no       | iOS/Android | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/deepanrajkumar/react-native-qr-decode-image-camera/blob/master/LICENSE) ，请自由地享受和参与开源。
