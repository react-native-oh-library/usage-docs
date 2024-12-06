> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-fs</code> </h1>
</p>
This project is based on [react-native-fs@2.20.0](https://github.com/itinance/react-native-fs)。

| Version                     | Package Name                         | Repository                                                                       | Release                                                                                            |
| --------------------------- | ------------------------------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| <= 2.20.0-0.1.14@deprecated | @react-native-oh-tpl/react-native-fs | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-fs) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-fs/releases) |
| >= 2.20.1                   | @react-native-ohos/react-native-fs   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-fs)                 | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-fs/releases)                 |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-ohos/react-native-fs
```

#### yarn

```bash
yarn add @react-native-ohos/react-native-fs
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState } from "react";
import { SafeAreaView, StyleSheet, ScrollView, View, Text, StatusBar, TextInput, Button } from "react-native";
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
        <ScrollView contentInsetAdjustmentBehavior="automatic" style={styles.scrollView}>
          <Text style={styles.sectionTitle}>{"React Native File Harmony Demo App"}</Text>
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
              <Button title="Create Directory" color="#9a73ef" onPress={mkdirExample} />
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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

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
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-fs": "file:../../node_modules/@react-native-ohos/react-native-fs/harmony/fs.har"
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

### 2.3 Configuring CMakeLists and Introducing RNFSPackage

> [!TIP] Required for version `v2.20.1` and above

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-fs/src/main/cpp" ./fs)
# RNOH_END: manual_package_linking_1

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_fs)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNFSPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNFSPackage>(ctx)
    };
}
```

### 2.4. Introducing FsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
import type { RNPackageContext, RNPackage } from 'rnoh/ts';
  ...
+ import { FsPackage } from '@react-native-ohos/react-native-fs/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FsPackage(ctx)
  ];
}
```

### 2.5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

