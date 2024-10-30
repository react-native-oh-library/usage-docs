> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-print)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-print Releases](https://github.com/react-native-oh-library/react-native-print/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-print@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-print@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
         title="local url printing"
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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/zh-cn/codegen.md).

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
    "@react-native-oh-tpl/react-native-print": "file:../../node_modules/@react-native-oh-tpl/react-native-print/harmony/print.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/zh-cn/link-source-code.md).

### 3. Introducing RNPrintPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-print Releases](https://github.com/react-native-oh-library/react-native-print/releases)

### Permission Requirements

#### Include applicable permissions in the module.json5 file within the entry directory.

Open the `entry/src/main/module.json5` file and add the following code:

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
+    "name": "fs.OpenMode.READ_ONLY",
+    "reason": "$string:fs_reason",
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

#### Apply the reasons for applicable permission in the entry directory.

Open the `entry/src/main/resources/base/element/string.json` file and add the following code:

```diff
...
{
  "string": [
+    {
+      "name": "print_reason",
+      "value": "Using a printer"
+    },
+    {
+      "name": "fs_reason",
+      "value": "Read data"
+    },
+    {
+      "name": "internet_reason",
+      "value": "Network request data"
+    },
  ]
}
```

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] HarmonyOS NEXT 上不支持 html、printerURL、isLandscape、baseUrl 等参数，并且不支持打印 word 文档: [issue#1](https://github.com/react-native-oh-library/react-native-print/issues/1)
- [ ] HarmonyOS NEXT 上不支持 selectPrinter()方法 : [issue#2](https://github.com/react-native-oh-library/react-native-print/issues/4)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/christopherdro/react-native-print/blob/master/LICENSE).
