> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fs</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/itinance/react-native-fs">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-fs/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-fs)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-library/react-native-fs Releases](https://github.com/react-native-oh-library/react-native-fs/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-fs
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-fs
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import {
  SafeAreaView,
  StyleSheet,
  ScrollView,
  View,
  Text,
  StatusBar,
  TextInput,
  Button,
} from "react-native";
import FS from "react-native-fs";
import { Colors } from "react-native/Libraries/NewAppScreen";
function App(): React.JSX.Element {
  const [mkdirParam, setMkdirParam] = useState("");
  const mkdirExample = () => {
    FS.mkdir(FS.DocumentDirectoryPath + "/" + mkdirParam).then(
      (result) => {
        console.log("file mkdirParam： " + mkdirParam);
        console.log("file Successfully created directory.");
      },
      (err) => {
        console.error("file mkdir: " + err.message);
      }
    );
  };

  return (
    <>
      <StatusBar barStyle="dark-content" />
      <SafeAreaView>
        <ScrollView
          contentInsetAdjustmentBehavior="automatic"
          style={styles.scrollView}
        >
          <Text style={styles.sectionTitle}>
            {"React Native File Harmony Demo App"}
          </Text>
          <View style={styles.body}>
            <View style={styles.sectionContainer}>
              <Text style={styles.sectionTitle}>{"mkdir"}</Text>
              <View style={styles.sectionDescription}>
                <TextInput
                  style={styles.input}
                  placeholder="Folder Path"
                  onChangeText={(mkdirParam) => setMkdirParam(mkdirParam)}
                  placeholderTextColor="#9a73ef"
                  autoCapitalize="none"
                />
              </View>
              <Button
                title="Create Directory"
                color="#9a73ef"
                onPress={mkdirExample}
              />
            </View>
          </View>
        </ScrollView>
      </SafeAreaView>
    </>
  );
}

const styles = StyleSheet.create({
  scrollView: {
    backgroundColor: Colors.black,
  },
  engine: {
    position: "absolute",
    right: 0,
  },
  body: {
    backgroundColor: Colors.dark,
  },
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: "600",
    color: Colors.white,
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: "400",
    color: Colors.dark,
  },
  input: {
    marginTop: 12,
  },
});

export default App;
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
    "@react-native-oh-tpl/react-native-fs": "file:../../node_modules/@react-native-oh-tpl/react-native-fs/harmony/fs.har"
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


### 3.Introducing FsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import type { RNPackageContext, RNPackage } from 'rnoh/ts';
  ...
