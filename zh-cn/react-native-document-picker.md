> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-document-picker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-documents/document-picker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-documents/document-picker/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/document-picker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-document-picker Releases](https://github.com/react-native-oh-library/document-picker/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-document-picker@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-document-picker@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState } from "react";
import { Text, TouchableOpacity, View, StyleSheet, Switch, ScrollView } from 'react-native';
import { pick, types, pickDirectory, pickSingle, DocumentPickerOptions } from 'react-native-document-picker';

const typeList = Object.keys(types);

interface MultiSelectProps {
  onSelectValue?: (val: string[]) => void
}

interface UiSelItem {
  label: keyof typeof types,
  selected: boolean,
  index: number
}

type DirType = 'documentDirectory' | 'cachesDirectory'

interface DirOpt {
  label: DirType,
  selected: boolean
}

const MultiSelect: React.FC<MultiSelectProps> = ({ onSelectValue }) => {

  const [typeUi, setTypeUi] = useState<UiSelItem[]>(typeList.map((val, index) => ({
    label: val as keyof typeof types,
    selected: false,
    index
  })))

  const onClickSelLabel = (val: typeof typeUi[0]) => {
    // 选择allfile不行选择其它的
    if (typeUi.find(t => t.label === 'allFiles')?.selected && val.label !== 'allFiles') {
      return;
    }
    let newList = [];
    if (val.label === 'allFiles') {
      newList = typeUi.map(s => {
        return s.label === 'allFiles' ? { ...s, selected: !s.selected } : { ...s, selected: false }
      })
    } else {
      newList = typeUi.map(s => {
        return val.index === s.index ? { ...s, selected: !s.selected } : { ...s }
      })
    }
    const extList = newList.filter(t => t.selected).map(t => types[t.label]).reduce((res, typeStr) => {
      res.push(...typeStr.split(' '))
      return res;
    }, [] as string[]);
    if (onSelectValue) {
      onSelectValue(extList)
    }
    setTypeUi(newList);
  }

  return <>
    <View style={{ display: 'flex', flexWrap: 'wrap', flexDirection: 'row', rowGap: 14 }}>
      <View style={{ width: '100%' }}>
        <Text style={{ fontSize: 20, fontWeight: '600', margin: 6 }}>picker 的文件类型</Text>
      </View>
      {
        typeUi.map(s =>
          <TouchableOpacity key={s.label} onPress={() => {
            onClickSelLabel(s);
          }} >
            <View style={s.selected ? styles.selectBtnActive : styles.selectBtn} >
              <Text>
                {s.label}
              </Text>
            </View>
          </TouchableOpacity>
        )
      }
    </View>
  </>
}

export default function DocumentPickerDemo(): JSX.Element {

  const [pickResult, setPickResult] = useState('');
  // 是否允许多选
  const [allowMultiSelection, setAllowMultiSelection] = useState(true);
  // 选择文件类型
  const [fileTypes, setFileTypes] = useState<string[]>([]);
  // copyTo 文件夹
  const [dirUi, setDirui] = useState<Array<DirOpt>>([
    { label: 'documentDirectory', selected: false },
    { label: 'cachesDirectory', selected: false },
  ]);

  const copyTo = dirUi.find(d => d.selected)?.label;

  const pickOpt: DocumentPickerOptions<'harmony'> = {
    allowMultiSelection,
  };
  if (copyTo) {
    pickOpt.copyTo = copyTo;
  }
  if (fileTypes.length) {
    pickOpt.type = fileTypes;
  }

  const onDirSelect = (val: DirOpt) => {
    const newUiList = dirUi.map(d => {
      if (val.label === d.label) {
        return { ...d, selected: !d.selected }
      } else {
        return { ...d, selected: false }
      }
    });
    setDirui(newUiList);
  }

  const pickFile = async () => {
    try {
      const res = await pick(pickOpt);
      setPickResult(JSON.stringify(res));
    } catch (err) {
      console.log(err);
    }
  }

  const pickS = async () => {
    try {
      const res = await pickSingle(pickOpt);
      setPickResult(JSON.stringify(res));
    } catch (err) {
      console.log(err);
    }
  }

  const pickDir = async () => {
    const res = await pickDirectory();
    console.log(res);
  }

  return <ScrollView>
    <Text>
      {JSON.stringify(pickOpt)}
    </Text>

    <MultiSelect onSelectValue={setFileTypes}></MultiSelect>

    <View style={{ width: '100%' }}>
      <Text style={{ fontSize: 20, fontWeight: '600', margin: 6 }}>是否多选</Text>
    </View>

    <Switch value={allowMultiSelection} onValueChange={setAllowMultiSelection}></Switch>

    <View style={{ width: '100%' }}>
      <Text style={{ fontSize: 20, fontWeight: '600', margin: 6 }}>copyTo文件夹</Text>
    </View>

    <View style={{ display: 'flex', flexWrap: 'wrap', flexDirection: 'row', rowGap: 14 }}>
      {
        dirUi.map(s =>
          <TouchableOpacity key={s.label} onPress={() => {
            onDirSelect(s);
          }} >
            <View style={s.selected ? styles.selectBtnActive : styles.selectBtn} >
              <Text>
                {s.label}
              </Text>
            </View>
          </TouchableOpacity>
        )
      }
    </View>

    <TouchableOpacity onPress={pickFile} style={styles.btn}>
      <Text
        style={styles.btnText}>
        pick file
        </Text>
    </TouchableOpacity>
    <TouchableOpacity onPress={pickS} style={styles.btn}>
      <Text
        style={styles.btnText}>
        pick file single
        </Text>
    </TouchableOpacity>
    <TouchableOpacity onPress={pickDir} style={styles.btn}>
      <Text
        style={styles.btnText}>
        pick Dir
        </Text>
    </TouchableOpacity>
    <View style={{ width: '100%' }}>
      <Text style={{ fontSize: 20, fontWeight: '600', margin: 6 }}>选择结果</Text>
    </View>
    <Text>
      {pickResult}
    </Text>
  </ScrollView>
}

const styles = StyleSheet.create({
  TextInput: { height: 40, borderColor: '#ccc', borderWidth: 1, borderRadius: 4, width: '90%' },
  btn: { borderRadius: 10, display: 'flex', justifyContent: 'center', alignItems: 'center', padding: 10, margin: 10, backgroundColor: 'blue' },
  btnText: { fontWeight: 'bold', color: '#fff', fontSize: 20 },
  selectBtn: { padding: 8, margin: 3, fontSize: 18, borderWidth: 1, borderRadius: 8, borderColor: '#753c13' },
  selectBtnActive: { padding: 8, margin: 3, backgroundColor: '#e2803b', fontSize: 18, borderRadius: 8, borderWidth: 1 }
});


```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides字段

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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-document-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-document-picker/harmony/document_picker.har"
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

### 在 ArkTs 侧引入 DocumentPickerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { DocumentPickerPackage } from '@react-native-oh-tpl/react-native-document-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new DocumentPickerPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-document-picker Releases](https://github.com/react-native-oh-library/document-picker/releases)

本文档内容基于以下版本验证通过：
1. RNOH: 0.72.20-CAPI; SDK: HarmonyOS NEXT Developer Beta1; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.18;
   
## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

### option pick方法的传参选项

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| allowMultiSelection  | Whether selecting multiple files is allowed. For pick, this is false by default. allowMultiSelection is false for pickSingle and cannot be overridden.        | boolean  | no | IOS/Android      | yes |
| type  | The type or types of documents to allow selection of. An array of strings or single string.   | string or Array<string>  | no | IOS/Android      | yes |
| copyTo  | Copy the selected file to the specified folder.   | "cachesDirectory" \| "documentDirectory"  | no | IOS/Android  | yes |
| presentationStyle  | Controls how the picker is presented, e.g. on an iPad you may want to present it fullscreen. Defaults to pageSheet.   | 'fullScreen' \| 'pageSheet' \| 'formSheet' \| 'overFullScreen'  | no | IOS  | no |
| transitionStyle  | Configure the transition style of the picker. Defaults to coverVertical.   | 'coverVertical' \| 'flipHorizontal' \| 'crossDissolve' \| 'partialCurl'  | no | IOS  | no |
| mode  | Defaults to import. If mode is set to import the document picker imports the file from outside to inside the sandbox, otherwise if mode is set to open the document picker opens the file in-place.   | "import" \| "open"  | no | IOS  | no |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name           | Description                   | Type | Required | Platform    | HarmonyOS Support |
|----------------|-------------------------------| -- | -------- | ----------- | ----------------- |
| pick    | The method for picking a file. | function | No       | IOS/Android | yes               |
| pickSingle       | Select a single file       | function | No       | IOS/Android | yes  |
| pickDirectory       | Opens a directory picker.       | function | No       | IOS/Android | no  |
| isCancel       | If the user cancels the document picker without choosing a file (by pressing the system back button on Android or the Cancel button on iOS), the Promise will be rejected with a cancellation error. You can check for this error using DocumentPicker.isCancel(err).       | function | No       | IOS/Android | yes  |
| isInProgress       | If the user somehow manages to open multiple file pickers (e.g. due the app being unresponsive), then only the picked result from the last opened picker will be considered and the promises from previous opened pickers will be rejected with an error that you can check using DocumentPicker.isInProgress()   | function | No       | IOS/Android | yes  |
| releaseSecureAccess  | If mode is set to open, iOS is giving you secure access to a file located outside from your sandbox. In that case Apple is asking you to release the access as soon as you finish using the resource.   | function | No       | IOS | no  |
| types       | File type object. eg type.images、types.pdf   | function | No       | IOS/Android | yes  |
| perPlatformTypes       | Different platforms, file type object map   | function | No       | IOS/Android | yes  |


## 遗留问题

- [ ]  HarmonyOS 端file picker selectMode设置选文件夹无效: [issue#1](https://github.com/react-native-oh-library/document-picker/issues/1) 
- [ ] releaseSecureAccess选择沙箱路径外文件无法实现， HarmonyOS 暂无此能力接口: [issue#2](https://github.com/react-native-oh-library/document-picker/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-documents/document-picker/blob/master/LICENSE.md) ，请自由地享受和参与开源。

