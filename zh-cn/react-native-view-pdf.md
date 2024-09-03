> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-view-pdf</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/rumax/react-native-PDFView">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/rumax/react-native-PDFView/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-PDFView)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-view-pdf Releases](https://github.com/react-native-oh-library/react-native-PDFView/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-view-pdf@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-view-pdf@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View } from "react-native";
import PDFView from "react-native-view-pdf";

export function PdfViewExample() {
  <View style={{ flex: 1 }}>
    <PDFView
      style={{ flex: 1 }}
      resource="https://www.w3.org/WAI/ER/tests/xhtml/testfiles/resources/pdf/dummy.pdf"
      resourceType="url"
      onLoad={() => {}}
      onError={(error: any) => {}}
    ></PDFView>
  </View>;
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-view-pdf": "file:../../node_modules/@react-native-oh-tpl/react-native-view-pdf/harmony/pdf_view.har"
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

### 在 ArkTs 侧引入 RNPDFView 组件

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RNPDFView } from '@react-native-oh-tpl/react-native-view-pdf'

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === RNPDFView.NAME) {
+   RNPDFView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。（如使用混合方案）

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ RNPDFView.NAME
  ];
```

### 在 ArkTs 侧引入 PDFViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { PDFViewPackage } from '@react-native-oh-tpl/react-native-view-pdf/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new PDFViewPackage(ctx)
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

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-view-pdf Releases](https://github.com/react-native-oh-library/react-native-PDFView/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                                                                                                                                                                                                        | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| resource          | A resource to render. It's possible to render PDF from file, url (should be encoded) or base64                                                                                                                                                     | string   | yes      | all      | yes               |
| resourceType      | Should correspond to resource and can be: file, url or base64                                                                                                                                                                                      | string   | no       | all      | yes               |
| fileFrom          | iOS: In case if resourceType is set to file, there are different way to search for it on iOS file system. Currently documentsDirectory, libraryDirectory, cachesDirectory, tempDirectory and bundle are supported. <br>harmony: files, cache, temp | string   | no       | iOS      | yes               |
| onLoad            | Callback that is triggered when loading is completed                                                                                                                                                                                               | function | no       | all      | yes               |
| onError           | Callback that is triggered when loading has failed. And error is provided as a function parameter                                                                                                                                                  | style    | no       | all      | yes               |
| style             | css style                                                                                                                                                                                                                                          | string   | no       | all      | yes               |
| fadeInDuration    | Fade in duration (in ms, defaults to 0.0) to smoothly fade the webview into view when pdf loading is completed                                                                                                                                     | number   | no       | all      | yes               |
| enableAnnotations | Android ONLY: Boolean to enable Android view annotations (default is false).                                                                                                                                                                       | boolean  | no       | Android  | no                |
| urlProps          | Extended properties for url type that allows to specify HTTP Method, HTTP headers and HTTP body                                                                                                                                                    | map      | no       | all      | no                |
| onPageChanged     | Callback that is invoked when page is changed. Provides active page and total pages information                                                                                                                                                    | function | no       | Android  | no                |
| onScrolled        | Callback that is invoked when PDF is scrolled. Provides offset value in a range between 0 and 1. Currently only 0 and 1 are supported.                                                                                                             | function | no       | all      | no                |

### 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description                                                                                                                                                                     | Type     | Required | Platform | HarmonyOS Support |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| reload | Allows to reload the PDF document. This can be useful in such cases as network issues, document is expired, etc. To reload the document you will need a `ref` to the component: | function | yes      | all      | yes               |

## 遗留问题

- [ ] urlProps 属性不支持, HarmonyOS 原生组件 webview 不支持 urlProps。[issue: #5](https://github.com/react-native-oh-library/react-native-PDFView/issues/5)
- [ ] onScrolled 属性不支持, HarmonyOS 原生组件 webview 加载 pdf 文件时 onScrolled 回调函数不执行。 [issue: #6](https://github.com/react-native-oh-library/react-native-PDFView/issues/6)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/rumax/react-native-PDFView/blob/master/LICENSE) ，请自由地享受和参与开源。
