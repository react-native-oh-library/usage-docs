> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-mlkit-ocr</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/agoldis/react-native-mlkit-ocr">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/agoldis/react-native-mlkit-ocr/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-mlkit-ocr)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-mlkit-ocr Releases](https://github.com/react-native-oh-library/react-native-mlkit-ocr/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-mlkit-ocr
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-mlkit-ocr
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import * as React from 'react';
import {
    StyleSheet,
    View,
    Button,
    SafeAreaView,
    ScrollView,
    Text,
    Dimensions,
    ActivityIndicator,
} from 'react-native';
import MlkitOcr, { MlkitOcrResult } from 'react-native-mlkit-ocr';
const styles = StyleSheet.create({
    container: {
        flex: 1,
        justifyContent: 'center',
    },
    scroll: {
        flex: 1,
        width: '100%',
        borderColor: '#ccc',
        borderWidth: 2,
    },
});
export const OcrTest = () => {
    const [loading, setLoading] = React.useState<boolean>(false);
    const [result, setResult] = React.useState<MlkitOcrResult | undefined>();

    if (loading) {
        return (
            <SafeAreaView style={styles.container}>
                <ActivityIndicator />
            </SafeAreaView>
        );
    }
    return (
        <SafeAreaView style={styles.container}>
            {Array.isArray(result) && result?.length && (
                <ScrollView
                    contentContainerStyle={{
                        alignItems: 'stretch',
                        padding: 20,
                        height: Dimensions.get('window').height,
                    }}
                    showsVerticalScrollIndicator
                    style={styles.scroll}
                >
                    {result?.map((block) => {
                        return block.lines.map((line) => {
                            return (
                                <View
                                    key={line.text}
                                    style={{
                                        backgroundColor: '#ccccccaf',
                                    }}
                                >
                                    <Text style={{ fontSize: 10 }}>{line.text}</Text>
                                </View>
                            );
                        });
                    })}
                </ScrollView>
            )}

            <Button
                title="识别网络照片"
                onPress={() => {
                    MlkitOcr.detectFromUri('https://res.vmallres.com//uomcdn/CN/pms/202407/E3B48F7290631FAF341FDB09CF907F03.jpg').then(res => {
                        setTimeout(() => {
                            setResult(res)
                            console.log("================uri=res", JSON.stringify(res))
                        }, 1000)
                    }).catch(err => {
                        console.log("=========err", err);
                    })
                }}
            />
            <Button
                title="识别本地照片"
                onPress={() => {
                    MlkitOcr.detectFromFile('file://docs/storage/Users/currentUser/test/1.jpg').then(res => {
                        setTimeout(() => {
                            setResult(res)
                            console.log("================file=res", JSON.stringify(res))
                        }, 1000)
                    }).catch(err => {
                        console.log("=========err", err);
                    })
                }}
            />
        </SafeAreaView>
    );
}
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-mlkit-ocr": "file:../../node_modules/@react-native-oh-tpl/react-native-mlkit-ocr/harmony/rn_mlkit_ocr.har"
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

### 3.配置 CMakeLists 和引入 RNMlkitOcrPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-oh-tpl/react-native-mlkit-ocr/src/main/cpp" ./rn_mlkit_ocr)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_mlkit_ocr)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "RNMlkitOcrPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<RNMlkitOcrPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNMlkitOcrPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
+ import { RNMlkitOcrPackage } from '@react-native-oh-tpl/react-native-mlkit-ocr/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNMlkitOcrPackage(ctx),
  ];
}
```

### 5.应用权限申请

> [!TIP] "ohos.permission.INTERNET"权限等级为<B>normal</B>，授权方式为<B>system_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+    {
+        "name": "ohos.permission.INTERNET",
+     },
    ]
  }
}
```



### 6.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-mlkit-ocr Releases](https://github.com/react-native-oh-library/react-native-mlkit-ocr/releases)



## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME         | Description                                                             | TYPE | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------ |--------------------------------- | ------ | -------- | -------- |
| detectFromUri(uri)| 传入网络图片地址 | Function  |Yes| All      | Yes      |
| detectFromFile(path) | 传入本地图片地址 | Function |Yes| All      | Yes      |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/agoldis/react-native-mlkit-ocr/blob/main/LICENSE) ，请自由地享受和参与开源。
