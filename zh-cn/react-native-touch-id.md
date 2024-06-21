<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-touch-id</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/naoufal/react-native-touch-id">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-touch-id)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-touch-id Releases](https://github.com/react-native-oh-library/react-native-touch-id/releases)，并下载适用版本的 tgz 包。


进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-touch-id@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-touch-id@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { Component, useState } from 'react';
import { Alert, View, Button, Text } from 'react-native';
import TouchID from 'react-native-touch-id';

const App = () => {
  const [result, setResult] = useState<string>('')
  return (
     <View>
      <Text style={{ height: 40, backgroundColor: 'white', textAlign: 'center' }}>{result}</Text>
      <Button title='验证是否有指纹权限'
        onPress={() => {
          TouchID.isSupported({ unifiedErrors: false }).then((res: any) => {
            setResult(res)
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
      <Button title='校验指纹'
        onPress={() => {
          TouchID.authenticate().then((res: boolean) => {
            setResult('认证成功')
          }).catch((err: any) => {
            setResult(err.message)
          })
        }}
      ></Button>
    </View>
  )
};

export default App;

```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。
## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides字段

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
    "@react-native-oh-tpl/react-native-touch-id": "file:../../node_modules/@react-native-oh-tpl/react-native-touch-id/harmony/touch_id.har"
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


### 在 ArkTs 侧引入 TouchIdPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { TouchIdPackage } from "@react-native-oh-tpl/react-native-touch-id/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new TouchIdPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-touch-id Releases](https://github.com/react-native-oh-library/react-native-touch-id/releases)


### 权限要求

（填入相关权限配置）

Add the following permissions to their respective files:

In your `module.json5`

```
 "requestPermissions": [
      {
        "name": "ohos.permission.ACCESS_BIOMETRIC"
      }
    ]
```

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| isSupported  | Whether touchid is supported | function  | yes | ios/andriod      | yes |
| authenticate  | Verify touchid | function  | yes | ios/andriod      | yes |
## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### Errors

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Touch ID Error  | Permission verification failed | string  | no | harmonry      | yes |
| Touch ID Error  | Incorrect parameters | string  | no | harmonry      | yes |
| Touch ID Error  | Authentication failed  | string  | no | harmonry  | yes |
| Touch ID Error  | The operation is canceled   | string  | no | harmonry  | yes |
| Touch ID Error  | The operation is time-out | string  | no | harmonry  | yes |
| Touch ID Error  | The authentication type is not supported   | string | no | harmonry  | yes |
| Touch ID Error  | The authentication trust level is not supported | string  | no | harmonry      | yes |
| Touch ID Error  | The authentication task is busy | string  | no | harmonry      | yes |
| Touch ID Error  | The authenticator is locked  | string  | no | harmonry  | yes |
| Touch ID Error  | General operation error   | string  | no | harmonry  | no |
| Touch ID Error  | The authentication type is not supported | string  | no | harmonry  | yes |
| Touch ID Error  | The type of credential has not been enrolled   | string | no | harmonry  | yes |
| Touch ID Error  | The authentication is canceled from widget's navigation button   | string | no | harmonry  | yes |
| Touch ID Error  | Indicates that current authentication failed because of PIN expired   | string | no | harmonry  | yes |
## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/naoufal/react-native-touch-id?tab=readme-ov-file#license) ，请自由地享受和参与开源。

<!-- {% endraw %} -->