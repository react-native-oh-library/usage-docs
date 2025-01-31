> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@bam.tech/react-native-image-resizer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bamlab/react-native-image-resizer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bamlab/react-native-image-resizer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-image-resizer)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-image-resizer Releases](https://github.com/react-native-oh-library/react-native-image-resizer/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-image-resizer
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-image-resizer
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useRef, useState } from 'react';
import {
  Alert,
  Image,
  Platform,
  ScrollView,
  StyleSheet,
  Text,
  TextInput,
  TouchableOpacity,
  View,
} from 'react-native';
import ImageResizer from '@bam.tech/react-native-image-resizer';
import type {
  ResizeMode,
  Response,
} from '@bam.tech/react-native-image-resizer';
import { launchImageLibrary } from 'react-native-image-picker';

const modeOptions: { label: string; value: ResizeMode }[] = [
  {
    label: 'contain',
    value: 'contain',
  },
  {
    label: 'cover',
    value: 'cover',
  },
  {
    label: 'stretch',
    value: 'stretch',
  },
];

const onlyScaleDownOptions: { label: string; value: boolean }[] = [
  {
    label: 'true',
    value: true,
  },
  {
    label: 'false',
    value: false,
  },
];

function ImageResizerDemo() {
  const [selectedMode, setMode] = useState<ResizeMode>('contain');
  const [onlyScaleDown, setOnlyScaleDown] = useState(false);
  const [imageUri, setImageUri] = useState<null | string>();
  const [sizeTarget, setSizeTarget] = useState(80);
  const [resizedImage, setResizedImage] = useState<null | Response>();

  const resize = async () => {
    if (!imageUri) return;

    setResizedImage(null);

    try {
      let result = await ImageResizer.createResizedImage(
        imageUri,
        sizeTarget,
        sizeTarget,
        'JPEG',
        100,
        0,
        undefined,
        false,
        {
          mode: selectedMode,
          onlyScaleDown,
        }
      );

      setResizedImage(result);
    } catch (error) {
      Alert.alert('Unable to resize the photo');
    }
  };
  
  const selectImageFromPicker = async () => {
    launchImageLibrary({ mediaType: 'photo' }, (response) => {
      if (!response || !response.assets) return;
      const asset = response.assets[0];
      if (asset) {
        setImageUri(asset.uri);
      }
    });
  };

  return (
    <ScrollView
      style={styles.scrollView}
      contentContainerStyle={styles.container}
    >
      <Text style={styles.welcome}>Image Resizer example</Text>
      <View style={styles.imageSourceButtonContainer}>
        <TouchableOpacity style={styles.button} onPress={selectImageFromPicker}>
          <Text>{'Select an image (react-native-image-picker)'}</Text>
        </TouchableOpacity>
      </View>
     
      <Text style={styles.instructions}>This is the original image:</Text>
      {imageUri ? (
        <Image
          style={styles.image}
          source={{ uri: imageUri }}
          resizeMode="contain"
        />
      ) : null}

      <Text style={styles.instructions}>Resized image:</Text>
      <Text>Mode: </Text>
      <View style={styles.optionContainer}>
        {modeOptions.map((mode) => (
          <TouchableOpacity
            style={styles.buttonOption}
            onPress={() => setMode(mode.value)}
            key={mode.label}
          >
            <Text>{`${mode.label} ${
              selectedMode === mode.value ? '✅' : ''
            }`}</Text>
          </TouchableOpacity>
        ))}
      </View>

      <Text>Only scale down? </Text>
      <View style={styles.optionContainer}>
        {onlyScaleDownOptions.map((scaleDownOption) => (
          <TouchableOpacity
            style={styles.buttonOption}
            onPress={() => setOnlyScaleDown(scaleDownOption.value)}
            key={scaleDownOption.label}
          >
            <Text>{`${scaleDownOption.label} ${
              onlyScaleDown === scaleDownOption.value ? '✅' : ''
            }`}</Text>
          </TouchableOpacity>
        ))}
      </View>

      <Text>Target size: </Text>
      <TextInput
        style={styles.textInput}
        placeholder={sizeTarget.toString()}
        keyboardType="decimal-pad"
        onChangeText={(text) => {
          setSizeTarget(Number(text));
        }}
      />

      <TouchableOpacity style={styles.button} onPress={resize}>
        <Text>Click me to resize the image</Text>
      </TouchableOpacity>
      {resizedImage ? (
        <>
          <Image
            style={styles.image}
            source={{ uri: resizedImage.uri }}
            resizeMode="contain"
          />
          <Text>Width: {resizedImage.width}</Text>
          <Text>Height: {resizedImage.height}</Text>
        </>
      ) : null}
    </ScrollView>
  );
};  
  
