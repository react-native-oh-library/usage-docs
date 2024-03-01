模板版本：v0.1.3

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-fs)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-library/react-native-fs> Releases](https://github.com/react-native-oh-library/react-native-fs/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-fs@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-fs@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React , { useState } from 'react';
import {
    SafeAreaView,
    StyleSheet,
    ScrollView,
    View,
    Text,
    StatusBar,
    TextInput,
    Button
} from 'react-native';
import FS from 'react-native-fs';
import { Colors} from 'react-native/Libraries/NewAppScreen';
function App(): React.JSX.Element {
    // 参数
    const [mkdirParam, setMkdirParam] = useState('');
    // 创建文件夹接口调用
    const mkdirExample = () => {
      FS.mkdir(FS.DocumentDirectoryPath + '/' + mkdirParam).then((result) => {
        console.log('file mkdirParam： '+ mkdirParam);
        console.log('file Successfully created directory.');
      }, err => {
        console.error('file mkdir: '+ err.message)
      });
    }
    // 组件
    return (
      <>
      <StatusBar barStyle="dark-content" />
      <SafeAreaView>
        <ScrollView
          contentInsetAdjustmentBehavior="automatic"
          style={styles.scrollView}>
          <Text style={styles.sectionTitle}>
            {"React Native File Harmony Demo App"}
          </Text>
          <View style={styles.body}>
            <View style={styles.sectionContainer}>
            <Text style={styles.sectionTitle}>
              {"mkdir"}
            </Text>
              <View style={styles.sectionDescription}>
              <TextInput style = {styles.input}
                placeholder = "Folder Path"
                onChangeText={mkdirParam => setMkdirParam(mkdirParam)}
                placeholderTextColor = "#9a73ef"
                autoCapitalize = "none"
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
 // 组件样式
 const styles = StyleSheet.create({
    scrollView: {
      backgroundColor: Colors.black,
    },
    engine: {
      position: 'absolute',
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
      fontWeight: '600',
      color: Colors.white,
    },
    sectionDescription: {
      marginTop: 8,
      fontSize: 18,
      fontWeight: '400',
      color: Colors.dark,
    },
    input: {
      marginTop: 12,
    },
  });
  
  export default App;
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-fs": "file:../../node_modules/@react-native-oh-tpl/react-native-fs/harmony/fs.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-fs": "file:../../node_modules/@react-native-oh-tpl/react-native-fs/harmony/fs"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

###  配置 CMakeLists 和引入 FsPackge

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
txtproject(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-fs/src/main/cpp" ./fs)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_fs)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "FsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<FsPackage>(ctx),
    };
}
```

### 在 ArkTs 侧引入 FsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { FsPackage } from 'rnoh-fs/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new FsPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<@react-native-oh-library/react-native-fs> Releases](https://github.com/react-native-oh-library/react-native-fs/releases)

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-fs](https://github.com/react-native-oh-library/react-native-fs)

| Name                         | Description | Type   | Required | Platform        | HarmonyOS Support | Remark                   |
| :--------------------------- | ----------- | ------ | -------- | --------------- | ----------------- | ------------------------ |
| DocumentDirectoryPath        | System Path | string | No       | IOS/Android     | yes               | No                       |
| CachesDirectoryPath          | System Path | string | No       | IOS/Android     | yes               | No                       |
| MainBundlePath               | System Path | string | No       | IOS             | No                | not available on Harmony |
| ExternalCachesDirectoryPath  | System Path | string | No       | Android         | No                | Android only             |
| DownloadDirectoryPath        | System Path | string | No       | Android/Windows | No                | not available on Harmony |
| TemporaryDirectoryPath       | System Path | string | No       | IOS/Android     | No                | not available on Harmony |
| LibraryDirectoryPath         | System Path | string | No       | IOS             | No                | IOS only                 |
| ExternalDirectoryPath        | System Path | string | No       | Android         | No                | Android only             |
| ExternalStorageDirectoryPath | System Path | string | No       | Android         | No                | Android only             |
| PicturesDirectoryPath        | System Path | string | No       | Windows         | No                | Windows only             |
| RoamingDirectoryPath         | System Path | string | No       | Windows         | No                | Windows only             |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-fs](https://github.com/react-native-oh-library/react-native-fs)

| Name                    | Description                                                  | Type     | Platform    | Required | HarmonyOS Support | Remark            |
| ----------------------- | ------------------------------------------------------------ | -------- | ----------- | -------- | ----------------- | ----------------- |
| mkdir                   | Create a directory at `filepath`.                            | function | Android     | No       | yes               | No                |
| exists                  | Check if the item exists at `filepath`.                      | function | IOS/Android | No       | yes               | No                |
| readFile                | Reads the file at `path` and return contents.                | function | IOS/Android | No       | yes               | No                |
| readFileAssets          | Reads the file at `path` in the harmony app's assets folder and return contents. | function | Android     | No       | yes               | No                |
| writeFile               | Write the `contents` to `filepath`.                          | function | IOS/Android | No       | yes               | No                |
| appendFile              | Append the `contents` to `filepath`.                         | function | IOS/Android | No       | yes               | No                |
| copyFile                | Copies the file located at `filepath` to `destPath`.         | function | IOS         | No       | yes               | No                |
| unlink                  | Unlinks the item at `filepath`.                              | function | IOS/Android | No       | yes               | No                |
| hash                    | Reads the file at `path` and returns its checksum as determined by `algorithm`, which can be one of `md5`, `sha1`, `sha256`. | function | IOS/Android | No       | partially         | No                |
| moveFile                | Moves the file located at `filepath` to `destPath`.          | function | IOS/Android | No       | yes               | No                |
| read                    | Reads `length` bytes from the given `position` of the file at `path` and returns contents. | function | IOS/Android | No       | yes               | No                |
| write                   | Write the `contents` to `filepath` at the given random access position. | function | IOS/Android | No       | yes               | No                |
| touch                   | Sets the modification timestamp `mtime`of the file at `filepath`. | function | IOS/Android | No       | partially         | No                |
| stat                    | Stats an item at `filepath`.                                 | function | IOS/Android | No       | yes               | No                |
| readDir                 | Reads the contents of `path`.                                | function | IOS/Android | No       | No                | No API on Harmony |
| readDirAssets           | Reads the contents of `dirpath ` in the Android app's assets folder. | function | Android     | No       | No                | Android only      |
| readdir                 | Node.js style version of `readDir` that returns only the names. | function | IOS/Android | No       | No                | No API on Harmony |
| readFileRes             | Reads the file named `filename` in the Android app's `res` folder and return contents. | function | Android     | No       | No                | Android only      |
| copyFolder              | Copies the contents located at `srcFolderPath` to `destFolderPath`. | function | Windows     | No       | No                | Windows only      |
| copyFileAssets          | Copies the file at `filepath` in the Android app's assets folder and copies it to the given `destPath ` path. | function | Android     | No       | No                | Android only      |
| copyFileRes             | Copies the file named `filename` in the Android app's res folder and copies it to the given `destPath ` path. | function | Android     | No       | No                | Android only      |
| copyAssetsFileIOS       | Reads an image file from Camera Roll and writes to `destPath`. | function | IOS         | No       | No                | IOS only          |
| copyAssetsVideoIOS      | Copies a video from assets-library, that is prefixed with 'assets-library://asset/asset.MOV?...' to a specific destination. | function | IOS         | No       | No                | IOS only          |
| existsAssets            | Check in the Android assets folder if the item exists.       | function | Android     | No       | No                | Android only      |
| existsRes               | Check in the Android res folder if the item named `filename` exists. | function | Android     | No       | No                | Android only      |
| downloadFile            | Abort the current download job with this ID.                 | function | IOS/Android | No       | No                | No API on Harmony |
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

##  遗留问题

- HarmonyOS的hash哈希API中关于算法参数algorithm目前仅支持"md5"、"sha1"  "sha256"，其他相关算法参数目前不支持，问题: [issue#1](https://github.com/react-native-oh-library/react-native-fs/issues/1)
- 原库部分接口在HarmonyOS中没有对应文件路径常量及接口处理相关逻辑，问题: [issue#2](https://github.com/react-native-oh-library/react-native-fs/issues/2)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/itinance/react-native-fs/blob/master/LICENSE) ，请自由地享受和参与开源。