+ import { FsPackage } from '@react-native-oh-tpl/react-native-fs/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FsPackage(ctx)
  ];
}
```

### 4.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-fs Releases](https://github.com/react-native-oh-library/react-native-fs/releases)

## Static Methods

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                         | Description | Type   | Required | Platform        | HarmonyOS Support | Remark                   |
| :--------------------------- | ----------- | ------ | -------- | --------------- | ----------------- | ------------------------ |
| DocumentDirectoryPath        | System Path | string | No       | IOS/Android     | yes               |                          |
| CachesDirectoryPath          | System Path | string | No       | IOS/Android     | yes               |                          |
| MainBundlePath               | System Path | string | No       | IOS             | yes               |                          |
| ExternalCachesDirectoryPath  | System Path | string | No       | Android         | No                | Android only             |
| DownloadDirectoryPath        | System Path | string | No       | Android/Windows | No                | not available on Harmony |
| TemporaryDirectoryPath       | System Path | string | No       | IOS/Android     | yes               |                          |
| LibraryDirectoryPath         | System Path | string | No       | IOS             | yes               |                          |
| ExternalDirectoryPath        | System Path | string | No       | Android         | No                | Android only             |
| ExternalStorageDirectoryPath | System Path | string | No       | Android         | No                | Android only             |
| PicturesDirectoryPath        | System Path | string | No       | Windows         | No                | Windows only             |
| RoamingDirectoryPath         | System Path | string | No       | Windows         | No                | Windows only             |

## APIs

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                                                  | Type     | Platform    | Required | HarmonyOS Support | Remark            |
| ----------------------- | ------------------------------------------------------------ | -------- | ----------- | -------- | ----------------- | ----------------- |
| mkdir                   | Create a directory at `filepath`.                            | function | Android     | No       | yes               |                   |
| exists                  | Check if the item exists at `filepath`.                      | function | IOS/Android | No       | yes               |                   |
| readFile                | Reads the file at `path` and return contents.                | function | IOS/Android | No       | yes               |                   |
| readFileAssets          | Reads the file at `path` in the harmony app's assets folder and return contents. | function | Android     | No       | yes               |                   |
| writeFile               | Write the `contents` to `filepath`.                          | function | IOS/Android | No       | yes               |                   |
| appendFile              | Append the `contents` to `filepath`.                         | function | IOS/Android | No       | yes               |                   |
| copyFile                | Copies the file located at `filepath` to `destPath`.         | function | IOS         | No       | yes               |                   |
| unlink                  | Unlinks the item at `filepath`.                              | function | IOS/Android | No       | yes               |                   |
| hash                    | Reads the file at `path` and returns its checksum as determined by `algorithm`, which can be one of `md5`, `sha1`, `sha256`. | function | IOS/Android | No       | partially         |                   |
| moveFile                | Moves the file located at `filepath` to `destPath`.          | function | IOS/Android | No       | yes               |                   |
| read                    | Reads `length` bytes from the given `position` of the file at `path` and returns contents. | function | IOS/Android | No       | yes               |                   |
| write                   | Write the `contents` to `filepath` at the given random access position. | function | IOS/Android | No       | yes               |                   |
| touch                   | Sets the modification timestamp `mtime`of the file at `filepath`. | function | IOS/Android | No       | partially         |                   |
| stat                    | Stats an item at `filepath`.                                 | function | IOS/Android | No       | yes               |                   |
| readDir                 | Reads the contents of `path`.                                | function | IOS/Android | No       | yes               |                   |
| readDirAssets           | Reads the contents of `dirpath ` in the Android app's assets folder. | function | Android     | No       | No                | Android only      |
| readdir                 | Node.js style version of `readDir` that returns only the names. | function | IOS/Android | No       | No                | No API on Harmony |
| readFileRes             | Reads the file named `filename` in the Android app's `res` folder and return contents. | function | Android     | No       | No                | Android only      |
| copyFolder              | Copies the contents located at `srcFolderPath` to `destFolderPath`. | function | Windows     | No       | No                | Windows only      |
| copyFileAssets          | Copies the file at `filepath` in the Android app's assets folder and copies it to the given `destPath ` path. | function | Android     | No       | No                | Android only      |
| copyFileRes             | Copies the file named `filename` in the Android app's res folder and copies it to the given `destPath ` path. | function | Android     | No       | No                | Android only      |
| copyAssetsFileIOS       | Reads an image file from Camera Roll and writes to `destPath`. | function | IOS         | No       | No                | IOS only          |
| copyAssetsVideoIOS      | Copies a video from assets-library, that is prefixed with 'assets-library://asset/asset.MOV?...' to a specific destination. | function | IOS         | No       | No                | IOS only          |
| existsAssets            | Check in the Android assets folder if the item exists.       | function | Android     | No       | yes               |                   |
| existsRes               | Check in the Android res folder if the item named `filename` exists. | function | Android     | No       | No                | Android only      |
| downloadFile            | Abort the current download job with this ID.                 | function | IOS/Android | No       | yes               |                   |
| stopDownload            | Abort the current download job with this ID.                 | function | IOS/Android | No       | No                | No API on Harmony |
| resumeDownload          | Resume the current download job with this ID.                | function | IOS         | No       | No                | IOS only          |
| isResumable             | Check if the the download job with this ID is resumable with `resumeDownload()`. | function | IOS         | No       | No                | IOS only          |
| completeHandlerIOS      | For use when using background downloads, tell iOS you are done handling a completed download. | function | IOS         | No       | No                | IOS only          |
| uploadFiles             | Percentage can be computed easily by dividing `totalBytesSent` by `totalBytesExpectedToSend`. | function | IOS/Android | No       | No                | No API on Harmony |
| stopUpload              | Abort the current upload job with this ID.                   | function | IOS         | No       | No                | IOS only          |
| getFSInfo               | Returns an object with the following properties.             | function | IOS/Android | No       | No                | No API on Harmony |
| scanFile                | Scan the file using [Media Scanner](https://developer.android.com/reference/android/media/MediaScannerConnection). | function | Android     | No       | No                | Android only      |
| getAllExternalFilesDirs | Returns an array with the absolute paths to application-specific directories on all shared/external storage devices where the application can place persistent files it owns. | function | Android     | No       | No                | Android only      |
| pathForGroup            | Returns the absolute path to the directory shared for all applications with the same security group identifier. | function | IOS         | No       | No                | IOS only          |

## Known Issues

- [ ] HarmonyOS 的 hash 哈希 API 中关于算法参数 algorithm 目前仅支持"md5"、"sha1"、 "sha256"，其他相关算法参数目前不支持，问题: [issue#1](https://github.com/react-native-oh-library/react-native-fs/issues/1)
- [ ] 原库部分接口在 HarmonyOS 中没有对应文件路径常量及接口处理相关逻辑，问题: [issue#2](https://github.com/react-native-oh-library/react-native-fs/issues/2)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/itinance/react-native-fs/blob/master/LICENSE).
