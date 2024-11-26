> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-linear-gradient</code> </h1>
</p>

本项目基于 [react-native-linear-gradient@3.0.0-alpha.1](https://github.com/react-native-linear-gradient/react-native-linear-gradient) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-linear-gradient`，具体版本所属关系如下：

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 3.0.0-0.5.0@deprecated | @react-native-oh-tpl/react-native-linear-gradient | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-linear-gradient/releases) |
| > 3.0.0                   | @react-native-ohos/react-native-linear-gradient   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/releases) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-linear-gradient
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-linear-gradient
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { ReactNode } from "react";
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  View,
} from "react-native";
import LinearGradient from "react-native-linear-gradient";

// Within your render function
function LinearGradientDemo() {
  return (
    <View style={styles.container}>
      <LinearGradient
        colors={["#4c669f", "#3b5998", "#192f6a"]}
        style={styles.linearGradient}
      >
        <Text style={styles.buttonText}>Sign in with Facebook</Text>
      </LinearGradient>
      ;
    </View>
  );
}
export default LinearGradientDemo;
// Later on in your styles..
var styles = StyleSheet.create({
  container: {
    backgroundColor: "#fff",
    flex: 1,
    paddingTop: 24,
  },
  linearGradient: {
    flex: 1,
    paddingLeft: 15,
    paddingRight: 15,
    borderRadius: 5,
  },
  buttonText: {
    fontSize: 18,
    fontFamily: "Gill Sans",
    textAlign: "center",
    margin: 10,
    color: "#ffffff",
    backgroundColor: "transparent",
  },
});
```

## 2. Manual Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1 Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `harmony/oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

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

### 2.2 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/react-native-linear-gradient": "file:../../node_modules/@react-native-ohos/react-native-linear-gradient/harmony/linear_gradient.har"
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

### 2.3 配置 CMakeLists 和引入 LinearGradientPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-linear-gradient/src/main/cpp" ./linear-gradient)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_linear_gradient)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "LinearGradientPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx),
+     std::make_shared<LinearGradientPackage>(ctx)
    };
}
```

### 2.4 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1 兼容性

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-linear-gradient Releases](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/releases)

## 4. 属性

> [!TIP] "Platform" 列表示这些属性在原始第三方库中支持的平台。

> [!TIP] "如果“HarmonyOS 支持”列的值为“yes”，则表示 HarmonyOS 平台支持该属性；“no”则表示不支持；“partially”表示部分支持该属性的功能。该属性在不同平台上的使用方法相同，效果与 iOS 或 Android 平台一致。

| Name        | Description                                              | Type                   | Required | Platform | HarmonyOS Support |
| ----------- | -------------------------------------------------------- | ---------------------- | -------- | -------- | ----------------- |
| colors      | Color Array                                              | (string\|number)[]     | NO       | All      | yes               |
| locations   | Color for unknown array (length 0 or the same as colors) | number[]               | NO       | All      | yes               |
| useAngle    | Use angle (default false)                                | boolean                | NO       | All      | yes               |
| angle       | Angle (useAngle=true valid)                              | number                 | NO       | All      | yes               |
| angleCenter | Middle angle coordinate                                  | { x: number,y: number} | NO       | All      | no                |
| start       | Starting point coordinates (default value: {x: 0.5,1})   | { x: number,y: number} | NO       | All      | yes               |
| end         | End point coordinates (default value: {x: 0.5,1})        | { x: number,y: number} | NO       | All      | yes               |

## 5. 遗留问题

- HarmonyOS 当前版本暂时无法实现 angleCenter

## 6. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/blob/master/LICENSE)，请自由地享受和参与开源。