Check the release version information in the release address of the third-party library:[@react-native-ohos/react-native-fs Releases](https://gitee.com/openharmony-sig/rntpc_react-native-fs/releases)

## 4. Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                         | Description | Type   | Required | Platform        | HarmonyOS Support | Remark                   |
| :--------------------------- | ----------- | ------ | -------- | --------------- | ----------------- | ------------------------ |
| DocumentDirectoryPath        | System Path | string | No       | iOS/Android     | yes               |                          |
| CachesDirectoryPath          | System Path | string | No       | iOS/Android     | yes               |                          |
| MainBundlePath               | System Path | string | No       | iOS             | yes               |                          |
| ExternalCachesDirectoryPath  | System Path | string | No       | Android         | No                | Android only             |
| DownloadDirectoryPath        | System Path | string | No       | Android/Windows | No                | not available on Harmony |
| TemporaryDirectoryPath       | System Path | string | No       | iOS/Android     | yes               |                          |
| LibraryDirectoryPath         | System Path | string | No       | iOS             | yes               |                          |
| ExternalDirectoryPath        | System Path | string | No       | Android         | No                | Android only             |
| ExternalStorageDirectoryPath | System Path | string | No       | Android         | No                | Android only             |
| PicturesDirectoryPath        | System Path | string | No       | Windows         | No                | Windows only             |
| RoamingDirectoryPath         | System Path | string | No       | Windows         | No                | Windows only             |

## 5. APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description                                                                                                                                                                   | Type     | Platform    | Required | HarmonyOS Support | Remark            |
| ----------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | ----------- | -------- | ----------------- | ----------------- |
| mkdir                   | Create a directory at `filepath`.                                                                                                                                             | function | Android     | No       | yes               |                   |
| exists                  | Check if the item exists at `filepath`.                                                                                                                                       | function | iOS/Android | No       | yes               |                   |
| readFile                | Reads the file at `path` and return contents.                                                                                                                                 | function | iOS/Android | No       | yes               |                   |
| readFileAssets          | Reads the file at `path` in the harmony app's assets folder and return contents.                                                                                              | function | Android     | No       | yes               |                   |
| writeFile               | Write the `contents` to `filepath`.                                                                                                                                           | function | iOS/Android | No       | yes               |                   |
| appendFile              | Append the `contents` to `filepath`.                                                                                                                                          | function | iOS/Android | No       | yes               |                   |
| copyFile                | Copies the file located at `filepath` to `destPath`.                                                                                                                          | function | iOS         | No       | yes               |                   |
| unlink                  | Unlinks the item at `filepath`.                                                                                                                                               | function | iOS/Android | No       | yes               |                   |
| hash                    | Reads the file at `path` and returns its checksum as determined by `algorithm`, which can be one of `md5`, `sha1`, `sha256`.                                                  | function | iOS/Android | No       | partially         |                   |
| moveFile                | Moves the file located at `filepath` to `destPath`.                                                                                                                           | function | iOS/Android | No       | yes               |                   |
| read                    | Reads `length` bytes from the given `position` of the file at `path` and returns contents.                                                                                    | function | iOS/Android | No       | yes               |                   |
| write                   | Write the `contents` to `filepath` at the given random access position.                                                                                                       | function | iOS/Android | No       | yes               |                   |
| touch                   | Sets the modification timestamp `mtime`of the file at `filepath`.                                                                                                             | function | iOS/Android | No       | partially         |                   |
| stat                    | Stats an item at `filepath`.                                                                                                                                                  | function | iOS/Android | No       | yes               |                   |
| readDir                 | Reads the contents of `path`.                                                                                                                                                 | function | iOS/Android | No       | yes               |                   |
| readDirAssets           | Reads the contents of `dirpath ` in the Android app's assets folder.                                                                                                          | function | Android     | No       | No                | Android only      |
| readdir                 | Node.js style version of `readDir` that returns only the names.                                                                                                               | function | iOS/Android | No       | No                | No API on Harmony |
| readFileRes             | Reads the file named `filename` in the Android app's `res` folder and return contents.                                                                                        | function | Android     | No       | No                | Android only      |
| copyFolder              | Copies the contents located at `srcFolderPath` to `destFolderPath`.                                                                                                           | function | Windows     | No       | No                | Windows only      |
| copyFileAssets          | Copies the file at `filepath` in the Android app's assets folder and copies it to the given `destPath ` path.                                                                 | function | Android     | No       | No                | Android only      |
| copyFileRes             | Copies the file named `filename` in the Android app's res folder and copies it to the given `destPath ` path.                                                                 | function | Android     | No       | No                | Android only      |
| copyAssetsFileIOS       | Reads an image file from Camera Roll and writes to `destPath`.                                                                                                                | function | iOS         | No       | No                | iOS only          |
| copyAssetsVideoIOS      | Copies a video from assets-library, that is prefixed with 'assets-library://asset/asset.MOV?...' to a specific destination.                                                   | function | iOS         | No       | No                | iOS only          |
| existsAssets            | Check in the Android assets folder if the item exists.                                                                                                                        | function | Android     | No       | yes               |                   |
| existsRes               | Check in the Android res folder if the item named `filename` exists.                                                                                                          | function | Android     | No       | No                | Android only      |
| downloadFile            | Abort the current download job with this ID.                                                                                                                                  | function | iOS/Android | No       | yes               |                   |
| stopDownload            | Abort the current download job with this ID.                                                                                                                                  | function | iOS/Android | No       | No                | No API on Harmony |
| resumeDownload          | Resume the current download job with this ID.                                                                                                                                 | function | iOS         | No       | No                | iOS only          |
| isResumable             | Check if the the download job with this ID is resumable with `resumeDownload()`.                                                                                              | function | iOS         | No       | No                | iOS only          |
| completeHandlerIOS      | For use when using background downloads, tell iOS you are done handling a completed download.                                                                                 | function | iOS         | No       | No                | iOS only          |
| uploadFiles             | Percentage can be computed easily by dividing `totalBytesSent` by `totalBytesExpectedToSend`.                                                                                 | function | iOS/Android | No       | No                | No API on Harmony |
| stopUpload              | Abort the current upload job with this ID.                                                                                                                                    | function | iOS         | No       | No                | iOS only          |
| getFSInfo               | Returns an object with the following properties.                                                                                                                              | function | iOS/Android | No       | No                | No API on Harmony |
| scanFile                | Scan the file using [Media Scanner](https://developer.android.com/reference/android/media/MediaScannerConnection).                                                            | function | Android     | No       | No                | Android only      |
| getAllExternalFilesDirs | Returns an array with the absolute paths to application-specific directories on all shared/external storage devices where the application can place persistent files it owns. | function | Android     | No       | No                | Android only      |
| pathForGroup            | Returns the absolute path to the directory shared for all applications with the same security group identifier.                                                               | function | iOS         | No       | No                | iOS only          |

## 6. Known Issues

- [ ] The algorithm parameter algorithm in the hash API of HarmonyOS currently only supports "md5", "sha1", and "sha256". Other related algorithm parameters are currently not supported. Problem: [issue#1](https://github.com/react-native-oh-library/react-native-fs/issues/1)
- [ ] Some interfaces in the original library do not have corresponding file path constants and interface processing related logic in HarmonyOS. Problem:[issue#2](https://github.com/react-native-oh-library/react-native-fs/issues/2)

## 7. Others

## 8. License

This project is licensed under [The MIT License (MIT)](https://github.com/itinance/react-native-fs/blob/master/LICENSE).
