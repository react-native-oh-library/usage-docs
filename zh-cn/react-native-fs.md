> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-fs</code> </h1>
</p>

本项目基于 [react-native-fs@2.20.0](https://github.com/itinance/react-native-fs) 开发。

| Version                     | Package Name                         | Repository                                                                       | Release                                                                                            |
| --------------------------- | ------------------------------------ | -------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| <= 2.20.0-0.1.14@deprecated | @react-native-oh-tpl/react-native-fs | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-fs) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-fs/releases) |
| >= 2.20.1                   | @react-native-ohos/react-native-fs   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-fs)                 | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-fs/releases)                 |

## 1. 安装与使用

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/react-native-fs": "file:../../node_modules/@react-native-ohos/react-native-fs/harmony/fs.har"
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

### 2.3. 配置 CMakeLists 和引入 RNFSPackage

> [!TIP] 版本 v2.20.1 及以上需要

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

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

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 2.4. 在 ArkTs 侧引入 FsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 2.5. 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性


请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-fs Releases](https://gitee.com/openharmony-sig/rntpc_react-native-fs/releases)

## 4. 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 5. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 6. 遗留问题

- [ ] HarmonyOS 的 hash 哈希 API 中关于算法参数 algorithm 目前仅支持"md5"、"sha1"、 "sha256"，其他相关算法参数目前不支持，问题: [issue#1](https://github.com/react-native-oh-library/react-native-fs/issues/1)
- [ ] 原库部分接口在 HarmonyOS 中没有对应文件路径常量及接口处理相关逻辑，问题: [issue#2](https://github.com/react-native-oh-library/react-native-fs/issues/2)

## 7. 其他

## 8. 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/itinance/react-native-fs/blob/master/LICENSE) ，请自由地享受和参与开源。
