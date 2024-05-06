> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-worklets-core</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-worklets-core/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-worklets-core)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-worklets-core Releases](https://github.com/react-native-oh-library/react-native-worklets-core/releases)，并下载适用版本的 tgz 包

进入到工程目录并输入以下命令：

<!-- tabs:start -->

> [!TIP] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm i @react-native-oh-tpl/react-native-worklets-core@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-worklets-core@file:#
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

```diff
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
+   "@react-native-oh-tpl/react-native-worklets-core": "file:../../node_modules/@react-native-oh-tpl/react-native-worklets-core/harmony/rn_worklets.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```shell
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```diff
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
+   "@react-native-oh-tpl/react-native-worklets-core": "file:../../node_modules/@react-native-oh-tpl/react-native-worklets-core/harmony/rn_worklets"
  }
```

打开终端，执行：

```shell
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入Worklets

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/@react-native-oh-tpl/react-native-worklets-core/src/main/cpp" ./worklets)
# RNOH_END: add_package_subdirectories

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_worklets)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "WorkletsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<WorkletsPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 ImageEditorPackage

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

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```shell
cd entry
ohpm install
```

然后编译、运行即可。

快速使用：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import { useState } from "react";
import { Button, Text, View } from "react-native"
import { useRunOnJS, useWorklet } from "react-native-worklets-core";

const App = () => {
    // 计数器
    const [count, setCount] = useState(0);
    // 定义一个useRunJS方法
    const setCountRunInJS = useRunOnJS(() => {
        setCount(Math.random());
    }, [count])
    // 在worklets线程使用RunInJS方法
    const countInWorkLet = useWorklet('default', () => {
        'worklet'
        setCountRunInJS();
    }, [setCountRunInJS])

    return (
        <View>
            <View style={{ flexDirection: 'row', gap: 10 }}>
                <Button title="SetCount" onPress={() => countInWorkLet()} />
            </View>
            <Text>count:{count}</Text>
        </View>
    )
}

export default App;
```

## 约束与限制

### 兼容性
本文档内容基于以下版本验证通过：

1. RNOH：0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：205.0.0.18;

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-worklets-core Releases](https://github.com/react-native-oh-library/react-native-worklets-core/releases)

### API

| NAME                   | Description                                                  | Required | Platform | HarmonyOS Support |
| ---------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| createContext          | Create a worker thread context object                        | YES      | All      | YES               |
| createSharedValue      | Creates a new worklet context with the given name            | YES      | All      | YES               |
| createRunOnJS          | Creates a function that can be executed asynchronously on the default React-JS context | YES      | All      | YES               |
| runOnJS                | Runs the given Function asynchronously on the default React-JS context | YES      | All      | YES               |
| getCurrentThreadId     | Returns a unique identifier for the Thread this method is called on | YES      | All      | YES               |
| defaultContext         | Get the default Worklet context                              | YES      | All      | YES               |
| context.createRunAsync | Creates a function that can be executed asynchronously on the Worklet context. | YES      | All      | YES               |
| context.runAsync       | Runs the given Function asynchronously on this Worklet context. | YES      | All      | YES               |
| useWorklet             | Same as `context.createRunAsync`                             | YES      | All      | YES               |
| useRunOnJS             | Same as `createRunOnJS`                                      | YES      | All      | YES               |
| useSharedValue         | Same as `createSharedValue`                                  | YES      | All      | YES               |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-worklets-core/blob/sig/LICENSE) ，请自由地享受和参与开源。
