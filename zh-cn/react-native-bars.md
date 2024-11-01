>模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-bars</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/zoontek/react-native-bars">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-bars/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>


> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-bars)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-bars Releases](https://github.com/react-native-oh-library/react-native-bars/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-bars@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-bars@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import { Switch, Text, View } from 'react-native';
import { StatusBar } from "react-native-bars"; 

export function BarExample() {

  const [isEnabled, setIsEnabled] = React.useState(false);
  const toggleSwitch = () => setIsEnabled(previousState => !previousState);

  return (
        <View >
          <StatusBar
            barStyle={isEnabled ? "light-content" : "dark-content"}
          />
          <Text style={{ color: "white" }}>关 dark-content/ 开 light-content</Text>
          <Switch
            trackColor={{ false: "#767577", true: "#81b0ff" }}
            thumbColor={isEnabled ? "#f5dd4b" : "#f4f3f4"}
            ios_backgroundColor="#3e3e3e"
            onValueChange={toggleSwitch}
            value={isEnabled}
          />
        </View>
  );
}

```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
  }
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

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
    "@react-native-oh-tpl/react-native-bars": "file:../../node_modules/@react-native-oh-tpl/react-native-bars/harmony/bars.har"
    
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


### 3.在 ArkTs 侧引入 RNBarsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNBarsPackage} from '@react-native-oh-tpl/react-native-bars/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBarsPackage(ctx)
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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-bars Releases](https://github.com/react-native-oh-library/react-native-bars/releases)



## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### StatusBar
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ---- | ------------ |
| barStyle | Status Bar Style     | string  | yes |     all  |       yes|
| animated | Should transition between status bar property changes be animated? (has no effect on Android)     | boolean  | no |     all  |       yes|

### NavigationBar
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ---- | ------------ |
| barStyle | Navigation Bar Style   | string  | yes |     all  |       no|

### SystemBar
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | ---- | ------------ |
| barStyle | System Style     | string  | yes |     all  |       no|
| animated | Should transition between status bar property changes be animated? (has no effect on Android)     | boolean  | no |     all  |       no|

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### StatusBar
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| pushStackEntry  | Add an instance to the heap queue        | StatusBar.pushStackEntry(props)  | no | all      | yes |
| popStackEntry  | Delete an instance from the heap queue         | StatusBar.popStackEntry(entry/*: StatusBarProps*/): void;  | no | all     | yes |
| replaceStackEntry  | Replace an instance of the heap queue         | const entry: StatusBarProps = StatusBar.replaceStackEntry(entry ,props )  | no | all      | yes |

### NavigationBar
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| pushStackEntry  | Add an instance to the heap queue         |NavigationBar.pushStackEntry(props)  | no | all      | no |
| popStackEntry  | Delete an instance from the heap queue        | NavigationBar.popStackEntry(entry/*: NavigationBarProps*/): void;  | no | all      | no |
| replaceStackEntry  | Replace an instance of the heap queue         |const entry: NavigationBarProps = NavigationBar.replaceStackEntry(entry ,props )  | no | all      | no|

## 遗留问题

- [ ] react-native-bars不支持NavigationBar问题: [issue#16](https://github.com/react-native-oh-library/react-native-bars/issues/16)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/zoontek/react-native-bars/blob/main/LICENSE) ，请自由地享受和参与开源。