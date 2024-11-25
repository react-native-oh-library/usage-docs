> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-view-shot)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-view-shot Releases](https://github.com/react-native-oh-library/react-native-view-shot/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-view-shot
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-view-shot
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Text, Button } from "react-native";
import ViewShot, { captureRef, captureScreen } from "react-native-view-shot";

export function ViewShotDemo() {
  const view = React.useRef < View > (null);
  const ref = React.useRef(null);
  const onCapture = (res) => {
    console.info("onCapture callback");
  };
  const onCaptureFailure = (err) => {
    console.info("onCaptureFailure " + JSON.stringify(err));
  };

  return (
    <View>
      <View
        ref={view}
        collapsable={false}
        style={{ backgroundColor: "#ffffff" }}
      >
        <Text style={{ color: "#000", marginBottom: 30 }}>
          Hello OpenHarmony
        </Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>Hello HarmonyOS</Text>
        <Text style={{ color: "#000", marginBottom: 30 }}>
          Hello HarmonyOS Next.
        </Text>

        <ViewShot
          ref={ref}
          style={{ backgroundColor: "#ffffff" }}
          onCapture={onCapture}
          onCaptureFailure={onCaptureFailure}
          captureMode="mount"
        >
          <Text style={{ color: "#000", marginBottom: 30 }}>Hello World</Text>
        </ViewShot>

      </View>
      <Button
        title="captureRef"
        onPress={() => {
          captureRef(view).then((res) => {
            console.info(`captureRef: ${JSON.stringify(res)}`);
          });
        }}
      />
      <Button
        title="ViewShot capture"
        onPress={() => {
          captureRef(ref).then((res) => {
            console.info(`captureRef: ${res}`);
          });
        }}
      />
      <Button
        title="captureScreen"
        onPress={() => {
          captureScreen().then((res) => {
            console.info(`captureScreen success: ${res}`);
          });
        }}
      />
    </View>
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

    "@react-native-oh-tpl/react-native-view-shot": "file:../../node_modules/@react-native-oh-tpl/react-native-view-shot/harmony/view_shot.har"
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

### 3.配置 CMakeLists 和引入 ViewShotPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-view-shot/src/main/cpp" ./view-shot)
# RNOH_BEGIN: manual_package_linking_1

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_view_shot)
# RNOH_BEGIN: manual_package_linking_2
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

### 4.在 ArkTs 侧引入 ViewShotPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { ViewShotPackage } from '@react-native-oh-tpl/react-native-view-shot/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ViewShotPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/view-shot Releases](https://github.com/react-native-oh-library/react-native-view-shot/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                     | Type                                   | Required | Platform     | HarmonyOS Support |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------- | -------- | ------------ | ----------------- |
| captureMode      | if not defined (default). the capture is not automatic and you need to use the ref and call `capture()` yourself<br>`"mount"`. Capture the view once at mount. (It is important to understand image loading won't be waited, in such case you want to use "none" with viewShotRef.capture() after Image#onLoad.) <br>`"continuous"` EXPERIMENTAL, this will capture A LOT of images continuously. For very specific use-cases.<br> `"update"` EXPERIMENTAL, this will capture images each time React redraw (on did update). For very specific use-cases. | ( 'mount' \| 'continuous' \| 'update') | no       | Android, iOS | yes               |
| onCapture        | when a `captureMode` is defined, this callback will be called with the capture result.                                                                                                                                                                                                                                                                                                                                                                                                                                                                          | function                               | no       | Android, iOS | yes               |
| onCaptureFailure | when a `captureMode` is defined, this callback will be called when a capture fails.                                                                                                                                                                                                                                                                                                                                                                                                                                                                             | function                               | no       | Android, iOS | yes               |
| options | view shot configuration. | object                         | no       | Android, iOS | partially     |
| children | the actual content to rasterize. | ReactNode | no | Android, iOS | yes |

#### options属性详情

| Name                     | Description                                                  | Type                                 | Required | Platform     | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------ | ------------------------------------ | -------- | ------------ | ----------------- |
| fileName                 | the file name of the file. Must be at least 3 characters long. | string                               | no       | Android, iOS | yes               |
| width / height           | the width and height of the final image (resized from the View bound. don't provide it if you want the original pixel size). | number                               | no       | Android, iOS | yes               |
| quality                  | the quality. 0.0 - 1.0 (default). (only available on lossy formats like jpg) | number                               | no       | Android, iOS | yes               |
| format                   | either png or jpg. Defaults to png.                          | string                               | no       | Android, iOS | yes               |
| result                   | the method you want to use to save the snapshot, one of:<br/>"tmpfile" (default): save to a temporary file (that will only exist for as long as the app is running).<br/>"base64": encode as base64 and returns the raw string. Use only with small images as this may result of lags (the string is sent over the bridge). N.B. This is not a data uri, use data-uri instead.<br/>"data-uri": same as base64 but also includes the Data URI scheme header. | ( 'tmpfile' \|'base64' \|'data-uri') | no       | Android, iOS | yes               |
| snapshotContentContainer | if true and when view is a ScrollView, the "content container" height will be evaluated instead of the container height. | boolean                              | no       | Android, iOS | no                |
| useRenderInContext       | change the iOS snapshot strategy to use method renderInContext instead of drawViewHierarchyInRect which may help for some use cases. | boolean                              | no       | Android, iOS | no                |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name             | Description | Type     | Required | Platform     | HarmonyOS Support |
| ---------------- | ----------- | -------- | -------- | ------------ | ----------------- |
| `captureRef`     | 组件截图    | function | no       | Android, iOS | yes               |
| `captureScreen`  | 屏幕截图    | function | no       | Android, iOS | yes               |
| `releaseCapture` | 资源释放    | function | no       | Android, iOS | yes               |

## 遗留问题

- [x] HarmonyOS 资源释放接口验证未通过 [issues#2](https://github.com/react-native-oh-library/react-native-view-shot/issues/2)。
- [ ] 被截图组件需要设置背景色，否则截图效果全黑 [issues#3](https://github.com/react-native-oh-library/react-native-view-shot/issues/3)。
- [ ] 截图配置项 snapshotContentContainer 与 useRenderInContext 暂未实现 [issues#34](https://github.com/react-native-oh-library/react-native-view-shot/issues/34)。

## 其他
## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/gre/react-native-view-shot/blob/master/LICENSE) ，请自由地享受和参与开源。