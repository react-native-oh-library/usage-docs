> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-screenshot-prevent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/killserver/react-native-screenshot-prevent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/killserver/react-native-screenshot-prevent/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-screenshot-prevent)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-screenshot-prevent Releases](https://github.com/react-native-oh-library/react-native-screenshot-prevent/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-screenshot-prevent@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-screenshot-prevent@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useEffect } from "react";
import { Alert } from "react-native";
import RNScreenshotPrevent, {
  addListener,
} from "react-native-screenshot-prevent";

RNScreenshotPrevent.enabled(true);

RNScreenshotPrevent.enabled(false);

useEffect(() => {
  const subscription = RNScreenshotPrevent.addListener(() => {
    Alert.alert(
      "You have taken a screenshot of the app.This is prohibited due to security reasons."
    );
  });

  return () => {
    subscription.remove();
  };
}, []);
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-screenshot-prevent": "file:../../node_modules/@react-native-oh-tpl/react-native-screenshot-prevent/harmony/react_native_screenshot_prevent.har"
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

### 在 ArkTs 侧引入 RNScreenShotPreventPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNScreenShotPreventPackage } from "@react-native-oh-tpl/react-native-screenshot-prevent/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNScreenShotPreventPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-screenshot-prevent Releases](https://github.com/react-native-oh-library/react-native-screenshot-prevent/releases)

### 权限要求

- 由于此库涉及开启窗口隐私模式，调用对应接口时则需要配置对应的权限，权限需配置在 entry/src/main 目录下 module.json5 文件中。需要打开 `entry/src/main/ets/module.json5`，添加：

```diff
  ...
 "requestPermissions": [
      {
        "name": "ohos.permission.INTERNET"
      },
      {
        "name": "ohos.permission.ACCELEROMETER"
      },
+     {
+        "name": "ohos.permission.PRIVACY_WINDOW"
+     }
    ]
```

## RNScreenshotPrevent

默认导出 RNScreenshotPrevent 对象

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

#### RNScreenshotPrevent 方法

| Name              | Description                                                                                                                                                                        | Type     | Required | Platform    | HarmonyOS Support |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| enabled           | Whether to enable the function of disabling screenshot/screen recording                                                                                                            | function | no       | iOS/Android | yes               |
| addListener       | notifies when user has taken screenshot (yes, after taking) - you can show alert or do some actions                                                                                | function | no       | iOS         | yes               |
| enableSecureView  | creates a hidden secureTextField which prevents Application UI capture on screenshots and allow uses imgUri as the source of the background image (can be both https://, file:///) | function | no       | iOS         | no                |
| disableSecureView | remove a hidden secureTextField which prevents Application UI capture on screenshots                                                                                               | function | no       | iOS         | no                |

## 遗留问题

- [ ] iOS 支持创建隐藏的安全文本字段，防止应用程序 UI 捕获屏幕截图 [issue#3](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/3)
- [ ] iOS 支持创建一个隐藏的安全文本字段，防止应用程序 UI 捕获屏幕截图，并使用 imgUri 作为背景图像的来源（可以是 https://, file:///） [issue#2](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/2)
- [ ] iOS 支持移除隐藏的安全文本字段，允许应用程序 UI 捕获屏幕截图 [issue#1](https://github.com/react-native-oh-library/react-native-screenshot-prevent/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/killserver/react-native-screenshot-prevent/blob/main/LICENSE) ，请自由地享受和参与开源。
