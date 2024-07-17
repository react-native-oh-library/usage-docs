<!--{%raw%}-->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@remobile/react-native-toast</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/remobile/react-native-toast">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/remobile/react-native-toast/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-toast)

## 安装与使用

请到三方库的 Releases
发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-toast Releases](https://github.com/react-native-oh-library/react-native-toast/releases)，并下载适用版本的tgz包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-toast@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-toast@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, {Component} from 'react';
import {Text, View, Button} from 'react-native';
import Toast from '@remobile/react-native-toast';

function ToastMasterDemo() {
    return (
        <View style={{flex: 2, justifyContent: 'center', alignItems: 'center'}}>
            <Text>Tosat !</Text>
            <Button
                title={'show toast'}
                onPress={() => {
                    Toast.show('This is a toast.');
                }}
            />
            <Button
                title={'short top toast'}
                onPress={() => {
                    Toast.showShortTop('This is a top toast.');
                }}
            />
            <Button
                title={'short center toast'}
                onPress={() => {
                    Toast.showShortCenter('This is a center toast.');
                }}
            />
            <Button
                title={'short bottom toast'}
                onPress={() => {
                    Toast.showShortBottom('This is a bottom toast.');
                }}
            />
            <Button
                title={'long top toast'}
                onPress={() => {
                    Toast.showLongTop('This is a long top toast.');
                }}
            />
            <Button
                title={'long center toast'}
                onPress={() => {
                    Toast.showLongCenter('This is a long center toast.');
                }}
            />
            <Button
                title={'long bottom toast'}
                onPress={() => {
                    Toast.showLongBottom('This is a long bottom toast.');
                }}
            />
            <Button
                title={'hide'}
                onPress={() => {
                    Toast.hide();
                }}
            />
        </View>
    );
}

export default ToastMasterDemo;

```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前HarmonyOS暂不支持 AutoLink，所以Link步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
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
"@react-native-oh-tpl/react-native-toast": "file:../../node_modules/@react-native-oh-tpl/react-native-toast/harmony/rn_toast.har"
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

### 在 ArkTs 侧引入 ToastPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {ToastPackage} from '@react-native-oh-tpl/react-native-toast/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ToastPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release
配套的版本信息：[@react-native-oh-tpl/react-native-toast Releases](https://github.com/react-native-oh-library/react-native-toast/releases)


## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| show()  | Displays the location of the toast, its duration, the content of the message | function  | yes | android      | yes |
| showShortTop()  | Display the top Toast for a short time | function  | yes | android      | yes |
| showShortCenter()  | Display the center Toast for a short time | function  | yes | android      | yes |
| showShortBottom()  | Display the bottom Toast for a short time | function  | yes | android      | yes |
| showLongTop()  | Display the top Toast for a long time | function  | yes | android      | yes |
| showLongCenter()  | Display the center Toast for a long time | function  | yes | android      | yes |
| showLongBottom()  | Display the bottom Toast for a long time | function  | yes | android      | yes |
| hide()  | Hide the toast that is being displayed         | function  | yes | android      | no |

## 遗留问题

- arkui侧的toast的hide()方法暂时没有[issue#3](https://github.com/react-native-oh-library/react-native-toast/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License](https://github.com/remobile/react-native-toast/blob/master/LICENSE)，请自由地享受和参与开源。

<!--{%endraw%}-->