const styles = StyleSheet.create({
  scrollView: {
    backgroundColor: '#F5FCFF',
  },
  container: {
    paddingVertical: 100,
    paddingHorizontal: 10,
  },
  imageSourceButtonContainer: {
    marginBottom: 10,
  },
  welcome: {
    fontSize: 20,
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#333333',
    marginBottom: 5,
  },
  image: {
    height: 250,
    marginBottom: 10,
  },
  button: {
    backgroundColor: '#2596be',
    paddingHorizontal: 30,
    paddingVertical: 20,
    borderRadius: 10,
    alignItems: 'center',
  },
  optionContainer: {
    alignSelf: 'stretch',
    flexDirection: 'row',
    justifyContent: 'space-around',
    marginBottom: 10,
  },
  buttonOption: {
    backgroundColor: '#2596be',
    paddingHorizontal: 10,
    paddingVertical: 10,
    borderRadius: 10,
  },
  textInput: {
    height: 40,
    borderColor: 'black',
    borderWidth: 2,
    margin: 10,
    alignSelf: 'stretch',
    textAlign: 'center',
    overflow: 'hidden',
  },
});

export default ImageResizerDemo;    
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-image-resizer": "file:../../node_modules/@react-native-oh-tpl/react-native-image-resizer/harmony/image_resizer.har"
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

### 3.在 ArkTs 侧引入 ImageResizerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {ImageResizerPackage} from '@react-native-oh-tpl/react-native-image-resizer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ImageResizerPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-image-resizer Releases](https://github.com/react-native-oh-library/react-native-image-resizer/releases)


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name               | Description         | Type     | Required | Platform    | HarmonyOS Support |
|--------------------|---------------------|----------|----------|-------------|-------------------|
| createResizedImage | Resize local images | function | No       | Android/iOS | Yes               |

### createResizedImage参数

| Name                 | Description         | Type    | Platform    | HarmonyOS Support |
|----------------------|---------------------|---------|-------------|-------------------|
| path                 | Path of image file, or a base64 encoded image string prefixed with 'data:image/imagetype' where imagetype is jpeg or png. | string  | Android/iOS | Yes               |
| width                | Width to resize to (see mode for more details) | number  | Android/iOS | Yes               |
| height               | Height to resize to (see mode for more details) | number  | Android/iOS | Yes               |
| compressFormat       | Can be either JPEG, PNG or WEBP. | string  | Android/iOS | Yes               |
| quality              | A number between 0 and 100. Used for the JPEG compression. | number  | Android/iOS | Yes               |
| rotation             | Rotation to apply to the image, in degrees. | number  | Android/iOS | Yes               |
| outputPath           | The resized image path. If null, resized image will be stored in cache folder. To set outputPath make sure to add option for rotation too (if no rotation is needed, just set it to 0). | string  | Android/iOS | Yes               |
| keepMeta             | If true, will attempt to preserve all file metadata/exif info, except the orientation value since the resizing also does rotation correction to the original image. Defaults to false, which means all metadata is lost. Note: This can only be true for JPEG images which are loaded from the file system (not Web). | boolean | Android/iOS | Yes               |
| options.mode         | Similar to react-native Image's resizeMode: either contain (the default), cover, or stretch. contain will fit the image within width and height, preserving its ratio. cover preserves the aspect ratio, and makes sure the image is at least width wide or height tall. stretch will resize the image to exactly width and height. | string  | Android/iOS | Yes               |
| options.onlyScaleDown | 	If true, will never enlarge the image, and will only make it smaller. | boolean | Android/iOS | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/bamlab/react-native-image-resizer/blob/master/LICENSE) ，请自由地享受和参与开源。