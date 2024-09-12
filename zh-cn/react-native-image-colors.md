> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-colors</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/osamaqarem/react-native-image-colors">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20web%20|%20harmony%20|%20expo%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/osamaqarem/react-native-image-colors/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-colors)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-colors Releases](https://github.com/react-native-oh-library/react-native-image-colors/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-colors@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-colors@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect, useState } from 'react'
import {
  Platform,
  StyleSheet,
  Text,
  View,
  Image,
  SafeAreaView,
  Button,
} from 'react-native'
import { getColors } from 'react-native-image-colors'

const imgCat = require('./assets/images/cat.jpg')
const yunaUrl = 'https://img0.baidu.com/it/u=1934875822,4119553331&fm=253&fmt=auto&app=138&f=JPEG?w=720&h=480'
const base = 'data:image/jpeg;base64...'

const initialState = {
  colorOne: { value: '', name: '' },
  colorTwo: { value: '', name: '' },
  colorThree: { value: '', name: '' },
  colorFour: { value: '', name: '' },
  rawResult: '',
}

export default function demo() {
  const [colors, setColors] = useState(initialState)
  const fetchColors = async () => {
    const result = await getColors(imgCat, {
      fallback: '#000000',
    })

    switch (result.platform) {
      case 'android':
      case 'web':
        setColors({
          colorOne: { value: result.lightVibrant, name: 'lightVibrant' },
          colorTwo: { value: result.dominant, name: 'dominant' },
          colorThree: { value: result.vibrant, name: 'vibrant' },
          colorFour: { value: result.darkVibrant, name: 'darkVibrant' },
          rawResult: JSON.stringify(result),
        })
        break
      case 'ios':
        setColors({
          colorOne: { value: result.background, name: 'background' },
          colorTwo: { value: result.detail, name: 'detail' },
          colorThree: { value: result.primary, name: 'primary' },
          colorFour: { value: result.secondary, name: 'secondary' },
          rawResult: JSON.stringify(result),
        })
        break
      case 'harmony':
        setColors({
          colorOne: { value: result.mainColor, name: 'mainColor' },
          colorTwo: { value: result.largestProportionColor, name: 'largestProportionColor' },
          colorThree: { value: result.highestSaturationColor, name: 'highestSaturationColor' },
          colorFour: { value: result.averageColor, name: 'averageColor' },
          rawResult: JSON.stringify(result),
        })
        break
      default:
        throw new Error('Unexpected platform')
    }
  }

  return (
    <View style={styles.container}>
      <SafeAreaView style={styles.resultContainer}>
        <Text style={styles.loading}>Result:</Text>
        <Button title='按钮' onPress={() => fetchColors() }></Button>
        <Text style={styles.result}>{colors.rawResult}</Text>
      </SafeAreaView>
      <Image
        resizeMode="contain"
        style={styles.image}
        source={ imgCat }
      />
      <View style={styles.row}>

        <Box name={colors.colorOne.name} value={colors.colorOne.value} />
        <Box name={colors.colorTwo.name} value={colors.colorTwo.value} />
      </View>
      <View style={styles.row}>
        <Box name={colors.colorThree.name} value={colors.colorThree.value} />
        <Box name={colors.colorFour.name} value={colors.colorFour.value} />
      </View>
    </View>
  )
}

interface BoxProps {
  value: string
  name: string
}

const Box = ({ value, name }: BoxProps) => {
  return (
    <View
      style={[
        styles.box,
        {
          backgroundColor: value,
        },
      ]}
    >
      <Text style={styles.colorName}>{name}</Text>
    </View>
  )
}

const styles = StyleSheet.create({
  image: {
    width: '100%',
    height: 250,
  },
  colorName: {
    backgroundColor: 'white',
    padding: 4,
    fontSize: 18,
  },
  box: {
    flex: 1,
    backgroundColor: 'red',
    justifyContent: 'center',
    alignItems: 'center',
  },
  row: {
    flex: 1,
    flexDirection: 'row',
    width: '100%',
  },
  resultContainer: {
    flex: 1,
    padding: 20,
    width: '100%'
  },
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
  loading: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  result: {
    textAlign: 'center',
    color: '#333333',
  },
})
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-colors": "file:../../node_modules/@react-native-oh-tpl/react-native-image-colors/harmony/image_colors.har"
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

### 3.在 ArkTs 侧引入 RNImageColorsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNImageColorsPackage } from "@react-native-oh-tpl/react-native-image-colors/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNImageColorsPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-colors Releases](https://github.com/react-native-oh-library/react-native-image-colors/releases)

