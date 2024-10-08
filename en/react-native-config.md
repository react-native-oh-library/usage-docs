> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-config</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lugg/react-native-config">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lugg/react-native-config/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-config)
## 基本用法
在 React Native 应用程序的根目录中创建一个新`.env`文件
```bash
API_URL=https://myapi.com
GOOGLE_MAPS_API_KEY=abcdefgh
```
然后从您的应用程序访问那里定义的变量：
```bash
import Config from "react-native-config";

Config.API_URL; // 'https://myapi.com'
Config.GOOGLE_MAPS_API_KEY; // 'abcdefgh'
```
请记住，此模块不会混淆或加密机密以进行打包，因此请勿将敏感密钥存储在`.env`中[基本上不可能阻止用户对移动应用程序机密进行逆向工程](https://rammic.github.io/2015/07/28/hiding-secrets-in-android-apps/)，因此请在设计应用程序（和 API）时牢记这一点。

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-config Releases](https://github.com/react-native-oh-library/react-native-config/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

#### npm

```bash
npm install @react-native-oh-tpl/react-native-config@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-config@file:#
```


下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```
import React, {Component} from 'react';
import {StyleSheet, Text, View} from 'react-native';

import Config from 'react-native-config';

export default class App extends Component {
  render() {
    return (
      <View style={styles.container}>
        <Text style={styles.text}>API_URL={Config.API_URL}</Text>
      </View>
    );
  }
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
  },
  text: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
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

该库仅支持源码形式引入

#### 直接链接源码情况说明

目前 DevEco Studio 不支持通过源码引入外部 module，请按照以下步骤操作，将源码通过操作改成 harmony 工程的内部模块。

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

把`<RN工程>/node_modules/@react-native-oh-tpl/react-native-config/harmony/`目录下的源码`<config>`复制到`harmony`工程根目录下

在`harmony`工程根目录的 `build-profile.template.json5`（若存在）和`build-profile.json5` 添加以下模块

```json
modules:[
  ...
  {
    name: 'config',
    srcPath: './config',
  }
]
```

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-config": "file:../config"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

### 3.在 ArkTs 侧引入 RNConfigPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type { RNPackageContext, RNPackage } from 'rnoh/ts';
  ...
+ import { RNConfigPackage } from '@react-native-oh-tpl/react-native-config/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNConfigPackage(ctx)
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

### 多环境
将不同环境的配置保存在不同的文件中：`.env.staging`，`.env.production`等等。
默认情况下，`react-native-config `将从`.env`中读取。最简单的方法是用环境变量告诉它读取什么文件，以命令行中使用IDE下的`hvigor.js`的方式（不推荐）。

例如在`CMD`窗口下

首先从RN工程根目录 `cd harmony` 进入harmony目录

然后先停止守护进程：

```bash
"D:\DevEcoStudio\tools\node\node.exe" "D:\DevEcoStudio\tools\hvigor\bin\hvigorw.js" --stop-daemon-all
```

*注意，命令中`node.exe`与`hvigor.js`路径为`DevEco Studio`安装目录下的`tools`目录下，需根据实际情况更改。

然后设置环境变量`ENVFILE`为想要指定的配置文件名（注意：文件名后不要加空格），并用`hvigor.js`构建工程，例如：

```bash
set ENVFILE=.env.staging&&"D:\DevEcoStudio\tools\node\node.exe" "D:\DevEcoStudio\tools\hvigor\bin\hvigorw.js"  --mode module -p module=entry@default -p product=default -p requiredDeviceType=phone assembleHap --analyze=normal --parallel --increm
```
之后可打开`DevEco Studio`构建运行，但此时为保证所设环境变量与工程构建在同一进程，不可在`DevEco Studio`的终端中以hvigor命令构建工程。

#### 建立映射

或者，您可以定义一个映射来将构建与环境文件关联起来，可以在`harmony`工程根目录的`build-profile.json5`中的`products`中的`buildOption`节点下的`arkOptions`子节点中通过增加`buildProfileFields`字段配置映射，字段中以键值对的方式配置，其中key值为小写的工程构建类型，value为该构建类型下所要读取的文件名
```json
"products": [
      {
        "name": "default",
        "signingConfig": "default",
        "compatibleSdkVersion": "5.0.0(12)",
        "runtimeOS": "HarmonyOS",
        "buildOption": {
          "arkOptions": {
            "buildProfileFields": {
              "debug": ".env.development",
              "release": ".env.production"
            }
          }
        }
      }
    ]
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-config Releases](https://github.com/react-native-oh-library/react-native-config/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name            | Description                       | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | --------------------------------- | -------- | -------- | ----------- | ----------------- |
| Config    | 类中属性名及其值对应.env文件中所定义的键值对           | Object     | no       | Android/iOS | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lugg/react-native-config/blob/master/LICENSE) ，请自由地享受和参与开源。

