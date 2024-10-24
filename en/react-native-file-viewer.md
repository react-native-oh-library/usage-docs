<!-- {% raw %} -->

> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-file-viewer
</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/vinzscam/react-native-file-viewer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-file-viewer)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-file-viewer Releases](https://github.com/react-native-oh-library/react-native-file-viewer/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-file-viewer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-file-viewer@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import { StyleSheet, ScrollView, Text, TouchableOpacity } from "react-native";
import DocumentPicker from "react-native-document-picker";
import FileViewer from "react-native-file-viewer";

export function FlieViewerExample() {
  const FileViewerTest = async (option?: any) => {
    try {
      const res: any = await DocumentPicker.pick({
        type: [DocumentPicker.types.allFiles],
      });
      await FileViewer?.open(res[0].uri, option);
    } catch (e) {
      // error
    }
  };

  const onDismissCb = () => {
    // do sth ...
  };

  return (
    <ScrollView style={{ backgroundColor: "skyblue" }}>
      <TouchableOpacity onPress={() => FileViewerTest()} style={styles.btn}>
        <Text style={styles.btnText}>Toogle Status Bar</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() => FileViewerTest("show_displayName string")}
        style={styles.btn}
      >
        <Text style={styles.btnText}>Toogle Status Bar (displayName str)</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() =>
          FileViewerTest({ displayName: "show_displayName option" })
        }
        style={styles.btn}
      >
        <Text style={styles.btnText}>Toogle Status Bar (displayName opt)</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() =>
          FileViewerTest({ showOpenWithDialog: true, onDismiss: onDismissCb })
        }
        style={styles.btn}
      >
        <Text style={styles.btnText}>Toogle Status Bar (onDismiss)</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() => FileViewerTest({ showOpenWithDialog: true })}
        style={styles.btn}
      >
        <Text style={styles.btnText}>
          Toogle Status Bar (showOpenWithDialog)
        </Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={() => FileViewerTest({ showAppsSuggestions: true })}
        style={styles.btn}
      >
        <Text style={styles.btnText}>
          Toogle Status Bar (showAppsSuggestions)
        </Text>
      </TouchableOpacity>
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
  btnText: {
    fontWeight: "bold",
    color: "#fff",
    fontSize: 20,
  },
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
    "@react-native-oh-tpl/react-native-file-viewer": "file:../../node_modules/@react-native-oh-tpl/react-native-file-viewer/harmony/file_viewer.har"
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

### 3. Introducing RNFileViewerTurboModule Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { RNFileViewerPackage } from '@react-native-oh-tpl/react-native-file-viewer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFileViewerPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-file-viewer Releases](https://github.com/react-native-oh-library/react-native-file-viewer/releases)

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

### `open(filepath: string, options?: Object): Promise<void>`

| Name                   | Description                                                                                                                                                                                                                                        | Type   | Required | Platform | HarmonyOS Support |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------ | -------- | -------- | ----------------- |
| **filepath**           | The absolute path where the file is stored. The file needs to have a valid extension to be successfully detected. Use [react-native-fs constants](https://github.com/itinance/react-native-fs#constants) to determine the absolute path correctly. | string | yes      | All      | yes               |
| **options** (optional) | Some options to customize the behaviour. See below.                                                                                                                                                                                                | Object | no       | All      | yes               |

#### Options

| Name                               | Description                                                                                       | Type     | Required | Platform | HarmonyOS Support |
| ---------------------------------- | ------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| **displayName** (optional)         | Customize the QuickLook title.                                                                    | string   | no       | iOS      | yes               |
| **onDismiss** (optional)           | Callback invoked when the viewer is being dismissed.                                              | function | no       | All      | partially         |
| **showOpenWithDialog** (optional)  | If there is more than one app that can open the file, show an _Open With_ dialogue box.           | boolean  | no       | Android  | yes               |
| **showAppsSuggestions** (optional) | If there is not an installed app that can open the file, open the Play Store with suggested apps. | boolean  | no       | Android  | partially         |

## Known Issues

- [x] HarmonyOS 端暂不支持关闭预览窗口的回调函数调用: [issue#1](https://github.com/react-native-oh-library/react-native-file-viewer/issues/4)
- [x] HarmonyOS 端无法直接跳转到应用市场的推荐应用页，目前只能跳转到应用市场首页: [issue#2](https://github.com/react-native-oh-library/react-native-file-viewer/issues/5)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/vinzscam/react-native-file-viewer/blob/master/LICENSE).

<!-- {% endraw %} -->