## API

### ImageColors.getColors(uri: string, config?: Config): Promise


> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name      | Description                           | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | ----------------- |
| getColors | Fetch prominent colors from an image. | Function | yes      | all      | yes               |


### Uri

A string which can be:

| Name      | Description                           | Type     | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | ----------------- |
| uri |  1. URL: [`https://i.imgur.com/O3XSdU7.jpg`](https://i.imgur.com/O3XSdU7.jpg);<br>2. Local file: const catImg = require('./images/cat.jpg');<br>3. Base64: const catImgBase64 = 'data:image/jpeg;base64,/9j/4Ri...' | string | yes      | all | yes               |

  > The mime type prefix for base64 is required (e.g. data:image/png;base64).

### Config

The config object is optional.

| Name       | Description                                                                                                                                                                                    | Type                                                   | Required                                           | Default     | Supported | HarmonyOS Support |
| -------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------ | ----------- | ------------------- | ----------------- | ----------------- |
| `fallback`     | If a color property couldn't be retrieved, it will default to this hex color string                                                         | `string`                                               | no                                             | `"#000000"` | all              | yes |
| `cache`        | Enables in-memory caching of the result - skip downloading the same image next time.                                                                                                           | `boolean`                                              | no                                            | `false`     | all              | yes |
| `key`          | Unique key to use for the cache entry. The image URI is used as the unique key by default. You should explicitly pass a key if you enable caching and you're using a base64 string as the URI. | `string`                                               | no                                             | `undefined` | all              | yes |
| `headers`      | HTTP headers to be sent along with the GET request to download the image                                                                                                                       | `Record<string, string>`                               | no                             | `undefined` | iOS, Android        | yes |
| `pixelSpacing` | How many pixels to skip when iterating over image pixels. Higher means better performance (**note**: value cannot be lower than 1).                                                            | `number`                                               | no                                             | `5`         | Android             | no |
| `quality`      | Highest implies no downscaling and very good colors.                                                                                                                                           | `'lowest'` <br> `'low'` <br> `'high'` <br> `'highest'` | no | `'low'`     | iOS, Web          | no |

### ImageColorsResult

Every result object contains a respective `platform` key to help narrow down the type.

HarmonyImageColors

| Name                     | Description                                         | Type        | Required | Platform  | HarmonyOS Support |
| ------------------------ | --------------------------------------------------- | ----------- | -------- | --------- | ----------------- |
| `mainColor`              | The main colors of the image.                       | `string`    | no       | harmonyOS | yes               |
| `largestProportionColor` | The color with the highest proportion in the image. | `string`    | no       | harmonyOS | yes               |
| `highestSaturationColor` | The color with the highest saturation in the image. | `string`    | no       | harmonyOS | yes               |
| `averageColor`           | The average color of the image.                     | `string`    | no       | harmonyOS | yes               |
| `platform`               | The platform is HarmonyOS.                | `string` | no       | all | yes               |

### ImageColors.cache

| Name      | Description                           | Type     | Required | Params | Platform | HarmonyOS Support |
| --------- | ------------------------------------- | -------- | -------- | -------- | -------- | ----------------- |
| getItem | Read cache result. | Function | no      | key: string      | all      | yes               |
| setItem | Set a cached result. | Function | no      | key: string, value: ImageColorsResult      | all      | yes               |
| removeItem | Delete a cached result. | Function | no      | key: string      | all      | yes               |
| clear | Clearing the cache. | Function | no      |                  | all      | yes               |


### Notes
- Since the implementation of each platform is different you can get **different color results for each**.
- This module is a wrapper around the [Palette](https://developer.android.com/reference/androidx/palette/graphics/Palette) class on Android, [UIImageColors](https://github.com/jathu/UIImageColors) on iOS and [node-vibrant](https://github.com/Vibrant-Colors/node-vibrant) for the web and [@ohos.effectKit](https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-effectkit-V5) on harmonyOS.


## 遗留问题

- [x] harmonyOS获取颜色值暂时只能得到固定的一种颜色，暂不支持通过传入`pixelSpacing`或`quality`参数来计算获取不同精确度的颜色值。[issue链接](https://github.com/react-native-oh-library/react-native-image-colors/issues/16) 

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/osamaqarem/react-native-image-colors/blob/master/LICENSE) ，请自由地享受和参与开源。
