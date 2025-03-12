> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-mail)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-mail Releases](https://github.com/react-native-oh-library/react-native-mail/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-mail
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-mail
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```jsx
import React, { Component } from "react";
import { View, Alert, Button } from "react-native";
import Mailer from "react-native-mail";

export default class App extends Component {
  handleEmail = () => {
    Mailer.mail(
      {
        subject: "need help",
        recipients: ["support@example.com"],
        ccRecipients: ["supportCC@example.com"],
        bccRecipients: ["supportBCC@example.com"],
        body: "<b>A Bold Body</b>",
        customChooserTitle: "This is my new title", // Android only (defaults to "Send Mail")
        isHTML: true,
        attachments: [
          {
            // Specify either `path` or `uri` to indicate where to find the file data.
            path: "", // /data/storage/el2/base/haps/entry/files/11.png
            uri: "", // file://<packageName>/data/storage/el2/base/haps/entry/files/11.png
            // Specify either `type` or `mimeType` to indicate the type of data.
            type: "", // Mime Type: jpg, png, doc, ppt, html, pdf, csv
            mimeType: "", // - use only if you want to use custom type
            name: "", // Optional: Custom filename for attachment
          },
        ],
      },
      (error, event) => {
        Alert.alert(
          error,
          event,
          [
            {
              text: "Ok",
              onPress: () => console.log("OK: Email Error Response"),
            },
            {
              text: "Cancel",
              onPress: () => console.log("CANCEL: Email Error Response"),
            },
          ],
          { cancelable: true }
        );
      }
    );
  };

  render() {
    return (
      <View>
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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-mail": "file:../../node_modules/@react-native-oh-tpl/react-native-mail/harmony/mail.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Introducing RNMailPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

### 4. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-mail Releases](https://github.com/react-native-oh-library/react-native-mail/releases)

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description                                                                        | Type                       | Required | Platform | HarmonyOS Support |
| ---- | ---------------------------------------------------------------------------------- | -------------------------- | -------- | -------- | ----------------- |
| mail | 拉起邮箱并向邮箱传递收件人、发件人、抄送人等信息，通过 callback 函数返回错误信息。 | Function(options,callback) | yes      | all      | yes               |

**options**

| Name               | Description         | Type     | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------- | -------- | -------- | -------- | ----------------- |
| subject            | 邮件主题            | string   | no       | all      | yes               |
| recipients         | 收件人              | string[] | no       | all      | yes               |
| ccRecipients       | 抄送收件人          | string[] | no       | all      | yes               |
| bccRecipients      | 密件抄送收件人      | string[] | no       | all      | yes               |
| body               | 邮件内容            | string   | no       | all      | yes               |
| customChooserTitle | 自定义选择器标题    | string   | no       | android  | no                |
| isHTML             | 邮件内容是否为 html | boolean  | no       | all      | no               |
| attachments        | 附件信息            | object[] | no       | all      | no                |

## Known Issues

- [ ] 不支持 attachments 附件传递: [issue#1](https://github.com/react-native-oh-library/react-native-mail/issues/1)
- [ ] 不支持 customChooserTitle: [issue#4](https://github.com/react-native-oh-library/react-native-mail/issues/4)
- [x] 邮箱应用上 body 显示异常: [issue#2](https://github.com/react-native-oh-library/react-native-mail/issues/2)
- [ ] 不支持 isHTML: [issue#7](https://github.com/react-native-oh-library/react-native-mail/issues/7)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/chirag04/react-native-mail/blob/master/LICENSE).
