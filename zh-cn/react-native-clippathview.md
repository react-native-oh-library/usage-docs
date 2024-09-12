<!-- {% raw %} -->
> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-clippathview</code> </h1>
</p>
<p align="center">
        <a href="https://github.com/Only-IceSoul/react-native-clippath/blob/main">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/Only-IceSoul/react-native-clippath/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-clippath)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-clippathview Releases](https://github.com/react-native-oh-library/react-native-clippath/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-clippathview@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-clippathview@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

```jsx
import { View, Text, ScrollView } from "react-native";
import React from "react";
import { ClipPathView } from "react-native-clippathview";

export default function index() {
  const viewBox = [0, 0, 400, 400];
  const path = "M 0 0 L 400 0 L 0 400 L 400 400 Z";

  return (
    <ScrollView style={{ width: "100%", height: "100%" }}>
      <ClipPathView d={path} style={{ backgroundColor: "#ff0" }}>
        <Text style={{ height: 800, fontSize: 26 }}>
          MMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMMM
        </Text>
      </ClipPathView>
    </ScrollView>
  );
}
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-clippathview Releases](https://github.com/react-native-oh-library/react-native-clippath/releases)

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

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "@react-native-oh-library/react-native-clippathview": "file:../../node_modules/@react-native-oh-tpl/react-native-clippathview/harmony/clip_path.har",
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

### 3.在 ArkTs 侧引入 ClipPath 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+ import { ClipPath } from '@react-native-oh-library/react-native-clippathview';

@Builder
function buildCustomComponent(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnComponentContext,
      tag: ctx.tag,
      buildCustomComponent: buildCustomComponent
    })
  }
+ else if (ctx.componentName === ClipPath.NAME) {
+   ClipPath({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag,
+   })
+ }
 ...
}
...
```

### 4.在 ArkTs 侧引入 ClipPathPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import { ClipPathPackage } from '@react-native-oh-library/react-native-clippathview/ts'

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ClipPathPackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                                  | Type              | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------ | ----------------- | -------- | ----------- | ----------------- |
| svgKey               | 唯一 key                                                     | string            | No       | iOS/Android | Yes               |
| d                    | 形状由一系列命令定义（svg path data）                        | string            | No       | iOS/Android | Yes               |
| viewBox              | 定义用户空间中的位置和维度                                   | Array<Number>(4)  | No       | iOS/Android | Yes               |
| align                | preserveAspectRatio 属性的 align                             | string            | No       | iOS/Android | No                |
| aspect               | preserveAspectRatio 属性的 meetOrSlice                       | meet/slice/none   | No       | iOS/Android | No                |
| fillRule             | 路径内部填充规则                                             | nonzero/evenodd   | No       | iOS/Android | No                |
| strokeWidth          | 路径描边宽度                                                 | number            | No       | iOS/Android | Yes               |
| strokeCap            | 开放路径两端的形状                                           | butt/round/square | No       | iOS/Android | Yes               |
| strokeJoin           | 路径转角处使用的形状                                         | bevel/miter/round | No       | iOS/Android | Yes               |
| strokeMiter          | strokeJoin 值是 miter，设置夹角延伸                          | number            | No       | iOS/Android | Yes               |
| strokeStart          | iOS CAShapeLayer 描线开始的地方占总路径的百分比。默认值是 0。 | number            | No       | iOS/Android | No                |
| strokeEnd            | iOS CAShapeLayer 表示绘制结束的地方站总路径的百分比。默认值是 1，如果小于等于 strokeStart 则绘制不出任何内容。 | number            | No       | iOS/Android | No                |
| translateZ           | 设置定位层级，相当于 index                                   | number            | No       | iOS/Android | Yes               |
| transX               | 在二维平面上水平方向移动元素                                 | number            | No       | iOS/Android | Yes               |
| transY               | 在二维平面上垂直方向移动元素                                 | number            | No       | iOS/Android | Yes               |
| transPercentageValue | transX、transY 使用百分比                                    | boolean           | No       | iOS/Android | Yes               |
| rot                  | 元素围绕一个定点旋转                                         | number            | No       | iOS/Android | Yes               |
| rotOx                | 旋转中心点水平位置                                           | number            | No       | iOS/Android | Yes               |
| rotOy                | 旋转中心点垂直位置                                           | number            | No       | iOS/Android | Yes               |
| rotPercentageValue   | rotOx、rotOy 使用百分比                                      | boolean           | No       | iOS/Android | Yes               |
| sc                   | 放大或缩小元素                                               | number            | No       | iOS/Android | Yes               |
| scX                  | 水平缩放                                                     | number            | No       | iOS/Android | Yes               |
| scY                  | 垂直缩放                                                     | number            | No       | iOS/Android | Yes               |
| scO                  | 缩放中心点位置                                               | number            | No       | iOS/Android | Yes               |
| scOx                 | 缩放中心点水平位置                                           | number            | No       | iOS/Android | Yes               |
| scOy                 | 缩放中心点垂直位置                                           | number            | No       | iOS/Android | Yes               |
| scPercentageValue    | scO、scOx、scOy 使用百分比                                   | boolean           | No       | iOS/Android | Yes               |

## 遗留问题

- [ ] 部分属性目前版本暂不支持，具体参考属性表格 `HarmonyOS ` 列: [issue#15](https://github.com/react-native-oh-library/react-native-clippath/issues/15)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/Only-IceSoul/react-native-clippath/blob/main/LICENSE) ，请自由地享受和参与开源。

---

<!-- {% endraw %} -->