> 模板版本：v0.2.2
<p align="center">
  <h1 align="center"> <code>react-native-thumbnail</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/phuochau/react-native-thumbnail">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/phuochau/react-native-thumbnail/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-thumbnail)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-thumbnail Releases](https://github.com/react-native-oh-library/react-native-thumbnail/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-thumbnail
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-thumbnail
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。<br/>
> [!TIP] 本示例依赖 react-native-image-picker 库，参照[@react-native-oh-tpl/react-native-image-picker 文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-image-picker.md)进行引入。
```js
import React from 'react';
import { StyleSheet, Text, View, TouchableOpacity, Image } from 'react-native';
import { launchCamera, launchImageLibrary } from 'react-native-image-picker';
import RNThumbnail from 'react-native-thumbnail';

export default function ThumbnailExample() {
    const [thumbnail, setThumbnail] = React.useState(null);

    const openCamera = async () => {
        try {
            const options = {
                mediaType: 'video',
                saveToPhotos: true,
                includeExtra: false,
                durationLimit: 5,
            };
            console.log('Launching camera with options:', options);
            const result = await launchCamera(options);
            console.log('Camera result:', result);
            if (result.didCancel) {
                console.log('User cancelled camera');
            } else if (result.errorCode === 'permission') {
                console.log('Permission not granted for camera.');
            } else if (result.errorCode === 'camera_unavailable') {
                console.log('Camera not available on device.');
            } else if (result.errorCode === 'others') {
                console.log(`Other error: ${result.errorMessage}`);
            } else {
                // 检查是否成功获取到视频
                if (result && result.assets && result.assets.length > 0) {
                    const asset = result.assets[0];
                    if (asset.type.includes('mp4')) {
                        console.log('Received video from camera. Getting thumbnail.');
                        const thumbnailResult = await RNThumbnail.get(asset.uri);
                        console.log('Thumbnail result:', thumbnailResult);
                        setThumbnail(thumbnailResult.path);
                    } else {
                        console.log('Gallery asset.type:', asset.type);
                    }
                } else {
                    console.log('No video selected or other issue occurred.');
                }
            }
        } catch (error) {
            console.log('Error launching camera: ', error);
        }
    };

    const openGallery = async () => {
        try {
            const options = {
                mediaType: 'video', // 修改为只选择视频
                selectionLimit: 1,
                includeExtra: false,
            };
            console.log('Launching gallery with options:', options);
            const result = await launchImageLibrary(options);
            if (result.didCancel) {
                console.log('User cancelled gallery');
            } else if (result.errorCode === 'permission') {
                console.log('Permission not granted for gallery.');
            } else if (result.errorCode === 'others') {
                console.log(`Other error: ${result.errorMessage}`);
            } else {
                if (result && result.assets && result.assets.length > 0) {
                    const asset = result.assets[0];
                    // Check if type is defined
                    if (asset.type === undefined) {
                        console.log('Asset type is undefined.');
                    }

                    if (asset.type.includes('mp4')) {
                        console.log('Received video from gallery. Getting thumbnail.');
                        const thumbnailResult = await RNThumbnail.get(asset.uri);
                        console.log('Thumbnail result:', thumbnailResult);
                        setThumbnail(thumbnailResult.path);
                    } else {
                        console.log('Gallery asset.type:', asset.type);
                    }
                }
            }
        } catch (error) {
            console.log('Error launching gallery: ', error);
        }
    };

    return (
        <View style={styles.container}>
            <TouchableOpacity onPress={openCamera}>
                <Text>Open Camera1</Text>
            </TouchableOpacity>
            <TouchableOpacity onPress={openGallery}>
                <Text>Open Gallery1</Text>
            </TouchableOpacity>
            {thumbnail? (
                <Image style={{ width: 200, height: 200, borderWidth: 1, borderColor: 'black' }} source={{ isStatic: true, uri: thumbnail }} />
            ) : null}
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        width: '100%',
        height: '100%',
        backgroundColor: '#fff',
        alignItems: 'center',
        justifyContent: 'center',
    },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/codegen.md)。

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
    "@react-native-oh-tpl/react-native-thumbnail": "file:../../node_modules/@react-native-oh-tpl/react-native-thumbnail/harmony/thumbnail.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/link-source-code.md)

### 在 ArkTs 侧引入 RNThumbnailPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import { RNPackageContext, RNPackage } from '@rnoh/react-native-openharmony/ts';
+import { RNThumbnailPackage } from '@react-native-oh-tpl/react-native-thumbnail/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNThumbnailPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[react-native-thumbnail Releases](https://github.com/react-native-oh-library/react-native-thumbnail/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| get  | Generates a thumbnail for a video file. | function | no | All      | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/phuochau/react-native-thumbnail/blob/master/LICENSE) ，请自由地享受和参与开源。
