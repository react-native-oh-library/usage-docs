> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-compass-heading</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/firofame/react-native-compass-heading">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/firofame/react-native-compass-heading/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-compass-heading)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-compass-heading Releases](https://github.com/react-native-oh-library/react-native-compass-heading/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-compass-heading@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-compass-heading@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from "react";
import { useState, useEffect } from "react";
import { StyleSheet, View, Text, Button, ScrollView } from "react-native";
import CompassHeading from "react-native-compass-heading";

export function RNCompassHeading() {
  const [heading, setHeading] = useState(0);
  const [accuracy, setAccuracy] = useState(0);

  interface Data {
    heading: number;
    accuracy: number;
  }

  useEffect(() => {
    const degree_update_rate = 3;
    CompassHeading.start(degree_update_rate, (data: Data) => {
      setHeading(data.heading);
      setAccuracy(data.accuracy);
    });
    return () => {
      CompassHeading.stop();
    };
  }, []);

  return (
    <ScrollView>
      <View
        style={{
          width: "100%",
          height: "100%",
          backgroundColor: "white",
          flex: 1,
        }}
      >
        <View style={styles.container}>
          <Text>{"heading: " + heading}</Text>
          <Text>{"headings: " + accuracy}</Text>
        </View>
      </View>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: "#fff",
    alignItems: "center",
    justifyContent: "center",
    height: 400,
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-compass-heading": "file:../../node_modules/@react-native-oh-tpl/react-native-compass-heading/harmony/compass_heading.har"
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

### 3.在 ArkTs 侧引入 RNCompassHeadingPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNCompassHeadingPackage} from '@react-native-oh-tpl/react-native-compass-heading/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNCompassHeadingPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-compass-heading Releases](https://github.com/react-native-oh-library/react-native-compass-heading/releases)

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name  | Description   | Type                                                  | Required | Platform    | HarmonyOS Support |
| ----- | ------------- | ----------------------------------------------------- | -------- | ----------- | ----------------- |
| start | start compass | (degreeUpdateRate: number, callback: CompassCallback) | yes      | Android/iOS | yes               |
| stop  | stop compass  | void                                                  | no       | Android/iOS | yes               |

**start(degree_update_rate,callback)**

| Name               | Description               | Type                                          | Required | Platform    | HarmonyOS Support |
| ------------------ | ------------------------- | --------------------------------------------- | -------- | ----------- | ----------------- |
| degree_update_rate | compass refresh frequency | number                                        | yes      | Android/iOS | yes               |
| callback           | compass callback          | ({heading: number;accuracy: number;}) => void | yes      | Android/iOS | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/firofame/react-native-compass-heading/blob/master/LICENSE) ，请自由地享受和参与开源。
