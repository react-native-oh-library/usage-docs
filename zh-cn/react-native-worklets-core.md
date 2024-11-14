> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-worklets-core</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/margelo/react-native-worklets-core">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/margelo/react-native-worklets-core/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-worklets-core)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-worklets-core Releases](https://github.com/react-native-oh-library/react-native-worklets-core/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm i @react-native-oh-tpl/react-native-worklets-core
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-worklets-core
```

在项目根目录下的 `babel.config.js` 中添加 `babel` 插件

```js
module.exports = {
  plugins: [
    ["@react-native-oh-tpl/react-native-worklets-core/plugin"],
    // ...
  ],
  // ...
};
```

重置缓存重启项目

```bash
yarn start --reset-cache
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```jsx
import { useState } from "react";
import { Button, Text, View } from "react-native";
import { useRunOnJS, useWorklet } from "react-native-worklets-core";

const App = () => {
  // 计数器
  const [count, setCount] = useState(0);
  // 定义一个useRunJS方法
  const setCountRunInJS = useRunOnJS(() => {
    setCount(Math.random());
  }, [count]);
  // 在worklets线程使用RunInJS方法
  const countInWorkLet = useWorklet(
    "default",
    () => {
      "worklet";
      setCountRunInJS();
    },
    [setCountRunInJS]
  );

  return (
    <View>
      <View style={{ flexDirection: "row", gap: 10 }}>
        <Button title="SetCount" onPress={() => countInWorkLet()} />
      </View>
      <Text>count:{count}</Text>
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-worklets-core": "file:../../node_modules/@react-native-oh-tpl/react-native-worklets-core/harmony/rn_worklets.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```shell
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 3.配置 CMakeLists 和引入 Worklets

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

add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-oh-tpl/react-native-worklets-core/src/main/cpp" ./worklets)

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_worklets)
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "WorkletsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<WorkletsPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 WorkletsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { WorkletsPackage } from "@react-native-oh-tpl/react-native-worklets-core/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new WorkletsPackage(ctx)
  ];
}
```

### 5.运行

点击右上角的 `sync` 按钮

或者在终端执行：

```shell
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-worklets-core Releases](https://github.com/react-native-oh-library/react-native-worklets-core/releases)

### API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| NAME                   | Description                                                  | Type      | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | --------- | -------- | -------- | ----------------- |
| createContext          | Creates a new worklet context with the given name.           | function  | no       | All      | yes               |
| createSharedValue      | Creates a value that can be shared between runtimes.         | function  | no       | All      | yes               |
| createRunOnJS          | Creates a function that can be executed asynchronously on the default React-JS context. | function  | no       | All      | yes               |
| runOnJS                | Runs the given Function asynchronously on the default React-JS context. | function  | no       | All      | yes               |
| getCurrentThreadId     | Returns a unique identifier for the Thread this method is called on. | function  | no       | All      | yes               |
| defaultContext         | Get the default Worklet context.                             | interface | no       | All      | yes               |
| currentContext         | Get the current Worklet context, or `undefined` if called in main React JS context. | interface | no       | All      | yes               |
| __jsi_is_array         | Returns true if jsi/cpp believes that the passed value is an array. | function  | no       | All      | yes               |
| __jsi_is_object        | Returns true if jsi/cpp believes that the passed value is an object. | function  | no       | All      | yes               |
| context.addDecorator   | Adds an object to the worklet context. The object will be available in all worklets. | function  | no       | All      | yes               |
| context.createRunAsync | Creates a function that can be executed asynchronously on the Worklet context. | function  | no       | All      | yes               |
| context.runAsync       | Runs the given Function asynchronously on this Worklet context. | function  | no       | All      | yes               |
| useWorklet             | Create a Worklet function that automatically memoizes itself using it's auto-captured closure. | function  | no       | All      | yes               |
| useRunOnJS             | Create a Worklet function that runs the given function on the JS context. | function  | no       | All      | yes               |
| useSharedValue         | Create a Shared Value that persists between re-renders.      | function  | no       | All      | yes               |
| isWorklet              | Checks whether the given function is a Worklet or not.       | function  | no       | All      | yes               |
| worklet                | Ensures the given function is a Worklet, and throws an error if not. | function  | no       | All      | yes               |
| getWorkletDependencies | Get the dependencies of the given worklet.                   | function  | no       | All      | yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/margelo/react-native-worklets-core/blob/main/LICENSE) ，请自由地享受和参与开源。
