> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-restart</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/avishayil/react-native-restart">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/avishayil/react-native-restart/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-restart)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-restart Releases](https://github.com/react-native-oh-library/react-native-restart/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-restart@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-restart@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { Button, Text, View, Alert } from "react-native";
import RNRestart from "react-native-restart";

export default function RestartDemo() {
  return (
    <View>
      <Text>重启restart</Text>
      <Button title="重启(restart)" onPress={() => RNRestart.restart()} />
      <Text>重启Restart</Text>
      <Button title="重启(Restart)" onPress={() => RNRestart.Restart()} />
    </View>
  );
}
```

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
   	"@react-native-oh-tpl/react-native-restart": "file:../../node_modules/@react-native-oh-tpl/react-native-restart/harmony/restart.har",
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/link-source-code.md)

### 在 ArkTs 侧引入 RNRestartPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type { RNPackageContext, RNPackage } from "rnoh/ts";
import { SamplePackage } from "rnoh-sample-package/ts";
+ import { RNRestartPackage } from '@react-native-oh-tpl/react-native-restart/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
      new SamplePackage(ctx), 
+     new RNRestartPackage(ctx)
  ];
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-restart Releases](https://github.com/react-native-oh-library/react-native-restart/releases)

本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1 B.0.18； IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description         | Type     | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------- | -------- | -------- | -------- | ----------------- |
| restart: () => void | To Restart Your App | Function | No       | All      | YES               |
| Restart: () => void | To Restart Your App | Function | No       | All      | YES               |

## 遗留问题

## 其他

 HarmonyOS 提供的重启方案每隔10s只能调用一次，所以10s内只能调用react-native-restart的`restart`重启一次，期间多次重复调用会抛出error`{ code: 16000064, message: 'Restart too frequently. Try again at least 10s later.' }`。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/avishayil/react-native-restart/blob/master/LICENSE)，请自由地享受和参与开源。
