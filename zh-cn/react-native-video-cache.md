<!-- {% raw %} -->
> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-video-cache</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zhigang1992/react-native-video-cache">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-video-cache)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-video-cache Releases](https://github.com/react-native-oh-library/react-native-video-cache/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-video-cache@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-video-cache@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useEffect, useState } from "react";
import { StyleSheet, Text, View } from "react-native";
import  { convertAsync } from "react-native-video-cache";

export default function App() {
    const url =
        "https://cdn.plyr.io/static/demo/View_From_A_Blue_Moon_Trailer-720p.mp4";
    const [asyncVersion, setAsyncVersion] = useState<string>('');
    useEffect(() => {
        convertAsync(url).then(setAsyncVersion);
    }, [])
    return (
        <View style={styles.container}>
            <Text style={styles.welcome}>☆Original URL☆</Text>
            <Text style={styles.instructions}>{url}</Text>
            <Text style={styles.welcome}>☆Async Proxy URL☆</Text>
            <Text style={styles.instructions}>{asyncVersion}</Text>
        </View>
    );
}

const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: "center",
        alignItems: "center",
        backgroundColor: "#F5FCFF",
        padding: 20
    },
    welcome: {
        fontSize: 20,
        textAlign: "center",
        margin: 10,
    },
    instructions: {
        textAlign: "center",
        color: "#333333",
        marginBottom: 5,
    },
});
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides字段

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/rnoh-video-cache": "file:../../node_modules/@react-native-oh-tpl/react-native-video-cache/harmony/react_native_video_cache.har"
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
    "@react-native-oh-tpl/rnoh-video-cache": "file:../../node_modules/@react-native-oh-tpl/react-native-video-cache/harmony/react_native_video_cache"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 RNVideoCachePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+   import { RNVideoCachePackage } from '@react-native-oh-tpl/rnoh-video-cache/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNVideoCachePackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-video-cache Releases](https://github.com/react-native-oh-library/react-native-video-cache/releases)。

本文档内容基于以下版本验证通过：
1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1(full sdk); IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-video-cache](https://github.com/zhigang1992/react-native-video-cache)

| Name           | Description                                          | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| convertToCache | Return the local proxy cache server URL using sync.  | string | no       | Androis/IOS | no                |
| convertAsync   | Return the local proxy cache server URL using async. | string | no       | Androis/IOS | yes               |

## 其他

## 遗留问题

- [ ] 由于 HarmonyOS 侧原生依赖 HarmonyOS 三方库@ohos/video-cache中HttpProxyCacheServer实例化对象方法getProxyUrl暂为异步方法，导致本库同步方法convertToCache暂无法实现，问题：[issue#1](https://github.com/react-native-oh-library/react-native-video-cache/issues/1)

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。
<!-- {% endraw %} -->