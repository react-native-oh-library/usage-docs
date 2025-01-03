> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-document-picker</code> </h1>
</p>


This project is based on [react-native-document-picker@9.2.0](https://github.com/react-native-documents/document-picker).

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-document-picker`, The version correspondence details are as follows:
| Version                        | Package Name                             | Repository                                                   | Release                                                      |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 9.2.0@deprecated | @react-native-oh-tpl/react-native-document-picker  | [Github(deprecated)](https://github.com/react-native-oh-library/document-picker) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/document-picker/releases) |
| > 9.2.0                        | @react-native-ohos/react-native-document-picker | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-document-picker) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-document-picker/releases) |


## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-ohos/react-native-document-picker
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-document-picker
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
            File type of the picker.
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
          Whether allow multiple selections.
        </Text>
      </View>

      <Switch
        value={allowMultiSelection}
        onValueChange={setAllowMultiSelection}
      ></Switch>

      <View style={{ width: "100%" }}>
        <Text style={{ fontSize: 20, fontWeight: "600", margin: 6 }}>
          Copy a file to a folder.
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
          Pick result.
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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-document-picker": "file:../../node_modules/@react-native-ohos/react-native-document-picker/harmony/document_picker.har"
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

### 2.3 Configuring CMakeLists and Introducing DocumentPickerPackage

> **[!TIP] Version v9.2.0 and above requires.**

Open entry/src/main/cpp/CMakeLists.txt and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-document-picker/src/main/cpp" ./document_picker)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_document_picker)
# RNOH_END: manual_package_linking_2
```

Open entry/src/main/cpp/PackageProvider.cpp and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "DocumentPickerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<DocumentPickerPackage>(ctx)
    };
}
```

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { DocumentPickerPackage } from '@react-native-ohos/react-native-document-picker/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new DocumentPickerPackage(ctx)
  ];
}
```

### 2.4 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints
### 3.1 Compatibility

Check the release version information in the release address of the third-party library:[@react-native-ohos/react-native-document-picker Releases](https://gitee.com/openharmony-sig/rntpc_react-native-document-picker/releases)


## 4. Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

Parameters of the option pick Method

| Name                | Description                                                                                                                                                                                         | Type                                                                    | Required | Platform    | HarmonyOS Support |
| ------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------- | -------- | ----------- | ----------------- |
| allowMultiSelection | Whether selecting multiple files is allowed. For pick, this is false by default. allowMultiSelection is false for pickSingle and cannot be overridden.                                              | boolean                                                                 | no       | IOS/Android | yes               |
| type                | The type or types of documents to allow selection of. An array of strings or single string.                                                                                                         | string or Array<string>                                                 | no       | IOS/Android | yes               |
| copyTo              | Copy the selected file to the specified folder.                                                                                                                                                     | "cachesDirectory" \| "documentDirectory"                                | no       | IOS/Android | yes               |
| presentationStyle   | Controls how the picker is presented, e.g. on an iPad you may want to present it fullscreen. Defaults to pageSheet.                                                                                 | 'fullScreen' \| 'pageSheet' \| 'formSheet' \| 'overFullScreen'          | no       | IOS         | no                |
| transitionStyle     | Configure the transition style of the picker. Defaults to coverVertical.                                                                                                                            | 'coverVertical' \| 'flipHorizontal' \| 'crossDissolve' \| 'partialCurl' | no       | IOS         | no                |
| mode                | Defaults to import. If mode is set to import the document picker imports the file from outside to inside the sandbox, otherwise if mode is set to open the document picker opens the file in-place. | "import" \| "open"                                                      | no       | IOS         | no                |

## 5. API

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

## 6. Known Issues

- [ ] The **pickerOpt. selectMode** API is invalid when it is set to **FOLDER** on HarmonyOS: [issue#1](https://github.com/react-native-oh-library/document-picker/issues/1).
- [ ] **releaseSecureAccess** cannot be used to select files outside the sandbox path. This API is not supported on HarmonyOS: [issue#2](https://github.com/react-native-oh-library/document-picker/issues/2).

## 7. Others

- The Gallery resources cannot be read or written due to permission issues. Selecting files from the Gallery is not supported in Files.

## 8. License

This project is licensed under [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-document-picker/blob/master/LICENSE.md).