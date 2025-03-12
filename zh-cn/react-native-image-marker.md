> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-marker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/JimmyDaddy/react-native-image-marker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/JimmyDaddy/react-native-image-marker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-marker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-marker Releases](https://github.com/react-native-oh-library/react-native-image-marker/releases)。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-marker
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-marker
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import Marker, {
    Position, ImageMarkOptions,  TextMarkOptions
  } from 'react-native-image-marker'
import React, { useState } from "react";
import { StyleSheet, ScrollView, Text, View, Button, Image } from "react-native";
import { Colors } from 'react-native/Libraries/NewAppScreen';

export const ImageMarkerText = () => {
    const [texturl, setTextMarkUrl] = useState('');
    const [imageurl,setImageMarkUrl] = useState('');
    const text_options: TextMarkOptions = {
      backgroundImage: { src: 'https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yuekan/xintexing00.jpg' },
      watermarkTexts: [{
        text: 'hello world \n 你好',
        position: {
          position: Position.topLeft,
        },
        style: {
          color: '#FFFF00',
          fontSize: 30,
          fontName: 'Arial',
          rotate: 30,
          textBackgroundStyle: {
            padding: '10% 10%',
            color: '#02B96B',
          },
          shadowStyle: {
            dx: 10,
            dy: 10,
            radius: 10,
            color: '#008F6D',
          },
          strikeThrough: true,
          underline: true,
        },
      }, {
        text: 'hello world \n 你好',
        position: {
          position: Position.center,
        },
        style: {
          color: '#FFFF00',
          fontSize: 30,
          fontName: 'Arial',
          textBackgroundStyle: {
            padding: '10% 10%',
            color: '#0FFF00',
          },
          strikeThrough: true,
          underline: true,
        },
      }],
    }

    const image_options: ImageMarkOptions = {
      backgroundImage: { src: 'https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yuekan/xintexing00.jpg' },
      watermarkImages: [{
        src: 'https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yingyongicon.png',
        rotate:20,
        position: {
          position: Position.topLeft,
        },
      },
      {
        src: 'https://developer.huawei.com/allianceCmsResource/resource/HUAWEI_Developer_VUE/images/yingyongicon.png',
        rotate:50,
        position: {
          position: Position.bottomCenter,
        },
      }
    ],
    }

    const markText = () => {
      Marker.markText(text_options).then((result) => {
        setTextMarkUrl(result)
      }).catch(error => {
        console.log('error', error)
      })
    }
    
    const markImage = () => {
      Marker.markImage(image_options).then((result) => {
        setImageMarkUrl(result)
      }).catch(error => {
        console.log('error', error)
      })
    }
    return (
        <ScrollView style={{flex: 1}}>
          <View style={styles.body}>
              <View style={styles.sectionContainer}>
                <Text style={styles.sectionTitle}>
                  {"image marker"}
                </Text>
                <Button
                  title="Mark image "
                  color="#9a73ef"
                  onPress={markImage}
                />
                <Text style={styles.sectionTitle}>
                  {imageurl}
                </Text>
                <Image resizeMode='contain' source={{ uri: imageurl, width: 300, height: 300 }} />
              </View>
            </View>
            <View style={styles.body}>
              <View style={styles.sectionContainer}>
                <Text style={styles.sectionTitle}>
                  {"image marker"}
                </Text>
                <Button
                  title="mark text "
                  color="#9a73ef"
                  onPress={markText}
                />
                <Text style={styles.sectionTitle}>
                  {texturl}
                </Text>
                <Image resizeMode='contain' source={{ uri: texturl, width: 300, height: 300 }} />
              </View>
            </View>
      </ScrollView>
      );
  }
  const styles = StyleSheet.create({
    body: {
      backgroundColor: Colors.dark,
    },
    sectionContainer: {
      marginTop: 32,
      paddingHorizontal: 24,
    },
    sectionTitle: {
      marginBottom: 30,
      fontSize: 12,
      fontWeight: '600',
      color: Colors.white,
    }
  });
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-marker": "file:../../node_modules/@react-native-oh-tpl/react-native-image-marker/harmony/image_marker.har"
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

### 3.在 ArkTs 侧引入 RNImageMarkerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNImageMarkerPackage} from '@react-native-oh-tpl/react-native-image-marker/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNImageMarkerPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-marker Releases](https://github.com/react-native-oh-library/react-native-image-marker/releases)

### 权限要求

如果用到了网络图片，需要在 entry 目录下的 module.json5 中添加网络信息权限

打开entry/src/main/module.json5，添加：

```js
...
"requestPermissions": [
    {
    "name": "ohos.permission.INTERNET"
    }
]
```
### 字体使用
如果需要使用字体，需要在entry的resources目录下的rawfile/assets/assets/fonts目录下存放使用的字体文件，
如下图：

![alt text](../img/react-natvie-image-marker/fonts.PNG)


##  API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description            | Type     | Required | Platform    | HarmonyOS Support |
| ------- | ---------------------- | -------- | -------- | ----------- | ----------------- |
| markImage   | mark icons on background image  | string | no  | Android/iOS | yes               |
| markText | mark texts on background image | string | no   | Android/iOS | yes               |

##### ImageOptions

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| src  | image src, local image | string | yes      | iOS/Android | yes               |
| scale | image scale `>0`.defaultValue 1 | number | no      | iOS/Android | yes               |
| rotate | rotate image rotate `0-360`.defaultValue 0 | number | no      | iOS/Android | yes               |
| alpha | transparent of image `0 - 1`.defaultValue 1 | number | no      | iOS/Android | yes |

##### ImageFormat

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| png  | iamge type png | string | no      | iOS/Android | yes               |
| jpg | iamge type jpg | string | no      | iOS/Android | yes               |
| base64 | iamge type base64 | string | no      | iOS/Android | yes               |
##### PositionOptions 

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| X  | horizontal coordinate on background image | number / string | no      | iOS/Android | yes |
| Y  | vertical coordinate on background image | number / string | no      | iOS/Android | yes |
| position  | position enum | [Position](#position) | no | iOS/Android | yes |

##### Position 

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| topLeft  | top left on background image |  string | no      | iOS/Android | yes |
| topCenter  | top center on background image | string | no      | iOS/Android | yes |
| topRight  |top right on background image | string | no | iOS/Android | yes |
| bottomLeft  | bottom left on background image | string | no | iOS/Android | yes |
| bottomCenter  | bottom center on background image | string | no | iOS/Android | yes |
| bottomRight  | bottom right on background image| string | no | iOS/Android | yes |
| center  | center on background image | string | no | iOS/Android | yes |
#### markImage
```js
markImage(options: ImageMarkOptions): Promise<string>;
```
##### ImageMarkOptions

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| backgroundImage  | background image options | [ImageOptions](#imageoptions) | yes      | iOS/Android | partially               |
| quality | image quality `0-100`, `100` is best quality. defaultValue 100 | number | no      | iOS/Android | yes               |
| filename | save image name | string | no      | iOS/Android | yes               |
| saveFormat | save image format 'png','jpg','base64',default 'png' | [ImageFormat](#imageformat) | no      | iOS/Android | yes               |
| watermarkImages | watermark images | Array\<[WatermarkImageOptions](#watermarkimageoptions)> | yes      | iOS/Android | yes  |



##### WatermarkImageOptions 

| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| src  | image src, local image | string | yes      | iOS/Android | yes               |
| scale | image scale `>0`.defaultValue 1 | number | no      | iOS/Android | yes               |
| rotate | rotate image rotate `0-360`.defaultValue 0 | number | no      | iOS/Android | yes               |
| alpha | transparent of image `0 - 1`.defaultValue 1 | number | no      | iOS/Android | yes |
| position  | the position of icon on background image | [PositionOptions](#positionoptions) | no      | iOS/Android | yes               |



#### markText

```json
markText(options: TextMarkOptions): Promise<string>;
```
##### TextMarkOptions
| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| backgroundImage | background image options | [ImageOptions](#imageoptions) | yes      | iOS/Android | partially                |
| watermarkTexts      | text options      | Array\<[TextOptions](#textoptions)> | yes      | iOS/Android | yes               |
| quality      | image quality 0-100, 100 is best quality. defaultValue 100 | number | no      | iOS/Android | yes               |
| filename      | save image name          | string | no      | iOS/Android | yes               |
| saveFormat      | save image format 'png','jpg','base64',default 'png'           | [ImageFormat](#imageformat) | no      | iOS/Android | yes               |

##### TextOptions
| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| text | text content | string | yes      | iOS/Android | yes               |
| position      | text position options | [PositionOptions](#positionoptions) | no      | iOS/Android | yes               |
| style      | text style         | [TextStyle](#textstyle) | no      | iOS/Android | yes               |

##### TextStyle

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| color | font color | string | yes      | iOS/Android | yes               |
| fontName      | font name | string | no      | iOS/Android | yes            |
| fontSize      | font size        | number | no      | iOS/Android | yes               |
| shadowStyle | text shadow style | [ShadowLayerStyle](#shadowlayerstyle) | no      | iOS/Android | yes               |
| textBackgroundStyle      | text background style | [TextBackgroundStyle](#textbackgroundstyle)  | no      | iOS/Android | yes               |
| underline      | text underline style        | boolean | no      | iOS/Android | yes               |
| skewX | css italic with degree, you can use italic instead | number | no      | iOS/Android | yes         |
| strikeThrough      | text stroke | boolean | no      | iOS/Android | yes               |
| textAlign      | text align . 'left' / 'center' / 'right'       | string | no      | iOS/Android | yes               |
| italic | text italic | boolean | no      | iOS/Android | yes            |
| bold      | text bold | boolean | no      | iOS/Android | yes               |
| rotate      | rotate text       | number | no      | iOS/Android | yes               |

##### ShadowLayerStyle

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| dx      | shadow offset x       | number | yes      | iOS/Android | yes               |
| dy      | shadow offset y     | number | yes      | iOS/Android | yes               |
| radius      |shadow radius      | number | yes      | iOS/Android | yes               |
| color      | shadow color       | string | yes      | iOS/Android | yes               |

##### TextBackgroundStyle
extends Padding
| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| type      | background type .TextBackgroundType enum      | [TextBackgroundType](#textbackgroundtype) | no      | iOS/Android | yes               |
| color      | background color    | string | yes      | iOS/Android | yes               |
| cornerRadius      |background corner radius     | [CornerRadius](#cornerradius) | no      | iOS/Android | yes               |
| padding      | padding for text background，Up to four values, separated by spaces   | number / string | no      | iOS/Android | yes               |
| paddingLeft      |  padding left for text background  | number / string | no      | iOS/Android | yes               |
| paddingRight      | padding right for text background    | number / string | no      | iOS/Android | yes               |
| paddingTop      | padding top for text background    | number / string | no      | iOS/Android | yes               |
| paddingBottom      | padding bottom for text background   | number / string  | no      | iOS/Android | yes               |
| paddingHorizontal      | padding left and right (horizontal) for text background    | number / string | no      | iOS/Android | yes               |
| paddingVertical      | padding top and bottom (vertical) for text background    | number / string | no      | iOS/Android | yes               |
| paddingX      |padding x, alias of paddingHorizontal    | number / string | no      | iOS/Android | yes               |
| paddingY      | padding y, alias of paddingVertical  | number / string | no      | iOS/Android | yes               |

##### TextBackgroundType

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| stretchX      | background type stretchX     | string | no      | iOS/Android | yes               |
| stretchY      |  background type  stretchY   | string | no      | iOS/Android | yes               |
| none      | background type fit    | string | no      | iOS/Android | yes               |


##### CornerRadius

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| topLeft      | topLeft Radius     | [RadiusValue](#radiusvalue) | no      | iOS/Android | yes               |
| topRight      | topRight Radius   | [RadiusValue](#radiusvalue) | no      | iOS/Android | yes               |
| bottomLeft      |bottomLeft Radius  | [RadiusValue](#radiusvalue) | no      | iOS/Android | yes               |
| bottomRight      |bottomRight Radius   | [RadiusValue](#radiusvalue) | no      | iOS/Android | yes               |
| all      | all Radius    | [RadiusValue](#radiusvalue) | no      | iOS/Android | yes               |

##### RadiusValue

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| x      | radius value for x     | number / string | no      | iOS/Android | yes               |
| y      | radius value for y  | number / string  | no      | iOS/Android | yes               |

## 遗留问题
- [ ] Harmony OS is not support backgroundImage-ImageOptions-alpha feature now: [issue#30](https://github.com/react-native-oh-library/react-native-image-marker/issues/30)
- [x] Harmony OS is not support font name feature now: [issue#7](https://github.com/react-native-oh-library/react-native-image-marker/issues/7) 
- [x] Harmony OS is not support font skewX feature  now: [issue#8](https://github.com/react-native-oh-library/react-native-image-marker/issues/8)
- [x] Harmony OS is not support font italic feature now: [issue#9](https://github.com/react-native-oh-library/react-native-image-marker/issues/9)

## 其他

## 开源协议

本项目基于[The MIT License(MIT)](https://github.com/JimmyDaddy/react-native-image-marker/blob/master/LICENSE) ，请自由地享受和参与开源。



