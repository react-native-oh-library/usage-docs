> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-MJRefresh</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-studio/react-native-MJRefresh">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-MJRefresh/blob/sig/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-MJRefresh)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-library/react-native-MJRefresh> Releases](https://github.com/react-native-oh-library/react-native-MJRefresh/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-mjrefresh@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-mjrefresh@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState } from "react";
import { ScrollView, Text, View } from "react-native";
import { MJRefreshControl } from "react-native-mjrefresh";

export const MjRefreshDemo = () => {
  const [state, setState] = useState<{
    message?: string;
  }>({
    message: "",
  });
  const { message } = state;
  let mjRefreshRef: React.RefObject<MJRefreshControl>;
  return (
    <View>
      <ScrollView
        style={{ width: "100%", height: "80%" }}
        refreshControl={
          <MJRefreshControl
            ref={(ref) => (this.mjRefreshRef = ref)}
            onRefresh={() => {
              setState({ message: "正在刷新" });
              console.log("------------onRefresh");
              // 开始刷新
              this.mjRefreshRef.beginRefresh();
              // 自定义刷新结束事件
              setTimeout(() => {
                console.log("------------ Finish Refresh");
                // 结束刷新
                this.mjRefreshRef.finishRefresh();
              }, 2000);
            }}
            onRefreshIdle={() => {
              setState({ message: "下拉刷新" });
              console.log("------------onRefreshIdle");
            }}
            onReleaseToRefresh={() => {
              setState({ message: "释放刷新" });
              console.log("------------onReleaseToRefresh");
            }}
            onPulling={() => {
              setState({ message: "下拉刷新" });
              console.log("------------onPulling");
            }}
          ></MJRefreshControl>
        }
      ></ScrollView>
      <Text>Refresh State:{message}</Text>
    </View>
  );
};
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
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "rnoh-mjrefresh": "file:../../node_modules/@react-native-oh-tpl/react-native-mjrefresh/harmony/mjrefresh.har"
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

### 配置 CMakeLists 和引入 MJRefreshPackge

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-mjrefresh/src/main/cpp" ./mjrefresh)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_mjrefresh)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "MJRefreshPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<MJRefreshPackage>(ctx),
    };
}
```

### 在 ArkTs 侧引入 MJRefresh 组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
+  import { MJRefresh, MJREFRESH_TYPE} from "rnoh-mjrefresh"

  @Builder
  function buildCustomComponent(ctx: ComponentBuilderContext) {
    if (ctx.componentName === SAMPLE_VIEW_TYPE) {
      SampleView({
        ctx: ctx.rnComponentContext,
        tag: ctx.tag,
        buildCustomComponent: buildCustomComponent
      })
    }
+   else if (ctx.componentName === MJREFRESH_TYPE) {
+     MJRefresh({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomComponent
+     })
+   }
    ...
  }
  ...
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<@react-native-oh-library/react-native-MJRefresh> Releases](https://github.com/react-native-oh-library/react-native-MJRefresh/releases)

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-MJRefresh](https://github.com/react-native-studio/react-native-MJRefresh)

| Name               | Description | Type     | Required | Platform | HarmonyOS Support |
| :----------------- | ----------- | -------- | -------- | -------- | ----------------- |
| onRefresh          | System Path | function | No       | IOS      | yes               |
| onRefreshIdle      | System Path | function | No       | IOS      | yes               |
| onReleaseToRefresh | System Path | function | No       | IOS      | yes               |
| onPulling          | System Path | function | No       | IOS      | yes               |

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-MJRefresh](https://github.com/react-native-studio/react-native-MJRefresh)

| Name          | Description | Type     | Required | Platform | HarmonyOS Support |
| :------------ | ----------- | -------- | -------- | -------- | ----------------- |
| beginRefresh  | System Path | function | No       | IOS      | yes               |
| finishRefresh | System Path | function | No       | IOS      | yes               |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-studio/react-native-MJRefresh/blob/master/LICENSE) ，请自由地享受和参与开源。
