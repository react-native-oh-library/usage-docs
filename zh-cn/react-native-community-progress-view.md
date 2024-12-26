> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>@react-native-community/progress-view</code> </h1>
</p>


本项目基于 [react-native-community/progress-view@1.4.2](https://github.com/react-native-progress-view/progress-view) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-progress-view`，具体版本所属关系如下：

| Version                        | Package Name                             | Repository                                                   | Release                                                      |
| ------------------------------ | ---------------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| <= 1.4.2@deprecated | @react-native-oh-tpl/progress-view  | [Github(deprecated)](https://github.com/react-native-oh-library/progress-view) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/progress-view/releases) |
| > 1.4.2                        | @react-native-ohos/progress-view | [Gitee](https://gitee.com/openharmony-sig/rntpc_progress-view) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_progress-view/releases) |

## 安装与使用

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/progress-view
```

#### **yarn**

```bash
yarn add @react-native-ohos/progress-view
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { ProgressView } from "@react-native-community/progress-view";

export default function ProgressViewExample() {
  return (
    <ProgressView
      progressTintColor="orange"
      trackTintColor="blue"
      progress={0.7}
    />
  )
}
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

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-ohos/progress-view": "file:../../node_modules/@react-native-ohos/progress-view/harmony/progress_view.har"
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

### 2.3 配置 CMakeLists 和引入 ProgressViewPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/progress-view/src/main/cpp" ./progress-view)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_progress_view)
# RNOH_BEGIN: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "ProgressViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ProgressViewPackage>(ctx)
    };
}
```

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
+ import { RNCProgressView, PROGRESS_VIEW_TYPE } from "@react-native-ohos/progress-view"

@Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...  
+ if (ctx.componentName === PROGRESS_VIEW_TYPE) {
+   RNCProgressView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
+   })
+ }
...
}
...
```

> [!TIP] 本库使用了混合方案，需要添加组件名。

在`entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets` 找到常量 `arkTsComponentNames` 在其数组里添加组件名

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ PROGRESS_VIEW_TYPE
  ];
```

 > **[!TIP] 版本 1.4.3 及以上需要.**

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ProgressViewPackage } from "@react-native-ohos/progress-view/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ProgressViewPackage(ctx), 
  ];
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

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-progress-view Releases](https://gitee.com/openharmony-sig/rntpc_progress-view/releases)

## 4. 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                | Description                                | Type   | Required | Platform | HarmonyOS Support |
| ------------------- | ------------------------------------------ | ------ | -------- | -------- | ----------------- |
| `progress`          | The progress value (between 0 and 1).      | number | No       | All      | Yes               |
| `progressTintColor` | The tint color of the progress bar itself. | string | No       | All      | Yes               |
| `trackTintColor`    | The tint color of the progress bar track.  | string | No       | All      | Yes               |
| `progressImage`     | A stretchable image to display as the progress bar.      | Image.propTypes.source | No       | All      | No               |
| `trackImage` | A stretchable image to display behind the progress bar. Network images only work on Windows.| Image.propTypes.source | No       | All      | No               |
| `progressViewStyle`    | The progress bar style. Network images only work on Windows.  | enum('default', 'bar') | No       | All      | No               |
| `isIndeterminate`    | Turns progress bar into an indeterminate progress bar.  | bool | No       | Windows      | Partially               |

## 5. 遗留问题

- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑，问题: [issue#1](https://github.com/react-native-oh-library/progress-view/issues/5)

## 6. 其他

## 7. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_progress-view/blob/master/LICENSE) ，请自由地享受和参与开源。

