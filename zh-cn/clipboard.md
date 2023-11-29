<p align="center">
  <h1 align="center"> <code>@react-native-clipboard/clipboard</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-clipboard/clipboard">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20macos%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-clipboard/clipboard/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

> [!tip] 目前 React-Native-OpenHarmony(RNOH) 三方库的 npm 包部署在私仓，需要通过 github token 来获取访问权限。

在与 `package.json` 文件相同的目录中，创建或编辑 `.npmrc` 文件以包含指定 GitHub Packages URL 和托管包的命名空间的行。 将 TOKEN 替换为 RNOH 三方库指定的 token。

```json
@react-native-oh-library:registry=https://npm.pkg.github.com
//npm.pkg.github.com/:_authToken=TOKEN
```

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-clipboard/clipboard@npm:@react-native-oh-library/clipboard
```

或者

```bash
npm install @react-native-clipboard/clipboard@npm:@react-native-oh-library/clipboard
```

快速使用：

```js
import Clipboard from "@react-native-clipboard/clipboard";

const [copiedText, setCopiedText] = useState("");

const copyToClipboard = () => {
  Clipboard.setString("hello world");
};

const fetchCopiedText = async () => {
  const text = await Clipboard.getString();
  setCopiedText(text);
};

<View style={styles.container}>
  <TouchableOpacity onPress={copyToClipboard}>
    <Text>Click here to copy to Clipboard</Text>
  </TouchableOpacity>
  <TouchableOpacity onPress={fetchCopiedText}>
    <Text>View copied text</Text>
  </TouchableOpacity>

  <Text style={styles.copiedText}>{copiedText}</Text>
</View>;
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-clipboard": "file:../../node_modules/@react-native-clipboard/clipboard/harmony/clipboard.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码
打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-clipboard": "file:../../node_modules/@react-native-clipboard/clipboard/harmony/clipboard"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 ClipboardPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-clipboard/src/main/cpp" ./clipboard)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_clipboard)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ClipboardPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ClipboardPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 Clipboard 组件

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {ClipboardPackage} from 'rnoh-clipboard/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ClipboardPackage(ctx)
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

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

| `@react-native-oh-library/clipboard` Version | Required React Native Version | Required RNOH Version | Required DevEco Studio Version | Required ROM Version  |
| -------------------------------------------- | ----------------------------- | --------------------- | ------------------------------ | --------------------- |
| 1.12.1-0.0.1                                 | `0.72.5`                      | `0.72.9`              | `4.0.3.601`                    | `OpenHarmony 4.10.11` |

## 属性

| 名称        | 说明                                                                                                                                                                                                                      | 类型     | 是否必填 | 原库平台    | 鸿蒙支持 |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | -------- |
| getString   | Get content of string type, this method returns a Promise, so you can use following code to get clipboard content                                                                                                         | function | NO       | ios,android | yes      |
| setString   | Set content of string type. You can use following code to set clipboard content                                                                                                                                           | function | NO       | ios,android | yes      |
| hasString   | Returns whether the clipboard has content or is empty.                                                                                                                                                                    | function | NO       | ios,android | yes      |
| getImage    | Get content of image in base64 string type, this method returns a Promise, so you can use following code to get clipboard content (ANDROID only)                                                                          | function | NO       | android     | no       |
| getStrings  | (iOS only) Get contents of string array type, this method returns a Promise, so you can use following code to get clipboard content                                                                                       | function | NO       | ios         | yes      |
| setStrings  | (iOS only) Set content of string array type. You can use following code to set clipboard content                                                                                                                          | function | NO       | ios         | yes      |
| hasNumber   | (iOS 14+ only) Returns whether the clipboard has a Number(UIPasteboardDetectionPatternNumber) content. Can check if there is a Number content in clipboard without triggering PasteBoard notification for iOS 14+         | function | NO       | ios         | yes      |
| hasImage    | Returns whether the clipboard has a Image                                                                                                                                                                                 | function | NO       | ios         | no       |
| hasUrl      | (iOS only) Returns whether the clipboard has a URL content. Can check if there is a URL content in clipboard without triggering PasteBoard notification for iOS 14+                                                       | function | NO       | ios         | no       |
| hasWebUrl   | (iOS 14+ only) Returns whether the clipboard has a WebURL(UIPasteboardDetectionPatternProbableWebURL) content. Can check if there is a WebURL content in clipboard without triggering PasteBoard notification for iOS 14+ | function | NO       | ios         | yes      |
| setImage    | Set content of Image type.（base64 string）                                                                                                                                                                               | function | NO       | ios         | no       |
| getImageJPG | get base64 string of JPG Image                                                                                                                                                                                            | function | NO       | ios         | no       |
| getImagePNG | get base64 string of PNG Image                                                                                                                                                                                            | function | NO       | ios         | no       |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/clipboard/blob/harmony/LICENSE) ，请自由地享受和参与开源。
