> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-keep-awake</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/corbt/react-native-keep-awake">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/corbt/react-native-keep-awake/blob/master/LICENCE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>





> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-keep-awake)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-keep-awake Releases](https://github.com/react-native-oh-library/react-native-keep-awake/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-keep-awake
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-keep-awake
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useEffect } from 'react';
import {
  Text,
  Button,
} from 'react-native';

import KeepAwake , { activateKeepAwake,deactivateKeepAwake,useKeepAwake} from 'react-native-keep-awake'

export function KeepAwakeExample() {
    useKeepAwake();

    const handleClick = (buttonId: number) => {
        switch (buttonId) {
            case 1:
                deactivateKeepAwake();
                break;
            case 2:
                activateKeepAwake();
                break;
            case 3:
                deactivateKeepAwake();
                break;
            case 4:
                KeepAwake.activate();
                break;
            case 5:
                KeepAwake.deactivate();
                break;
            default:
                break;
        }
    };

    return (
        <>
          <Text style={{color:"blue"}}>Button 1:hook默认方法开启(常亮),----useKeepAwake(),点击按键1关闭常亮</Text>
          <Button title='Button 1' onPress={() => handleClick(1)} ></Button>

          <Text style={{color:"blue"}}>Button 2:functions方法开启----activateKeepAwake()</Text>
          <Button title='Button 2' onPress={() => handleClick(2)}></Button>

          <Text style={{color:"blue"}}>Button 3:function方法关闭----deactivateKeepAwake()</Text>
          <Button title='Button 3' onPress={() => handleClick(3)}></Button>

          <Text style={{color:"blue"}}>Button 4:老接口方法----KeepAwake.activate()</Text>
          <Button title='Button 4' onPress={() => handleClick(4)}></Button>

          <Text style={{color:"blue"}}>Button 5:老接口方法----KeepAwake.deactivate()</Text>
          <Button title='Button 5' onPress={() => handleClick(5)}></Button>
        </>
      );

}

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
    "@react-native-oh-tpl/react-native-keep-awake": "file:../../node_modules/@react-native-oh-tpl/react-native-keep-awake/harmony/keep_awake.har"
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
    "@react-native-oh-tpl/react-native-keep-awake": "file:../../node_modules/@react-native-oh-tpl/react-native-keep-awake/harmony/keep_awake"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 3.在 ArkTs 侧引入 RNKeepAwakePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNKeepAwakePackage } from "@react-native-oh-tpl/react-native-keep-awake/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNKeepAwakePackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-keep-awake Releases](https://github.com/react-native-oh-library/react-native-keep-awake/releases)

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18、HarmonyOS NEXT Developer Preview0 B.0.60、HarmonyOS NEXT Developer Preview2 B.0.73; IDE：DevEco Studio 5.0.3.200; ROM：2.0.0.18;

## 使用方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] 功能函数形式使用下，新老接口均可使用。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                   | Description             | Required | Platform | HarmonyOS Support |
| ---------------------- |-------------------------| -------- | -------- | ----------------- |
| `<KeepAwake/>`         | 组件形式使用，开启当前屏幕常亮模式   | No     | All      | yes           |
| KeepAwake.activate()   | 功能函数形式使用，开启当前屏幕常亮模式(老接口) | No       | All      | yes               |
| KeepAwake.deactivate() | 功能函数形式使用，开启当前屏幕常亮模式(老接口) | No       | All      | yes               |
| useKeepAwake()         | hooks形式使用               | No       | All      | yes               |
| activateKeepAwake()    | 功能函数形式使用，开启当前屏幕常亮模式(新接口) | No       | All      | yes               |
| deactivateKeepAwake()  | 功能函数形式使用，关闭当前屏幕常亮模式(新接口) | No       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/corbt/react-native-keep-awake/blob/master/LICENCE) ，请自由地享受和参与开源。

