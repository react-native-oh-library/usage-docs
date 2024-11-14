> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-pdf</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonday/react-native-pdf">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wonday/react-native-pdf/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-pdf)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-pdf Releases](https://github.com/react-native-oh-library/react-native-pdf/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-pdf
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-pdf
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from "react";
import { View, Dimensions, StyleSheet } from "react-native";
import Pdf from "react-native-pdf";

export function PdfExample() {
  // const source = { uri: 'https://www-file.huawei.com/minisite/media/annual_report/annual_report_2022_cn.pdf', cache: true };
  const source = require("../assets/test.pdf");

  return (
    <View style={styles.sectionContainer}>
      <Pdf
        source={source}
        onLoadComplete={(numberOfPages, filePath) => {
          console.log(`Number of pages: ${numberOfPages}`);
        }}
        onPageChanged={(page, numberOfPages) => {
          console.log(`Current page: ${page}`);
        }}
        onError={(error) => {
          console.log(error);
        }}
        onPressLink={(uri) => {
          console.log(`Link pressed: ${uri}`);
        }}
        style={styles.pdf}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    flex: 1,
    justifyContent: "flex-start",
    alignItems: "center",
  },
  pdf: {
    flex: 1,
    width: Dimensions.get("window").width,
    height: Dimensions.get("window").height,
  },
});
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
    "@react-native-oh-tpl/react-native-pdf": "file:../../node_modules/@react-native-oh-tpl/react-native-pdf/harmony/pdfview.har"
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

### 3.配置 CMakeLists 和引入 PdfViewPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-pdf/src/main/cpp" ./pdfview)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_pdf_view)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "PdfViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<PdfViewPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RTNPdfView 组件

找到 **function buildCustomRNComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
  ...
+ import { RTNPdfView, PDF_VIEW_TYPE } from '@react-native-oh-tpl/react-native-pdf';

  @Builder
