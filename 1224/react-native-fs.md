> 模板版本：v0.1.3

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
    const [mkdirParam, setMkdirParam] = useState('');
    const mkdirExample = () => {
      FS.mkdir(mkdirParam).then((result) => {
        console.log('mkdir mkdirParam： '+mkdirParam);
        console.log('mkdir Successfully created directory.');
      }, err => {
        console.error('mkdir mkdir: '+ err.message)
      });
    }
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

| Name            | Description | Type   | Required | Platform    | HarmonyOS Support |
| --------------- | ----------- | ------ | -------- | ----------- | ----------------- |
| FileSandBoxPath | System Path | string | No       | IOS/Android | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-fs](https://github.com/react-native-oh-library/react-native-fs)

| Name           | Description                                                  | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ------------------------------------------------------------ | ------ | -------- | ----------- | ----------------- |
| mkdir          | Create a directory at `filepath`.                            | string | No       | Android     | yes               |
| exists         | Check if the item exists at `filepath`.                      | string | No       | IOS/Android | yes               |
| readFile       | Reads the file at `path` and return contents.                | string | No       | IOS/Android | yes               |
| readFileAssets | Reads the file at `path` in the harmony app's assets folder and return contents. | string | No       | Android     | yes               |
| writeFile      | Write the `contents` to `filepath`.                          | string | No       | IOS/Android | yes               |
| appendFile     | Append the `contents` to `filepath`.                         | string | No       | IOS/Android | yes               |
| copyFile       | Copies the file located at `filepath` to `destPath`.         | string | No       | IOS         | yes               |
| unlink         | Unlinks the item at `filepath`.                              | string | No       | IOS/Android | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/itinance/react-native-fs/blob/master/LICENSE) ，请自由地享受和参与开源。