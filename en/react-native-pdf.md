> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-pdf)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-pdf Releases](https://github.com/react-native-oh-library/react-native-pdf/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
   ...
   "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-pdf": "file:../../node_modules/@react-native-oh-tpl/react-native-pdf/harmony/pdfview.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing PdfViewPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4. Introducing RTNPdfView Component to ArkTS

Find `function buildCustomRNComponent()`, which is usually located in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets`, and add the following code:

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

> [!TIP] If the repository uses a mixed solution, the component name needs to be added.

Find the constant `arkTsComponentNames` in `entry/src/main/ets/pages/index.ets` or `entry/src/main/ets/rn/LoadBundle.ets` and add the component name to the array.

```diff
const arkTsComponentNames: Array<string> = [
  SampleView.NAME,
  GeneratedSampleView.NAME,
  PropsDisplayer.NAME,
+ PDF_VIEW_TYPE
  ];
```

### 5. Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-pdf Releases](https://github.com/react-native-oh-library/react-native-pdf/releases)

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name    | Description                                                                                                                              | Type                 | Required | Platform      | HarmonyOS Support |
| ------- | ---------------------------------------------------------------------------------------------------------------------------------------- | -------------------- | -------- | ------------- | ----------------- |
| setPage | Set the current page of the PDF component. pageNumber is a positive integer. If pageNumber > numberOfPages, current page is not changed. | function(pageNumber) | NO       | iOS / Android | no                |

## Known Issues

- [ ] onLoadComplete 回调函数参数返回目前仅支持 numberOfPages, path参数：[issue#47](https://github.com/react-native-oh-library/react-native-pdf/issues/47)
- [ ] 原库部分接口在 HarmonyOS 中没有对应属性及接口处理相关逻辑: [issue#48](https://github.com/react-native-oh-library/react-native-pdf/issues/48)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/wonday/react-native-pdf/blob/master/LICENSE).
