> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/clipboard/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/clipboard Releases](https://github.com/react-native-oh-library/clipboard/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/clipboard
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/clipboard
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

const App = () => {
  return (
    <View style={styles.container}>
      <TouchableOpacity onPress={copyToClipboard}>
        <Text>Click here to copy to Clipboard</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={fetchCopiedText}>
        <Text>View copied text</Text>
      </TouchableOpacity>

      <Text style={styles.copiedText}>{copiedText}</Text>
    </View>
  );
};

export default App;
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/clipboard": "file:../../node_modules/@react-native-oh-tpl/clipboard/harmony/clipboard.har"
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

### 3.配置 CMakeLists 和引入 ClipboardPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/clipboard/src/main/cpp" ./clipboard)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_clipboard)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ClipboardPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<ClipboardPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 ClipboardPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {ClipboardPackage} from '@react-native-oh-tpl/clipboard/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ClipboardPackage(ctx)
  ];
}

```

### 5.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/clipboard Releases](https://github.com/react-native-oh-library/clipboard/releases)

### 权限要求

> [!TIP] "ohos.permission.READ_PASTEBOARD"权限等级为<B>system_basic</B>，授权方式为<B>user_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.READ_PASTEBOARD",
+    "reason": "$string:Access_clipboard",
+    "usedScene": {
+      "abilities": [
+        "EntryAbility"
+      ],
+      "when":"always"
+    }
+  },
]
```

#### 在 entry 目录下添加申请剪切板权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "Access_clipboard",
+      "value": "access clipboard"
+    }
  ]
}
```

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                                                                                                                                                                               | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | ----------- | ----------------- |
| getString   | Get content of string type, this method returns a Promise, so you can use following code to get clipboard content                                                                                                         | function | NO       | iOS,Android | yes               |
| setString   | Set content of string type. You can use following code to set clipboard content                                                                                                                                           | function | NO       | iOS,Android | yes               |
| hasString   | Returns whether the clipboard has content or is empty.                                                                                                                                                                    | function | NO       | iOS,Android | yes               |
| getImage    | Get content of image in base64 string type, this method returns a Promise, so you can use following code to get clipboard content (ANDROID only)                                                                          | function | NO       | Android     | no                |
| getStrings  | (iOS only) Get contents of string array type, this method returns a Promise, so you can use following code to get clipboard content                                                                                       | function | NO       | iOS        | yes                |
| setStrings  | (iOS only) Set content of string array type. You can use following code to set clipboard content                                                                                                                          | function | NO       | iOS        | yes                |
| hasNumber   | (iOS 14+ only) Returns whether the clipboard has a Number(UIPasteboardDetectionPatternNumber) content. Can check if there is a Number content in clipboard without triggering PasteBoard notification for iOS 14+         | function | NO       | iOS        | yes               |
| hasImage    | Returns whether the clipboard has a Image                                                                                                                                                                                 | function | NO       | iOS        | yes               |
| hasUrl      | (iOS only) Returns whether the clipboard has a URL content. Can check if there is a URL content in clipboard without triggering PasteBoard notification for iOS 14+                                                       | function | NO       | iOS        | yes                |
| hasWebUrl   | (iOS 14+ only) Returns whether the clipboard has a WebURL(UIPasteboardDetectionPatternProbableWebURL) content. Can check if there is a WebURL content in clipboard without triggering PasteBoard notification for iOS 14+ | function | NO       | iOS        | yes               |
| setImage    | Set content of Image type.（base64 string）                                                                                                                                                                               | function | NO       | iOS        | yes               |
| getImageJPG | get base64 string of JPG Image                                                                                                                                                                                            | function | NO       | iOS        | yes               |
| getImagePNG | get base64 string of PNG Image                                                                                                                                                                                            | function | NO       | iOS        | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-clipboard/clipboard/blob/master/LICENSE) ，请自由地享受和参与开源。
