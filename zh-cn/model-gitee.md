# 文档模板(删除)

> [!ATTENTION] 使用模板时请将后面带有 (删除) 的语句删除。(删除)

> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>原库 npm 包名</code> </h1>
</p>

本项目基于 [原库 npm 名称@x.x.x](原库仓库连接) 开发。

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
npm install @react-native-ohos/库名
```

#### **yarn**

```bash
yarn add @react-native-ohos/库名
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
// react-native-safe-area-context 为例
import React from "react";
import { Text, View } from "react-native";
import {
  SafeAreaProvider,
  SafeAreaView,
  initialWindowMetrics,
} from "react-native-safe-area-context";

const App = () => {
  return (
    <SafeAreaProvider initialMetrics={initialWindowMetrics}>
      <SafeAreaView style={{ flex: 1, backgroundColor: "red" }}>
        <View style={{ flex: 1 }}>
          <Text>hello</Text>
        </View>
      </SafeAreaView>
    </SafeAreaProvider>
  );
};

export default App;
```

## 2. Manual Link

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1. Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

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

### 2.2. 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/Package_Name": "file:../../node_modules/@react-native-ohos/Package_Name/harmony/xxx.har"
    // 提示: "@react-native-ohos/react-native-safe-area-context": "file:../../node_modules/@react-native-ohos/react-native-safe-area-context/harmony/safe_area.har"（删除）
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3. 配置 CMakeLists 和引入 xxxPackge

**若涉及接入 codegen-lib 导致的配置项新增，需要在配置项前明确声明：> [!TIP] 版本 vx.x.x 及以上需要**（删除）

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-safe-area-context/src/main/cpp" ./safe-area)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_safe_area)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "SafeAreaViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<SafeAreaViewPackage>(ctx),
    };
}
```

**提示：ArkTs 侧引入 Fabric 组件**（删除）

### 2.4. 在 ArkTs 侧引入 xxx 组件（若本库已 CAPI 化则需要删除本段）

找到 `function buildCustomRNComponent()`，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { SAFE_AREA_VIEW_TYPE, SafeAreaView, SAFE_AREA_PROVIDER_TYPE, SafeAreaProvider } from "@react-native-ohos/react-native-safe-area-context"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+ if (ctx.componentName === SAFE_AREA_VIEW_TYPE) {
+   SafeAreaView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
+ RNC_VIDEO_TYPE
  ];
```

**提示：TurboModule**（删除）

### 2.5. 在 ArkTs 侧引入 xxx Package

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {SafeAreaViewPackage} from '@react-native-ohos/react-native-safe-area-context/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new SafeAreaViewPackage(ctx)
  ];
}
```

### 2.6. 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1. 兼容性

**修改了原库代码的库使用下述描述**（删除）

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<HarmonyOS npm 包名> Releases](https://gitee.com/openharmony-sig/仓库名/releases)

提示：[@react-native-ohos/react-native-linear-gradient Releases](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/releases)（删除）

**未修改原库代码的库使用下述描述**（删除）

本文档内容基于以下版本验证通过：

(示例)

1. RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); IDE: DevEco Studio 5.0.3.906; ROM: NEXT.0.0.71;

### 3.2. 权限要求（如有）

（填入相关权限配置）

**以下属性、静态方法、API 需要检查说明中手机平台描述，例如已支持 HarmonyOS 的接口并且说明中提到 iOS 和 Android，那么需要检查是否补充 HarmonyOS 进到描述中。示例如下（删除）**

```
// 原描述
Needed for Android to work properly with assets, iOS will ignore it.
// 修改后
Needed for Android and HarmonyOS to work properly with assets, iOS will ignore it.
```

（删除）

## 4. 属性（如有）

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 5. 静态方法（如有）

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 6. API（如有，一般是 TurboModules）

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| XXX  | XXX         | XXX  | (yes/no) | xxx      | (yes/no/partially) |

## 7. 遗留问题

- [ ] xxx 问题: [issue#\*\*\*](issue地址1)
- [ ] yyy 问题: [issue#\*\*\*](issue地址2)

## 8. 其他

**其他补充说明（删除）**

## 9. 开源协议

本项目基于 [XXX License (XXX)](gitee仓库的LICENSE链接) ，请自由地享受和参与开源。

例子：本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-linear-gradient/blob/master/LICENSE) ，请自由地享受和参与开源。(删除)
