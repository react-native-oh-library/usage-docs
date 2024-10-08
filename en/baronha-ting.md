> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@baronha/ting</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/<原库源码仓地址>">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/baronha/ting/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/ting)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/ting Releases](https://github.com/react-native-oh-library/ting/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/ting@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/ting@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View } from "react-native";
import {
    ToastOptions,
    toast
} from '@baronha/ting';

function handleToast(options: ToastOptions) {
    toast(options);
}

const App = () => {
  return (
    <View>
        <Button
            title="defalut"
            onPress={() => {
                const options: ToastOptions = {
                    title: 'title-Toast',
                    message: 'message-Toast',
                };
                handleToast(options);
            }}
        />
    </View>
};

export default App;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[Codegen 使用文档](/zh-cn/codegen.md)。

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/ting": "file:../../node_modules/@react-native-oh-tpl/ting/harmony/ting.har"
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

### 3.在 ArkTs 侧引入 RNTingPackage

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
  ...
+ import {RNTingPackage} from '@react-native-oh-tpl/ting';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNTingPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/ting Releases](https://github.com/react-native-oh-library/ting/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### ToastOptions

| Name                 | Description                                             | Type | Required | Platform | HarmonyOS Support   |
|----------------------|---------------------------------------------------------|------|----------|----------|---------------------|
| title                | The text for the toast’s title                                       | string   | no        | All      | yes  |
| message              | The text for the toast’s message                                     | string   | no        | All      | yes  |
| titleColor           | The color of the title text in hexadecimal format      | string   | no        | All      | yes  |
| messageColor         | The color of the message text in hexadecimal format    | string   | no        | All      | yes  |
| preset               |  The preset style of the toast. Options include done (success), error (error), none (no style), or spinner (loading spinner)                                                    | string  | no        | All      | partially |
| duration             | The lifetime of the toast (seconds)                    | number  | no         | All      | yes  |
| haptic               | The type of haptic feedback. Options include success (success), warning (warning), error (error), or none (no haptic feedback)                                                     | string  | no         | iOS      | yes                 |
| shouldDismissByDrag  | Whether the toast can be dismissed by dragging                                                     | boolean  | no        | All      | yes  |
| position             | Toast is displayed from top or bottom                  | string   | no         | All      |yes                 |
| backgroundColor      | The background color of the toast in hexadecimal format| string   | no         | All      |yes       |
| icon                 | A custom icon for the toast                                                     | object  | no        | All      | yes  |
| progressColor        | The color of the progress spinner for the spinner preset style                                                     | string  | no        | Android   | yes  |

### AlertOptions

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| title                | The text for the toast’s title                                       | string   | no        | All      | yes  |
| message              | The text for the toast’s message                                     | string   | no        | All      | yes  |
| titleColor           | The color of the title text in hexadecimal format      | string   | no        | All      | yes  |
| messageColor         | The color of the message text in hexadecimal format    | string   | no        | All      | yes  |
| preset               |  The preset style of the toast. Options include done (success), error (error), none (no style), or spinner (loading spinner)                                                    | string  | no        | All      | partially |
| duration             | The lifetime of the toast (seconds)                    | number  | no         | All      | yes  |
| haptic               | The type of haptic feedback. Options include success (success), warning (warning), error (error), or none (no haptic feedback)                                                     | string  | no         | iOS      | yes                 |
| shouldDismissByTap  | Whether the toast can be dismissed by tapping                                                     | boolean  | no        | All      | yes  |
| backgroundColor      | The background color of the toast in hexadecimal format| string   | no         | All      |yes       |
| borderRadius  | The border radius of the toast box, which determines how rounded the corners are         | number  | no | All      | yes |
| blurBackdrop  | The intensity of the background blur effect on Android platforms         | number  | no | Android      | no |
| backdropOpacity  | The opacity of the background blur effect on Android platforms, with a range from 0 (fully transparent) to 1 (fully opaque)         | number  | no | All      | yes |
| icon                 | A custom icon for the toast                                                     | object  | no        | All      | yes  |
| progressColor        | The color of the progress spinner for the spinner preset style                                                     | string  | no        | Android   | yes  |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| toast  | Displays a Toast notification         | function  | yes | All      | yes |
| alert  | Displays an Alert dialog         | function  | yes | All      | yes |
| dismissAlert  | Closes the currently displayed Alert dialog         | function  | yes | All      | yes |
| setup  | Configures global settings for Toast and Alert         | function  | yes | All      | yes |

## 遗留问题

- [ ] AlertOptions和ToastOptions中的preset：done，动画效果未实现。[issue#3](https://github.com/react-native-oh-library/ting/issues/3)

## 其他

- AlertOptions中的blurBackdrop参数配置后，iOS不支持，Android无效果。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/baronha/ting/blob/main/LICENSE) ，请自由地享受和参与开源。