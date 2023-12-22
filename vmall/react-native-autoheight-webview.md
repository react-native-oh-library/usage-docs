> 模板版本：v0.1.1
<p align="center">
  <h1 align="center"> <code>react-native-autoheight-webview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-oh-library/react-native-autoheight-webview">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-autoheight-webview)

## 安装与使用

进入到工程目录并输入以下命令：

```bash
yarn add @react-native-oh-tpl/react-native-autoheight-webview
```

或者

```bash
npm install @react-native-oh-tpl/react-native-autoheight-webview
```

下面的代码展示了这个库的基本使用场景：

```js
import AutoHeightWebView from "react-native-autoheight-webview";

<AutoHeightWebView source={{ uri: "https://reactnative.dev/" }} />;
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
    "rnoh-webview": "file:../../node_modules/@react-native-oh-tpl/react-native-webview/harmony/rn_webview.har"
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
    "rnoh-webview": "file:../../node_modules/@react-native-oh-tpl/react-native-webview/harmony/rn_webview"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 WebViewPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-webview/src/main/cpp" ./webview)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_webview)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "WebViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<WebViewPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 webview 组件

打开 `entry/src/main/ets/pages/index.ets`，添加：

```diff
+ import { WebView, WEB_VIEW } from "rnoh-webview"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.componentName === WEB_VIEW) {
+   WebView({
+     ctx: ctx.rnohContext,
+     tag: ctx.tag,
+     buildCustomComponent: CustomComponentBuilder
+   })
+ }
 ...
}
...
```

### 在 ArkTs 侧引入 WebViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import { WebViewPackage } from 'rnoh-webview/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new WebViewPackage(ctx)
  ];
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

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-autoheight-webview Releases](https://github.com/react-native-oh-library/react-native-autoheight-webview/releases)

## 属性

| 名称                              | 说明                                                                                                                                                                             | 类型                                                                                                          | 是否必填 | 原库平台 | 鸿蒙支持 |
| --------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- |
| `source`                          | Loads static HTML or a URI (with optional headers) in the WebView                                                                                                                | One of: <br />**Load uri :**<br />uri <br />headers <br />**Static HTML :**<br />html <br />baseUrl           | yes      | All      | yes      |
| `originWhitelist?`                | List of origin strings to allow being navigated to.                                                                                                                              | string[]                                                                                                      | No       | All      | yes      |
| `scalesPageToFit?`                | Boolean that controls whether the web content is scaled to fit the view and enables the user to change the scale.                                                                | boolean                                                                                                       | No       | android  | yes      |
| `customScript?`                   | -                                                                                                                                                                                | string                                                                                                        | No       | All      | yes      |
| `style?`                          | A style object that allow you to customize the WebView style.                                                                                                                    | Style                                                                                                         | No       | All      | yes      |
| `customStyle?`                    | The custom css content will be added to the page's <head>.                                                                                                                       | string                                                                                                        | No       | All      | yes      |
| `onSizeUpdated?`                  | Either updated height or width will trigger onSizeUpdated.                                                                                                                       | function                                                                                                      | No       | All      | yes      |
| `showsHorizontalScrollIndicator?` | Boolean value that determines whether a horizontal scroll indicator is shown in the WebView.                                                                                     | boolean                                                                                                       | No       | All      | yes      |
| `showsVerticalScrollIndicator`    | Boolean value that determines whether a vertical scroll indicator is shown in the WebView.                                                                                       | boolean                                                                                                       | No       | All      | yes      |
| `files?`                          | Using local or remote files. To add local files: Add files to android/app/src/main/assets/ (depends on baseUrl) on android; add files to web/ (depends on baseUrl) on iOS.       | PropTypes.arrayOf(PropTypes.shape({ href: PropTypes.string, type: PropTypes.string, rel: PropTypes.string })) | No       | All      | yes      |
| `scrollEnabledWithZoomedin?`      | Making the webview scrollable on iOS when zoomed in even if scrollEnabled is false.                                                                                              | boolean                                                                                                       | No       | ios      | no       |
| `viewportContent?`                | Please note that 'width=device-width' with scalesPageToFit may cause some layout issues on Android, for these conditions, using customScript prop to apply custom viewport meta. | string                                                                                                        | No       | All      | yes      |

## 遗留问题

- [ ] autoheight-webview 部分属性未实现鸿蒙化[issue#1](https://github.com/react-native-oh-library/react-native-autoheight-webview/issues/1)

## 其他

## 开源协议

本项目基于 [The ISC License (ISC)](https://github.com/iou90/react-native-autoheight-webview/blob/master/LICENSE) ，请自由地享受和参与开源。
