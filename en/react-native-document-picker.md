> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/document-picker)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-document-picker Releases](https://github.com/react-native-oh-library/document-picker/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-document-picker
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-document-picker
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import {
  Text,
  TouchableOpacity,
  View,
  StyleSheet,
  Switch,
  ScrollView,
} from "react-native";
import {
  pick,
  types,
  pickDirectory,
  pickSingle,
  DocumentPickerOptions,
} from "react-native-document-picker";

const typeList = Object.keys(types);

interface MultiSelectProps {
  onSelectValue?: (val: string[]) => void;
}

interface UiSelItem {
  label: keyof typeof types;
  selected: boolean;
  index: number;
}

type DirType = "documentDirectory" | "cachesDirectory";

interface DirOpt {
  label: DirType;
  selected: boolean;
}

const MultiSelect: React.FC<MultiSelectProps> = ({ onSelectValue }) => {
  const [typeUi, setTypeUi] = useState<UiSelItem[]>(
    typeList.map((val, index) => ({
      label: val as keyof typeof types,
      selected: false,
      index,
    }))
  );

  const onClickSelLabel = (val: (typeof typeUi)[0]) => {
    if (
      typeUi.find((t) => t.label === "allFiles")?.selected &&
      val.label !== "allFiles"
    ) {
      return;
    }
    let newList = [];
    if (val.label === "allFiles") {
      newList = typeUi.map((s) => {
        return s.label === "allFiles"
          ? { ...s, selected: !s.selected }
          : { ...s, selected: false };
      });
    } else {
      newList = typeUi.map((s) => {
        return val.index === s.index
          ? { ...s, selected: !s.selected }
          : { ...s };
      });
    }
    const extList = newList
      .filter((t) => t.selected)
      .map((t) => types[t.label])
      .reduce((res, typeStr) => {
        res.push(...typeStr.split(" "));
        return res;
      }, [] as string[]);
    if (onSelectValue) {
      onSelectValue(extList);
    }
    setTypeUi(newList);
  };

  return (
    <>
      <View
        style={{
          display: "flex",
          flexWrap: "wrap",
          flexDirection: "row",
          rowGap: 14,
        }}
      >
        <View style={{ width: "100%" }}>
          <Text style={{ fontSize: 20, fontWeight: "600", margin: 6 }}>
            picker 的文件类型
          </Text>
        </View>
        {typeUi.map((s) => (
          <TouchableOpacity
            key={s.label}
            onPress={() => {
              onClickSelLabel(s);
            }}
          >
            <View
              style={s.selected ? styles.selectBtnActive : styles.selectBtn}
            >
              <Text>{s.label}</Text>
            </View>
          </TouchableOpacity>
        ))}
      </View>
    </>
  );
};

export default function DocumentPickerDemo(): JSX.Element {
  const [pickResult, setPickResult] = useState("");
  const [allowMultiSelection, setAllowMultiSelection] = useState(true);
  const [fileTypes, setFileTypes] = useState<string[]>([]);
  const [dirUi, setDirui] = useState<Array<DirOpt>>([
    { label: "documentDirectory", selected: false },
    { label: "cachesDirectory", selected: false },
  ]);

  const copyTo = dirUi.find((d) => d.selected)?.label;

  const pickOpt: DocumentPickerOptions<"harmony"> = {
    allowMultiSelection,
  };
  if (copyTo) {
    pickOpt.copyTo = copyTo;
  }
  if (fileTypes.length) {
    pickOpt.type = fileTypes;
  }

  const onDirSelect = (val: DirOpt) => {
    const newUiList = dirUi.map((d) => {
      if (val.label === d.label) {
        return { ...d, selected: !d.selected };
      } else {
        return { ...d, selected: false };
      }
    });
    setDirui(newUiList);
  };

  const pickFile = async () => {
    try {
      const res = await pick(pickOpt);
      setPickResult(JSON.stringify(res));
    } catch (err) {
      console.log(err);
    }
  };

  const pickS = async () => {
    try {
      const res = await pickSingle(pickOpt);
      setPickResult(JSON.stringify(res));
    } catch (err) {
      console.log(err);
    }
  };

  const pickDir = async () => {
    const res = await pickDirectory();
    console.log(res);
  };

  return (
    <ScrollView>
      <Text>{JSON.stringify(pickOpt)}</Text>

      <MultiSelect onSelectValue={setFileTypes}></MultiSelect>

      <View style={{ width: "100%" }}>
        <Text style={{ fontSize: 20, fontWeight: "600", margin: 6 }}>
          是否多选
        </Text>
      </View>

      <Switch
        value={allowMultiSelection}
        onValueChange={setAllowMultiSelection}
      ></Switch>

      <View style={{ width: "100%" }}>
        <Text style={{ fontSize: 20, fontWeight: "600", margin: 6 }}>
          copyTo文件夹
        </Text>
      </View>

      <View
        style={{
          display: "flex",
          flexWrap: "wrap",
          flexDirection: "row",
          rowGap: 14,
        }}
      >
        {dirUi.map((s) => (
          <TouchableOpacity
            key={s.label}
            onPress={() => {
              onDirSelect(s);
            }}
          >
            <View
              style={s.selected ? styles.selectBtnActive : styles.selectBtn}
            >
              <Text>{s.label}</Text>
            </View>
          </TouchableOpacity>
        ))}
      </View>

      <TouchableOpacity onPress={pickFile} style={styles.btn}>
        <Text style={styles.btnText}>pick file</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={pickS} style={styles.btn}>
        <Text style={styles.btnText}>pick file single</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={pickDir} style={styles.btn}>
        <Text style={styles.btnText}>pick Dir</Text>
      </TouchableOpacity>
      <View style={{ width: "100%" }}>
        <Text style={{ fontSize: 20, fontWeight: "600", margin: 6 }}>
          选择结果
        </Text>
      </View>
      <Text>{pickResult}</Text>
    </ScrollView>
  );
}

const styles = StyleSheet.create({
  TextInput: {
    height: 40,
    borderColor: "#ccc",
    borderWidth: 1,
    borderRadius: 4,
    width: "90%",
  },
  btn: {
    borderRadius: 10,
    display: "flex",
    justifyContent: "center",
    alignItems: "center",
    padding: 10,
    margin: 10,
    backgroundColor: "blue",
  },
  btnText: { fontWeight: "bold", color: "#fff", fontSize: 20 },
  selectBtn: {
    padding: 8,
    margin: 3,
    fontSize: 18,
    borderWidth: 1,
    borderRadius: 8,
    borderColor: "#753c13",
  },
  selectBtnActive: {
    padding: 8,
    margin: 3,
    backgroundColor: "#e2803b",
    fontSize: 18,
    borderRadius: 8,
    borderWidth: 1,
  },
});
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
    "@react-native-oh-tpl/react-native-document-picker": "file:../../node_modules/@react-native-oh-tpl/react-native-document-picker/harmony/document_picker.har"
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

### 3. Introducing DocumentPickerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-document-picker Releases](https://github.com/react-native-oh-library/document-picker/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### option pick 方法的传参选项

| Name                | Description                                                                                                                                                                                         | Type                                                                    | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| allowMultiSelection | Whether selecting multiple files is allowed. For pick, this is false by default. allowMultiSelection is false for pickSingle and cannot be overridden.                                              | boolean                                                                 | no       | IOS/Android | yes               |
| type                | The type or types of documents to allow selection of. An array of strings or single string.                                                                                                         | string or Array<string>                                                 | no       | IOS/Android | yes               |
| copyTo              | Copy the selected file to the specified folder.                                                                                                                                                     | "cachesDirectory" \| "documentDirectory"                                | no       | IOS/Android | yes               |
| presentationStyle   | Controls how the picker is presented, e.g. on an iPad you may want to present it fullscreen. Defaults to pageSheet.                                                                                 | 'fullScreen' \| 'pageSheet' \| 'formSheet' \| 'overFullScreen'          | no       | IOS         | no                |
| transitionStyle     | Configure the transition style of the picker. Defaults to coverVertical.                                                                                                                            | 'coverVertical' \| 'flipHorizontal' \| 'crossDissolve' \| 'partialCurl' | no       | IOS         | no                |
| mode                | Defaults to import. If mode is set to import the document picker imports the file from outside to inside the sandbox, otherwise if mode is set to open the document picker opens the file in-place. | "import" \| "open"                                                      | no       | IOS         | no                |

## API

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                                                                                                                                                                                                                                                                                     | Type     | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| pick                | The method for picking a file.                                                                                                                                                                                                                                                                                  | function | No       | IOS/Android | yes               |
| pickSingle          | Select a single file                                                                                                                                                                                                                                                                                            | function | No       | IOS/Android | yes               |
| pickDirectory       | Opens a directory picker.                                                                                                                                                                                                                                                                                       | function | No       | IOS/Android | no                |
| isCancel            | If the user cancels the document picker without choosing a file (by pressing the system back button on Android or the Cancel button on iOS), the Promise will be rejected with a cancellation error. You can check for this error using DocumentPicker.isCancel(err).                                           | function | No       | IOS/Android | yes               |
| isInProgress        | If the user somehow manages to open multiple file pickers (e.g. due the app being unresponsive), then only the picked result from the last opened picker will be considered and the promises from previous opened pickers will be rejected with an error that you can check using DocumentPicker.isInProgress() | function | No       | IOS/Android | yes               |
| releaseSecureAccess | If mode is set to open, iOS is giving you secure access to a file located outside from your sandbox. In that case Apple is asking you to release the access as soon as you finish using the resource.                                                                                                           | function | No       | IOS         | no                |
| types               | File type object. eg type.images、types.pdf                                                                                                                                                                                                                                                                     | function | No       | IOS/Android | yes               |
| perPlatformTypes    | Different platforms, file type object map                                                                                                                                                                                                                                                                       | function | No       | IOS/Android | yes               |

## Known Issues

- [ ] HarmonyOS 端 file picker selectMode 设置选文件夹无效: [issue#1](https://github.com/react-native-oh-library/document-picker/issues/1)
- [ ] releaseSecureAccess 选择沙箱路径外文件无法实现， HarmonyOS 暂无此能力接口: [issue#2](https://github.com/react-native-oh-library/document-picker/issues/2)

## Others

- 因权限问题无法读写图库资源，文件管理中从图库选择文件暂不支持。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-documents/document-picker/blob/master/LICENSE.md).
