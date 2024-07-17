<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mail</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/chirag04/react-native-mail">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/chirag04/react-native-mail/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
         <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-mail)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[https://github.com/react-native-oh-library/react-native-mail Releases](https://github.com/react-native-oh-library/react-native-mail/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-mail@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-mail@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import React, { Component } from 'react';
import { View, Alert, Button } from 'react-native';
import Mailer from 'react-native-mail';

export default class App extends Component {

  handleEmail = () => {
    Mailer.mail({
      subject: 'need help',
      recipients: ['support@example.com'],
      ccRecipients: ['supportCC@example.com'],
      bccRecipients: ['supportBCC@example.com'],
      body: '<b>A Bold Body</b>',
      customChooserTitle: 'This is my new title', // Android only (defaults to "Send Mail")
      isHTML: true,
      attachments: [{
        // Specify either `path` or `uri` to indicate where to find the file data.
        path: '', // /data/storage/el2/base/haps/entry/files/11.png
        uri: '', // file://<packageName>/data/storage/el2/base/haps/entry/files/11.png
        // Specify either `type` or `mimeType` to indicate the type of data.
        type: '', // Mime Type: jpg, png, doc, ppt, html, pdf, csv
        mimeType: '', // - use only if you want to use custom type
        name: '', // Optional: Custom filename for attachment
      }]
    }, (error, event) => {
      Alert.alert(
        error,
        event,
        [
          {text: 'Ok', onPress: () => console.log('OK: Email Error Response')},
          {text: 'Cancel', onPress: () => console.log('CANCEL: Email Error Response')}
        ],
        { cancelable: true }
      )
    });
  }

  render() {
    return (
      <View style={styles.container}>
        <Button
          onPress={this.handleEmail}
          title="Email Me"
          color="#841584"
          accessabilityLabel="Purple Email Me Button"
        />
      </View>
    );
  }
}

```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

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
    "@react-native-oh-tpl/react-native-mail": "file:../../node_modules/@react-native-oh-tpl/react-native-mail/harmony/mail.har"
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

### 在 ArkTs 侧引入 RNMailPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {RNMailPackage} from '@react-native-oh-tpl/react-native-mail/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNMailPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-mail Releases](https://github.com/react-native-oh-library/react-native-mail/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| mail  | 拉起邮箱并向邮箱传递收件人、发件人、抄送人等信息，通过callback函数返回错误信息。         | Function(options,callback)  | yes | all      | yes |

**options**

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| subject        | 邮件主题       | string  | no | all      | yes |
| recipients     | 收件人         | string[]  | no | all      | yes |
| ccRecipients   | 抄送收件人     | string[]  | no | all      | yes |
| bccRecipients  | 密件抄送收件人 | string[]  | no | all      | yes |
| body           | 邮件内容      | string  | no | all      | yes |
| customChooserTitle  | 自定义选择器标题 | string  | no | android      | no |
| isHTML  | 邮件内容是否为html        | boolean  | no | all      | yes |
| attachments  | 附件信息         | object[]  | no | all      | no |

## 遗留问题

- [ ] 不支持attachments附件传递: [issue#1](https://github.com/react-native-oh-library/react-native-mail/issues/1)
- [ ] 不支持customChooserTitle: [issue#4](https://github.com/react-native-oh-library/react-native-mail/issues/4)
- [ ] 邮箱应用上body显示异常: [issue#2](https://github.com/react-native-oh-library/react-native-mail/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/chirag04/react-native-mail/blob/master/LICENSE) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