export function buildCustomRNComponent(ctx: ComponentBuilderContext) {
  ...
+  if (ctx.componentName === PDF_VIEW_TYPE) {
+     RTNPdfView({
+       ctx: ctx.rnComponentContext,
+       tag: ctx.tag,
+     })
+   }
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
+ PDF_VIEW_TYPE
  ];
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-pdf Releases](https://github.com/react-native-oh-library/react-native-pdf/releases)

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                           | Description                                                                                                                                                                                     | Type                                                          | Required | Platform      | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------- | -------- | ------------- |-------------------|
| source                         | PDF source like {uri:xxx, cache:false}. see the following for detail.                                                                                                                           | object                                                        | YES      | iOS / Android | yes               |
| page                           | initial page index                                                                                                                                                                              | number                                                        | NO       | iOS / Android | yes               |
| scale                          | should minScale<=scale<=maxScale                                                                                                                                                                | number                                                        | NO       | iOS / Android | yes               |
| minScale                       | min scale                                                                                                                                                                                       | number                                                        | NO       | iOS / Android | yes               |
| maxScale                       | max scale                                                                                                                                                                                       | number                                                        | NO       | iOS / Android | yes               |
| horizontal                     | draw page direction, if you want to listen the orientation change, you can use [[react-native-orientation-locker\]](https://github.com/react-native-oh-library/react-native-orientation-locker) | bool                                                          | NO       | iOS / Android | no                |
| showsHorizontalScrollIndicator | shows or hides the horizontal scroll bar indicator on iOS                                                                                                                                       | bool                                                          | NO       | iOS           | no                |
| showsVerticalScrollIndicator   | shows or hides the vertical scroll bar indicator on iOS                                                                                                                                         | bool                                                          | NO       | iOS           | no                |
| fitWidth                       | if true fit the width of view, can not use fitWidth=true together with scale                                                                                                                    | bool                                                          | NO       | iOS / Android | no                |
| fitPolicy                      | 0:fit width, 1:fit height, 2:fit both(default)                                                                                                                                                  | number                                                        | NO       | iOS / Android | yes               |
| spacing                        | the breaker size between pages                                                                                                                                                                  | number                                                        | NO       | iOS / Android | yes               |
| password                       | pdf password, if password error, will call OnError() with message "Password required or incorrect password."                                                                                    | string                                                        | NO       | iOS / Android | yes               |
| style                          | support normal view style, you can use this to set border/spacing color...                                                                                                                      | object                                                        | NO       | iOS / Android | yes               |
| renderActivityIndicator        | when loading show it as an indicator, you can use your component                                                                                                                                | (progress) => Component                                       | NO       | iOS / Android | no                |
| enableAntialiasing             | improve rendering a little bit on low-res screens, but maybe course some problem on Android 4.4, so add a switch                                                                                | bool                                                          | NO       | iOS / Android | no                |
| enablePaging                   | only show one page in screen                                                                                                                                                                    | bool                                                          | NO       | iOS / Android | no                |
| enableRTL                      | scroll page as "page3, page2, page1"                                                                                                                                                            | bool                                                          | NO       | iOS / Android | no                |
| enableAnnotationRendering      | enable rendering annotation, notice:iOS only support initial setting,not support realtime changing                                                                                              | bool                                                          | NO       | iOS           | no                |
| enableDoubleTapZoom            | Enable double tap to zoom gesture                                                                                                                                                               | bool                                                          | NO       | iOS / Android | no                |
| trustAllCerts                  | Allow connections to servers with self-signed certification                                                                                                                                     | bool                                                          | NO       | iOS / Android | no                |
| singlePage                     | Only show first page, useful for thumbnail views                                                                                                                                                | bool                                                          | NO       | iOS / Android | no                |
| onLoadProgress                 | callback when loading, return loading progress (0-1)                                                                                                                                            | function(percent)                                             | NO       | iOS / Android | yes               |
| onLoadComplete                 | callback when pdf load completed, return total page count, pdf local/cache path, {width,height} and table of contents                                                                           | function(numberOfPages, path, {width, height}, tableContents) | NO       | iOS / Android | partially         |
| onPageChanged                  | callback when page changed ,return current page and total page count                                                                                                                            | function(page,numberOfPages)                                  | NO       | iOS / Android | yes               |
| onError                        | callback when error happened                                                                                                                                                                    | function(error)                                               | NO       | iOS / Android | yes               |
| onPageSingleTap                | callback when page was single tapped                                                                                                                                                            | function(page)                                                | NO       | iOS / Android | no                |
| onScaleChanged                 | callback when scale page                                                                                                                                                                        | function(scale)                                               | NO       | iOS / Android | yes               |
| onPressLink                    | callback when link tapped                                                                                                                                                                       | function(uri)                                                 | NO       | iOS / Android | yes               |

#### Source

| Name          | Description                                   | Type   | Required | Platform      | HarmonyOS Support |
| ------------- | --------------------------------------------- | ------ | -------- | ------------- | ----------------- |
| uri           | see the following for detail.                 | object | YES      | iOS / Android | yes               |
| cache         | use cache or not                              | bool   | NO       | iOS / Android | no                |
| cacheFileName | specific file name for cached pdf file        | string | NO       | iOS / Android | no                |
| expiration    | cache file expired seconds (0 is not expired) | number | NO       | iOS / Android | no                |
| method        | request method when uri is a url              | string | NO       | iOS / Android | no                |
| headers       | request headers when uri is a url             | object | NO       | iOS / Android | no                |

#### Uri

| Name                                                               | Description                                                                             | Type          | Required | Platform      | HarmonyOS Support |
| ------------------------------------------------------------------ | --------------------------------------------------------------------------------------- | ------------- | -------- | ------------- | ----------------- |
| {uri:"http://xxx/xxx.pdf"}                                         | load pdf from a url                                                                     | object        | NO       | iOS / Android | yes               |
| {require("./test.pdf")}                                            | load pdf relate to js file (do not need add by xcode)                                   | require(path) | NO       | iOS           | yes               |
| {uri:"bundle-assets://path/to/xxx.pdf"}                            | load pdf from assets, the file should be at Android/app/src/main/assets/path/to/xxx.pdf | object        | NO       | iOS           | no                |
| {uri:"data:application/pdf;base64,JVBERi0xLjcKJc..."}              | load pdf from base64 string                                                             | object        | NO       | iOS / Android | no                |
| {uri:"file:///absolute/path/to/xxx.pdf"}                           | load pdf from local file system                                                         | object        | NO       | iOS / Android | no                |
| {uri:"ms-appx:///xxx.pdf"}                                         | load pdf bundled with UWP app                                                           | object        | NO       | Windows       | no                |
| {uri:"content://com.example.blobs/xxxxxxxx-...?offset=0&size=xxx"} | load pdf from content URI                                                               | object        | NO       | iOS           | no                |
| {uri:"blob:xxxxxxxx-...?offset=0&size=xxx"}                        | load pdf from blob URL                                                                  | object        | NO       | Android       | no                |

## 静态方法

| Name    | Description                                                                                                                              | Type                 | Required | Platform      | HarmonyOS Support |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | -------- | ------------- | ----------------- |
| setPage | Set the current page of the PDF component. pageNumber is a positive integer. If pageNumber > numberOfPages, current page is not changed. | function(pageNumber) | NO       | iOS / Android | no                |

## 遗留问题

- [ ] onLoadComplete 回调函数参数返回目前仅支持 numberOfPages, path参数：[issue#47](https://github.com/react-native-oh-library/react-native-pdf/issues/47)
- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑: [issue#48](https://github.com/react-native-oh-library/react-native-pdf/issues/48)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wonday/react-native-pdf/blob/master/LICENSE) ，请自由地享受和参与开源。


