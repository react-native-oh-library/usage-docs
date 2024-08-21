> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-email-link</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/tschoffelen/react-native-email-link">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/tschoffelen/react-native-email-link/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-email-link)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-email-link Releases](https://github.com/react-native-oh-library/react-native-email-link/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-email-link@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-email-link@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import {
  SafeAreaView,
  View,
  StyleSheet,
  Text,
  StatusBar,
  Button,
} from "react-native";
import {
  getEmailClients,
  openInbox,
  openComposer,
} from "react-native-email-link";

export function EmailLinkExample() {
  const [emailClients, setEmailClients] = useState(
    "点击getEmailClients按钮获取邮箱信息"
  );
  return (
    <SafeAreaView style={styles.container}>
      <View style={styles.wrapper}>
        <Text style={styles.text}>{emailClients}</Text>
        <Button
          title="getEmailClients"
          onPress={async () => {
            let clients = await getEmailClients();
            setEmailClients(JSON.stringify(clients));
          }}
        />

        <Button
          title="openInbox-without-app"
          onPress={() => {
            openInbox();
          }}
        />

        <Button
          title="openInbox-with-app"
          onPress={() => {
            openInbox({
              app: "mail",
            });
          }}
        />

        <Button
          title="openComposer-without-app"
          onPress={() => {
            openComposer({
              to: "support@example.com",
              cc: "cc@example.com",
              bcc: "bcc@example.com",
              subject: "I have a question",
              body: "Hi, can you help me with...",
            });
          }}
        />

        <Button
          title="openComposer-with-app"
          onPress={() => {
            openComposer({
              app: "mail",
              to: "support@example.com",
              cc: "cc@example.com",
              bcc: "bcc@example.com",
              subject: "I have a question",
              body: "Hi, can you help me with...",
            });
          }}
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    marginTop: StatusBar.currentHeight,
  },
  item: {
    backgroundColor: "#f9c2ff",
    justifyContent: "center",
    marginVertical: 8,
    marginHorizontal: 16,
    padding: 20,
  },
  title: {
    fontSize: 24,
  },
  wrapper: {
    height: 200,
  },
  text: {
    marginBottom: 20,
    color: "white",
    textAlign: "center",
  },
});
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

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
    "@react-native-oh-tpl/react-native-email-link": "file:../../node_modules/@react-native-oh-tpl/react-native-email-link/harmony/email_link.har"
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

### 在 ArkTs 侧引入 RNEmailLinkPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNEmailLinkPackage} from '@react-native-oh-tpl/react-native-email-link/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNEmailLinkPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-email-link Releases](https://github.com/react-native-oh-library/react-native-email-link/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name              | Description                                                                                            | Type     | Required | Platform | HarmonyOS Support |
| ----------------- | ------------------------------------------------------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `openInbox`       | Directly open the inbox of the default mail client on your device.                                     | function | No       | All      | yes               |
| `openComposer`    | Used to open a new email authoring interface that allows users to create emails directly from the app. | function | No       | All      | yes               |
| `getEmailClients` | Get a list of all supported mail client applications installed on the device.                          | function | No       | All      | yes               |

**openInbox 方法参数**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `title` | Text for the top of the ActionSheet or Intent | string | no | All | no |
| `message` | Subtext under the title on the ActionSheet | string | no | iOS | no |
| `cancelLabel` | Text for last button of the ActionSheet | string | no | iOS | no |
| `removeText` | If true, not text will be show above the ActionSheet or Intent. Default value is false | boolean | no | All | no |
| `defaultEmailLabel` | Text for first button of the ActionSheet | function | no | iOS | no |
| `newTask` | If true, the email Intent will be started in a new Android task. Else, the Intent will be launched in the current task | boolean | no | Android | no |

**openComposer 方法参数**
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `app` | App to open the composer with| string | no | All | yes |
| `title` | Text for the top of the ActionSheet or Intent | string | no | All | no |
| `message` | Subtext under the title on the ActionSheet | string | no | iOS | no |
| `cancelLabel` | Text for last button of the ActionSheet | string | no | iOS | no |
| `removeText` | If true, not text will be show above the ActionSheet or Intent. Default value is false | boolean | no | All | no |
| `defaultEmailLabel` | Text for first button of the ActionSheet | function | no | iOS | no |
| `to` | Recipient's email address | string | no | All | yes |
| `cc` | Email's cc | string | no | All | yes |
| `bcc` | Email's bcc | string | no | All | yes |
| `subject` | Email's subject | string | no | All | yes |
| `body` | Email's body | string | no | All | yes |
| `encodeBody` | Apply encodeURIComponent to the email's body | boolean | no | All | yes |

## 遗留问题

- [ ] 目前只支持 harmonyOS 系统自带邮箱，本库支持邮箱均未适配harmonyOS Next。[issues#5](https://github.com/react-native-oh-library/react-native-email-link/issues/5)

## 其他

- title、message、cancelLabel、 removeText、defaultEmailLabel、newTask属性暂不支持，与iOS表现一致。[issue#141](https://github.com/tschoffelen/react-native-email-link/issues/141)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/tschoffelen/react-native-email-link/blob/master/LICENSE) ，请自由地享受和参与开源。
