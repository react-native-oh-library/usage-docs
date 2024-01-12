> 模板版本：v0.1.2

<p align="center">
  <h1 align="center"> <code>react-native-view-shot</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/gre/react-native-view-shot">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/gre/react-native-view-shot/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-view-shot)

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

**正在 npm 发布中，当前请先从仓库[Releases](https://github.com/react-native-oh-library/react-native-view-shot/releases)中获取库 tgz，通过使用本地依赖来安装本库。**

#### **yarn**

```bash
yarn add xxx
```

#### **npm**

```bash
npm install xxx
```

<!-- tabs:end -->

快速使用：

```js
import React from "react";
import { View, Text, Button } from "react-native";
import { captureRef, captureScreen } from "react-native-view-shot";

export default function App() {
  const view = React.useRef < View > null;
  return (
    <View>
      <View ref={view} collapsable={false} style={{ backgroudColor: "#FFF" }}>
        <Text style={{ color: "#000", marginBottom: 30 }}>
          Hello OpenHarmony
        </Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>Hello HarmonyOS</Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>
          Hello HarmonyOS Next
        </Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>Hello World</Text>
      </View>
      <View>
        <Button
          title="captureRef"
          onPress={() => {
            captureRef(view).then((uri) => {
              console.info(`captureRef: ${uri}`);
            });
          }}
        />
        <Button
          title="captureScreen"
          onPress={() => {
            captureScreen().then((str) => {
              console.info(`captureScreen: ${uri}`);
            });
          }}
        />
      </View>
    </View>
  );
}
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
    "rnoh-view-shot": "file:../../node_modules/@react-native-oh-tpl/react-native-view-shot/harmony/view_shot.har"
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
    "rnoh-view-shot": "file:../../node_modules/@react-native-oh-tpl/react-native-view-shot/harmony/view_shot"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 ViewShotPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-view-shot/src/main/cpp" ./view-shot)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_view_shot)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ViewShotPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ViewShotPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 ViewShotPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { ViewShotPackage } from 'rnoh-view-shot/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ViewShotPackage(ctx),
  ];
}
```

### 应用权限申请

> [!tip] "ohos.permission.WRITE_IMAGEVIDEO"权限等级为<B>system_basic</B>，授权方式为<B>user_grant</B>，[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.WRITE_IMAGEVIDEO" }
    ]
  }
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/view-shot Releases](https://github.com/react-native-oh-library/react-native-view-shot/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name   | Description  | Type  | Required | Platform | HarmonyOS Support |
| ------ | ------------ | ----- | -------- | -------- | ----------------- |
| `captureRef`  | 组件截图  | function | no | android, ios | yes           |
| `captureScreen`  | 屏幕截图  | function | no | android, ios | yes           |
| `releaseCapture`  | 资源释放  | function | no | android, ios | no           |

## 遗留问题

- [ ] harmonyOS 资源释放接口验证未通过 [issues#2](https://github.com/react-native-oh-library/react-native-view-shot/issues/2)。

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-view-shot/blob/harmony/LICENSE) ，请自由地享受和参与开源。