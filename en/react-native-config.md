> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-config)

## Basic Usage

在 React Native 应用程序的根目录中创建一个新`.env`文件

```bash
API_URL=https://myapi.com
GOOGLE_MAPS_API_KEY=abcdefgh
```

然后从您的应用程序访问那里定义的变量:

```bash
import Config from "react-native-config";

Config.API_URL; // 'https://myapi.com'
Config.GOOGLE_MAPS_API_KEY; // 'abcdefgh'
```

请记住，此模块不会混淆或加密机密以进行打包，因此请勿将敏感密钥存储在`.env`中[基本上不可能阻止用户对移动应用程序机密进行逆向工程](https://rammic.github.io/2015/07/28/hiding-secrets-in-android-apps/)，因此请在设计应用程序（和 API）时牢记这一点。

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-library/react-native-config Releases](https://github.com/react-native-oh-library/react-native-config/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### npm

```bash
npm install @react-native-oh-tpl/react-native-config@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-config@file:#
```

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

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

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-config": "file:../config"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

### 3. Introducing RNConfigPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

### 多环境

将不同环境的配置保存在不同的文件中: `.env.staging`，`.env.production`等等。
默认情况下，`react-native-config `将从`.env`中读取。最简单的方法是用环境变量告诉它读取什么文件，以命令行中使用 IDE 下的`hvigor.js`的方式（不推荐）。

例如在`CMD`窗口下

首先从 RN 工程根目录 `cd harmony` 进入 harmony 目录

然后先停止守护进程:

```bash
"D:\DevEcoStudio\tools\node\node.exe" "D:\DevEcoStudio\tools\hvigor\bin\hvigorw.js" --stop-daemon-all
```

\*注意，命令中`node.exe`与`hvigor.js`路径为`DevEco Studio`安装目录下的`tools`目录下，需根据实际情况更改。

然后设置环境变量`ENVFILE`为想要指定的配置文件名（注意: 文件名后不要加空格），并用`hvigor.js`构建工程，例如:

```bash
set ENVFILE=.env.staging&&"D:\DevEcoStudio\tools\node\node.exe" "D:\DevEcoStudio\tools\hvigor\bin\hvigorw.js"  --mode module -p module=entry@default -p product=default -p requiredDeviceType=phone assembleHap --analyze=normal --parallel --increm
```

之后可打开`DevEco Studio`构建运行，但此时为保证所设环境变量与工程构建在同一进程，不可在`DevEco Studio`的终端中以 hvigor 命令构建工程。

#### 建立映射

或者，您可以定义一个映射来将构建与环境文件关联起来，可以在`harmony`工程根目录的`build-profile.json5`中的`products`中的`buildOption`节点下的`arkOptions`子节点中通过增加`buildProfileFields`字段配置映射，字段中以键值对的方式配置，其中 key 值为小写的工程构建类型，value 为该构建类型下所要读取的文件名

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

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-config Releases](https://github.com/react-native-oh-library/react-native-config/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name   | Description                                   | Type   | Required | Platform    | HarmonyOS Support |
| ------ | --------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| Config | 类中属性名及其值对应.env 文件中所定义的键值对 | Object | no       | Android/iOS | yes               |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lugg/react-native-config/blob/master/LICENSE).
