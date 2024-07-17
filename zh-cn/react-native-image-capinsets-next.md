<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-image-capinsets-next</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mayconmesquita/react-native-image-capinsets-next">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-capinsets-next)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-capinsets-next Releases](https://github.com/react-native-oh-library/react-native-image-capinsets-next/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-capinsets-next@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-capinsets-next@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import ImageCapInset from 'react-native-image-capinsets-next';
import React, {useState} from 'react';
import {View, StyleSheet, Text, Switch} from 'react-native';

const YourImage = () => {
  // 以下图片资源可在img文件夹中获取
  const img1 = require('./capinset_bg.png');
  const img2 = require('./capinset_bg2.png');
  const initInset = JSON.stringify({top: 4, right: 3, bottom: 4, left: 12});
  const initInset2 = JSON.stringify({top: 1, right: 1, bottom: 1, left: 5});
  const [currentImg, setCurrentImg] = useState(img1);
  const [currentCapInset, setCurrentCapInset] = useState(JSON.parse(initInset));

  const onChangeUrl = () => {
    const url = currentImg === img1 ? img2 : img1;
    setCurrentImg(url);
  };

  const onChangeInset = () => {
    const inset =
      JSON.stringify(currentCapInset) === initInset ? initInset2 : initInset;
    setCurrentCapInset(JSON.parse(inset));
  };

  return (
    <View style={styles.container}>
      <ImageCapInset
        style={styles.imgStyle}
        source={currentImg}
        capInsets={currentCapInset}>
        <Text>图片内容2</Text>
      </ImageCapInset>
      <View style={styles.switchItem}>
        <Text>切换图片: </Text>
        <Switch
          trackColor={{false: '#767577', true: '#81b0ff'}}
          thumbColor={currentImg === img1 ? '#f5dd4b' : '#f4f3f4'}
          ios_backgroundColor="#3e3e3e"
          onValueChange={onChangeUrl}
          value={currentImg === img1 ? true : false}
        />
      </View>
      <View style={styles.switchItem}>
        <Text>切换Inset: </Text>
        <Switch
          thumbColor={currentCapInset === initInset ? '#f5dd4b' : '#f4f3f4'}
          onValueChange={onChangeInset}
          value={JSON.stringify(currentCapInset) === initInset ? true : false}
        />
      </View>
    </View>
  );
};

const styles = StyleSheet.create({
  container: {
    paddingTop: 50,
    justifyContent: 'center',
    alignItems: 'center',
  },
  imgStyle: {
    width: 200,
    height: 40,
    display: 'flex',
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: 'lightblue',
  },
  switchItem: {
    display: 'flex',
    flexDirection: 'row',
    alignItems: 'center',
  },
});

export default YourImage;
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
    "@react-native-oh-tpl/react-native-image-capinsets-next": "file:../../node_modules/@react-native-oh-tpl/react-native-image-capinsets-next/harmony/rn_image_capinsets.har"
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

### 在 ArkTs 侧引入 RNCImageCapInsets 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { IMAGE_CAP_INSETS, RNCImageCapInsets } from "@react-native-oh-tpl/react-native-image-capinsets-next"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
...
+ if (ctx.componentName === IMAGE_CAP_INSETS) {
+   RNCImageCapInsets({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ IMAGE_CAP_INSETS
  ];
```

### 在 ArkTs 侧引入 xxx Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNCImageCapInsetsPackage } from '@react-native-oh-tpl/react-native-image-capinsets-next/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCImageCapInsetsPackage(ctx)
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-capinsets-next Releases](https://github.com/react-native-oh-library/react-native-image-capinsets-next/releases)


## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| source  | Image source data         | [ImageSource](https://reactnative.cn/docs/next/image#imagesource)  | yes | All      | yes |
| capInsets  | When the image is scaled, the size of the corners specified by the capInsets is fixed without scaling, while the rest of the middle and sides are stretched. This is useful for making variable-size rounded button shadows and other resources         | [Rect](https://reactnative.cn/docs/next/rect)   | no | All      | yes |


## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。


<!-- {% endraw %} -->