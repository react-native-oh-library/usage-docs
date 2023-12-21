<p align="center">
  <h1 align="center"> <code>react-native-webview</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-webview/react-native-webview">
        <img src="https://img.shields.io/badge/platforms-android%20%7C%20ios%20%7C%20windows%20%7C%20macos%20%7C%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-webview/react-native-webview/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

## 安装与使用

进入到工程目录并输入以下命令：

**正在 npm 发布中，当前请先从仓库[Release](https://github.com/react-native-oh-library/react-native-webview/releases)中获取库 tgz，通过使用本地依赖来安装本库。**

```bash
yarn add xxx
```

或者

```bash
npm install xxx
```

下面的代码展示了这个库的基本使用场景：

```js
import { WebView } from "react-native-webview";

<WebView source={{ uri: "https://reactnative.dev/" }} />;
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
    "rnoh-webview": "file:../../node_modules/react-native-webview/harmony/rn_webview.har"
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
    "rnoh-webview": "file:../../node_modules/react-native-webview/harmony/rn_webview"
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
import {
  RNApp,
  ComponentBuilderContext,
  RNAbility,
  AnyJSBundleProvider,
  MetroJSBundleProvider,
  ResourceJSBundleProvider,
} from 'rnoh'
import { SampleView, SAMPLE_VIEW_TYPE, PropsDisplayer } from "rnoh-sample-package"
import { createRNPackages } from '../RNPackagesFactory'
+ import { WebView, WEB_VIEW } from "rnoh-webview"

@Builder
function CustomComponentBuilder(ctx: ComponentBuilderContext) {
  if (ctx.descriptor.type === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnohContext,
      tag: ctx.descriptor.tag,
      buildCustomComponent: CustomComponentBuilder
    })
  }
+ else if (ctx.descriptor.type === WEB_VIEW) {
+   WebView({
+     ctx: ctx.rnohContext,
+     tag: ctx.descriptor.tag,
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-webview Releases](https://github.com/react-native-oh-library/react-native-webview/releases)

## 属性

详情请查看[webview 官方文档](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Reference.md)

如下是 webview 已经鸿蒙化的属性：

| 名称                                              | 说明                                                                                                                        | 类型                                                                                                | 是否必填 | 原库平台          | 鸿蒙支持 |
| ------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- | -------- | ----------------- | -------- |
| `source`                                          | Loads static HTML or a URI (with optional headers) in the WebView                                                           | One of: <br />**Load uri :**<br />uri <br />headers <br />**Static HTML :**<br />html <br />baseUrl | yes      | All               | yes      |
| `injectedJavaScript?`                             | Set this to provide JavaScript that will be injected into the web page after the document finishes loading                  | string                                                                                              | No       | All               | yes      |
| `originWhitelist?`                                | List of origin strings to allow being navigated to.                                                                         | string[]                                                                                            | No       | iOS,android,macOS | yes      |
| `scalesPageToFit?`                                | Boolean that controls whether the web content is scaled to fit the view and enables the user to change the scale.           | boolean                                                                                             | No       | android           | yes      |
| `startInLoadingState?`                            | Boolean value that forces the WebView to show the loading view on the first load.                                           | boolean                                                                                             | No       | iOS,android,macOS | yes      |
| `style?`                                          | A style object that allow you to customize the WebView style.                                                               | Style                                                                                               | No       | ALL               | yes      |
| `domStorageEnabled?`                              | Boolean value to control whether DOM Storage is enabled. Used only in Android.                                              | boolean                                                                                             | No       | android           | yes      |
| `javaScriptEnabled?`                              | Boolean value to enable JavaScript in the WebView.                                                                          | boolean                                                                                             | No       | All               | yes      |
| `showsHorizontalScrollIndicator?`                 | Boolean value that determines whether a horizontal scroll indicator is shown in the WebView.                                | boolean                                                                                             | No       | iOS,android,macOS | yes      |
| `showsVerticalScrollIndicator`                    | Boolean value that determines whether a vertical scroll indicator is shown in the WebView.                                  | boolean                                                                                             | No       | iOS,android,macOS | yes      |
| `cacheEnabled?`                                   | Sets whether WebView should use browser caching.                                                                            | boolean                                                                                             | No       | iOS,android,macOS | yes      |
| `cacheMode?`                                      | Overrides the way the cache is used.                                                                                        | string                                                                                              | No       | android           | yes      |
| `textZoom?`                                       | If the user has set a custom font size in the Android system, an undesirable scale of the site interface in WebView occurs. | number                                                                                              | No       | android           | yes      |
| ` injectJavaScript?: (script: string) => void`    | Executes the JavaScript string.                                                                                             | function                                                                                            | No       | iOS,android,macOS | yes      |
| ` onLoadEnd?: (event) => void`                    | Function that is invoked when the WebView load succeeds or fails used.                                                      | function                                                                                            | No       | All               | yes      |
| ` onMessage?: (event) => void`                    | Function that is invoked when the webview calls window.ReactNativeWebView.postMessage.                                      | function                                                                                            | No       | iOS,android,macOS | yes      |
| ` onShouldStartLoadWithRequest?: (event) => void` | Function that allows custom handling of any web view requests.                                                              | function                                                                                            | No       | iOS,android,macOS | yes      |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-webview/react-native-webview/blob/master/LICENSE) ，请自由地享受和参与开源。
