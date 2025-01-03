
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-selector</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/prscX/react-native-file-selector">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/prscX/react-native-file-selector/blob/master/README.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-file-selector)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-file-selector Releases](https://github.com/react-native-oh-library/react-native-file-selector/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：


#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-file-selector
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-file-selector
```


下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import FileSelector from 'react-native-file-selector';
import React from 'react';
function App(): React.JSX.Element {
  
  return (
    <FileSelector
      onDone={(path) => {console.log("file selected: " + path);}}
      onCancel={() => {console.log("cancelled");}}
    />)
};
export default App;
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
    "@rnoh/react-native-openharmony" : "file:./react_native_openharmony"
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
    "@rnoh/react-native-openharmony" : "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-file-selector": "file:../../node_modules/@react-native-oh-tpl/react-native-file-selector/harmony/file_selector.har"
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


### 3.在 ArkTs 侧引入 RNFileSelectorPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
import type {RNPackageContext, RNPackage} from '@rnoh/react-native-openharmony/ts';
+import {RNFileSelectorPackage}  from '@react-native-oh-tpl/react-native-file-selector/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+    new RNFileSelectorPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-file-selector Releases](https://github.com/react-native-oh-library/react-native-file-selector/releases)

## 属性

 FileSelector

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| :--- | ----------- | ---- | -------- | -------- | ------------------ |
| filter | Filter to sort the files | string | no | All | yes |
| path | Path of directory | string | no | All | yes |
| onDone | Function called when file is selected | func | no | All | yes |
| onCancel | Function called when file selector is closed without selecting any file | func | no | All | yes |
| title | Title on the toolbar | string | no | Android iOS | no |
| closeMenu | Color of tint | string | no | Android iOS | no |
| hiddenFiles | If true it shows hidden files as well | bool | no | Android | no |
| filterDirectories | Filter should be applied on directories or not | bool | no | Android | no |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Show | present a fileselector  | function  | no | All      | yes |

 Show

```js
Show(filter?: string, path?: string, onDone?: func, onCancel?: func, title?: string, closeMenu?: string, hiddenFiles?: bool, filterDirectories?: bool);
```

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| :--- | ----------- | ---- | -------- | -------- | ------------------ |
| filter | Filter to sort the files | string | no | All | yes |
| path | Path of directory | string | no | All | yes |
| onDone | Function called when file is selected | func | no | All | yes |
| onCancel | Function called when file selector is closed without selecting any file | func | no | All | yes |
| title | Title on the toolbar | string | no | Android iOS | no |
| closeMenu | Color of tint | string | no | Android iOS | no |
| hiddenFiles | If true it shows hidden files as well | bool | no | Android | no |
| filterDirectories | Filter should be applied on directories or not | bool | no | Android | no |

## 遗留问题


- [ ] FileSelector title：harmony暂不支持: [issue#4](https://github.com/react-native-oh-library/react-native-file-selector/issues/4)
- [ ] FileSelector closeMenu：harmony暂不支持: [issue#5](https://github.com/react-native-oh-library/react-native-file-selector/issues/5)
- [ ] FileSelector hiddenFiles：harmony暂不支持: [issue#6](https://github.com/react-native-oh-library/react-native-file-selector/issues/6)
- [ ] FileSelector filterDirectories：harmony暂不支持: [issue#7](https://github.com/react-native-oh-library/react-native-file-selector/issues/7)

- [ ] Show title：harmony暂不支持: [issue#4](https://github.com/react-native-oh-library/react-native-file-selector/issues/4)
- [ ] Show closeMenu：harmony暂不支持: [issue#5](https://github.com/react-native-oh-library/react-native-file-selector/issues/5)
- [ ] Show hiddenFiles：harmony暂不支持: [issue#6](https://github.com/react-native-oh-library/react-native-file-selector/issues/6)
- [ ] Show filterDirectories：harmony暂不支持: [issue#7](https://github.com/react-native-oh-library/react-native-file-selector/issues/7)

## 其他 

## 开源协议

本项目基于 [Apache License 2.0](https://github.com/prscX/react-native-file-selector/blob/master/LICENSE) ，请自由地享受和参与开源。