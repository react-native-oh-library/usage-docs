> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-get-random-values</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/LinusU/react-native-get-random-values">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/LinusU/react-native-get-random-values/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-get-random-values)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-get-random-values](https://github.com/react-native-oh-library/react-native-get-random-values/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-get-random-values
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-get-random-values
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text, StyleSheet, Button } from "react-native";
import "react-native-get-random-values";

export const GetRandomValues = () => {
  const [randomValue, setRandomValue] = useState < any > [];
  const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: "center",
      alignItems: "center",
      backgroundColor: "#F5FCFF",
    },
  });

  const clickBtn = () => {
    const getRandomValues = global?.crypto?.getRandomValues(new Uint8Array(4));
    console.log(JSON.stringify(getRandomValues), "click");

    const array = Object.values(getRandomValues);
    console.log(array, "click");

    setRandomValue(array);
  };
  return (
    <View style={styles.container}>
      <Text style={{ fontSize: 20 }}> 点击获取随机数 </Text>
      <Button onPress={clickBtn} title="click" />
      {randomValue?.map((item: any, index: number) => {
        return <Text key={index}>{item}</Text>;
      })}
    </View>
  );
};
```

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
    "@react-native-oh-tpl/react-native-get-random-values": "file:../../node_modules/@react-native-oh-tpl/react-native-get-random-values/harmony/get_random_values.har"
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

### 3.在 ArkTs 侧引入 RNGetRandomValuesPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNGetRandomValuesPackage } from "@react-native-oh-tpl/react-native-get-random-values/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNGetRandomValuesPackage(ctx)
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

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Preview2; IDE: DevEco Studio 4.1.3.700; ROM: 3.0.0.19;

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。
>
> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。
>
> | Name                          | Description                                          | Type    | Required | Platform    | HarmonyOS Support |
> | ----------------------------- | ---------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
> | global.crypto.getRandomValues | lets you get cryptographically strong random values. | funtion | no       | IOS/Android | yes               |

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/LinusU/react-native-get-random-values/blob/master/LICENSE) ，请自由地享受和参与开源。
