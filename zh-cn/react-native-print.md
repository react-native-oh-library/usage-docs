> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-print</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/christopherdro/react-native-print">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20Windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/christopherdro/react-native-print/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-print)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-print Releases](https://github.com/react-native-oh-library/react-native-print/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-print
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-print
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 本示例依赖 react-native-document-picker 库，参照[@react-native-oh-tpl/react-native-document-picker 文档](/zh-cn/react-native-document-picker.md)进行引入。

```js
import React, {useState} from 'react';
import {
  ScrollView,
  Button,
} from 'react-native';
import {
  pick,
  DocumentPickerOptions,
  isCancel,
} from 'react-native-document-picker';
import RNPrint from 'react-native-print';

type DirType = 'documentDirectory' | 'cachesDirectory';

interface DirOpt {
  label: DirType;
  selected: boolean;
}

export default function RNPrint(): JSX.Element {
  const [pickResult, setPickResult] = useState('');
  const [allowMultiSelection, setAllowMultiSelection] = useState(true);
  const [fileTypes, setFileTypes] = useState<string[]>([]);
  const [dirUi, setDirui] = useState<Array<DirOpt>>([
    {label: 'documentDirectory', selected: false},
    {label: 'cachesDirectory', selected: false},
  ]);
  const copyTo = dirUi.find(d => d.selected)?.label;
  const pickOpt: DocumentPickerOptions<'harmony'> = {
    allowMultiSelection,
    presentationStyle: 'overFullScreen',
  };
  if (copyTo) {
    pickOpt.copyTo = copyTo;
  }
  if (fileTypes.length) {
    pickOpt.type = fileTypes;
  }
  const pickFile = async () => {
    try {
      const res = await pick(pickOpt);
      setPickResult(JSON.stringify(res));
      return res;
    } catch (err) {
      console.log(err);
      console.log('isCancel: ' + isCancel(err));
    }
  };

  return (
        <Button
         title="本地url打印"
         onPress={async () => {
            const res = await pickFile();
            RNPrint.print({
                filePath: res[0].uri,
                jobName: 'huawei',
            });
            }}
        />
  );
}

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
    "@react-native-oh-tpl/react-native-print": "file:../../node_modules/@react-native-oh-tpl/react-native-print/harmony/print.har"
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

### 3.在 ArkTs 侧引入 RNPrintPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNPrintPackage} from '@react-native-oh-tpl/react-native-print/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNPrintPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-print Releases](https://github.com/react-native-oh-library/react-native-print/releases)

### 权限要求

#### 在 entry 目录下的 module.json5 中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.PRINT",
+    "reason": "$string:print_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"always"
+    }
+  },
+  {
+    "name": "ohos.permission.INTERNET",
+    "reason": "$string:internet_reason",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"always"
+    }
+  }
]
```

#### 在 entry 目录下添加申请以上权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "print_reason",
+      "value": "使用打印机"
+    },
+    {
+      "name": "internet_reason",
+      "value": "网络请求数据"
+    },
  ]
}
```

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### print(options: Object)

| Name          | Description                                                   | Type    | Required | Platform     | HarmonyOS Support |
| ------------- | ------------------------------------------------------------- | ------- | -------- | ------------ | ----------------- |
| `html`        | HTML string to print(The value must be html or filepath.)     | string  | no       | Android、iOS | no                |
| `filePath`    | Local or remote file url(The value must be html or filepath.) | string  | no       | Android、iOS | yes               |
| `printerURL`  | **iOS Only:** URL returned from `selectPrinterMethod()`       | string  | no       | iOS          | no                |
| `isLandscape` | Landscape print; default value is false                       | boolean | no       | Android、iOS | no                |
| `jobName`     | Name of printing job; default value is "Document"             | string  | no       | Android、iOS | yes               |
| `baseUrl`     | Used to resolve relative links in the HTML                    | string  | no       | Android      | no                |

### selectPrinter(options: Object)

| Name | Description                        | Type   | Required | Platform | HarmonyOS Support |
| ---- | ---------------------------------- | ------ | -------- | -------- | ----------------- |
| `x`  | The x position of the popup dialog | number | yes      | iOS      | no                |
| `y`  | The y position of the popup dialog | number | yes      | iOS      | no                |

## 遗留问题

- [ ] HarmonyOS NEXT 上不支持 html、printerURL、isLandscape、baseUrl 等参数，并且不支持打印 word 文档: [issue#1](https://github.com/react-native-oh-library/react-native-print/issues/1)
- [ ] HarmonyOS NEXT 上不支持 selectPrinter()方法 : [issue#2](https://github.com/react-native-oh-library/react-native-print/issues/4)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/christopherdro/react-native-print/blob/master/LICENSE) ，请自由地享受和参与开源。
