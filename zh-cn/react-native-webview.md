> 模板版本：v0.2.1

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

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-webview)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-webview Releases](https://github.com/react-native-oh-library/react-native-webview/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-webview@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-webview@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { WebView } from "react-native-webview";

export default function WebViewDemo() {
  return (
    <View>
      <WebView source={{ uri: "https://reactnative.dev/" }} />
    </View>
  );
}
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides 字段


```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```


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

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 配置 CMakeLists 和引入 WebViewPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(OH_MODULE "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: add_package_subdirectories
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE}/rnoh-webview/src/main/cpp" ./webview)
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

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
+ import { WebView, WEB_VIEW } from "rnoh-webview"

@Builder
function buildCustomComponent(ctx: ComponentBuilderContext) {
  if (ctx.componentName === SAMPLE_VIEW_TYPE) {
    SampleView({
      ctx: ctx.rnComponentContext,
      tag: ctx.tag,
      buildCustomComponent: buildCustomComponent
    })
  }
+ if (ctx.componentName === WEB_VIEW) {
+   WebView({
+     ctx: ctx.rnComponentContext,
+     tag: ctx.tag
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

## 约束与限制

## 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[ @react-native-oh-tpl/react-native-webview Releases](https://github.com/react-native-oh-library/react-native-webview/releases)

本文档内容基于以下版本验证通过：

RNOH: 0.72.26; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.300; ROM: 3.0.0.22;

## 属性

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请查看[webview 官方文档](https://github.com/react-native-webview/react-native-webview/blob/master/docs/Reference.md)

如下是 webview 已经鸿蒙化的属性：

> [!tip] "鸿蒙支持"列为 yes 的属性表示支持鸿蒙平台，并且效果对标"原库平台"列中的 ios 或 android 的效果。

| Name                                               | Description                                                  | Type     | Required | Platform          | HarmonyOS Support                                            |
| -------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- | ------------------------------------------------------------ |
| `source`                                           | Loads static HTML or a URI (with optional headers) in the WebView | object   | yes      | All               | partially (Only of:  **Load uri :** uri  headers  **Static HTML :** html  baseUrl) |
| `injectedJavaScript?`                              | Set this to provide JavaScript that will be injected into the web page after the document finishes loading | string   | No       | All               | yes                                                          |
| `originWhitelist?`                                 | List of origin strings to allow being navigated to.          | string[] | No       | iOS,android,macOS | yes                                                          |
| `scalesPageToFit?`                                 | Boolean that controls whether the web content is scaled to fit the view and enables the user to change the scale. | boolean  | No       | android           | yes                                                          |
| `startInLoadingState?`                             | Boolean value that forces the WebView to show the loading view on the first load. | boolean  | No       | iOS,android,macOS | yes                                                          |
| `style?`                                           | A style object that allow you to customize the WebView style. | Style    | No       | ALL               | yes                                                          |
| `domStorageEnabled?`                               | Boolean value to control whether DOM Storage is enabled. Used only in Android and harmony. | boolean  | No       | android           | yes                                                          |
| `javaScriptEnabled?`                               | Boolean value to enable JavaScript in the WebView.           | boolean  | No       | All               | yes                                                          |
| `showsHorizontalScrollIndicator?`                  | Boolean value that determines whether a horizontal scroll indicator is shown in the WebView. | boolean  | No       | iOS,android,macOS | yes                                                          |
| `showsVerticalScrollIndicator`                     | Boolean value that determines whether a vertical scroll indicator is shown in the WebView. | boolean  | No       | iOS,android,macOS | yes                                                          |
| `cacheEnabled?`                                    | Sets whether WebView should use browser caching.             | boolean  | No       | iOS,android,macOS | yes                                                          |
| `cacheMode?`                                       | Overrides the way the cache is used.                         | string   | No       | android           | yes                                                          |
| `textZoom?`                                        | If the user has set a custom font size in the Android and harmony system, an undesirable scale of the site interface in WebView occurs. | number   | No       | android           | yes                                                          |
| `injectJavaScript?: (script: string) => void`      | Executes the JavaScript string.                              | function | No       | iOS,android,macOS | yes                                                          |
| `onLoadEnd?: (event) => void`                      | Function that is invoked when the WebView load succeeds or fails used. | function | No       | All               | yes                                                          |
| `onMessage?: (event) => void`                      | Function that is invoked when the webview calls window.ReactNativeWebView.postMessage. | function | No       | iOS,android,macOS | yes                                                          |
| `onShouldStartLoadWithRequest?: (event) => void`   | Function that allows custom handling of any web view requests. | function | No       | iOS,android,macOS | yes                                                          |
| `reload?`                                          | Reloads the current page.                                    | function | No       | iOS,android,macOS | yes                                                          |
| `stopLoading?`                                     | Stop loading the current page.                               | function | No       | iOS,android,macOS | yes                                                          |
| `goBack?`: () => void                              | Go back one page in the web view's history.                  | function | No       | iOS,android,macOS | yes                                                          |
| `goForward?`: () => void                           | Go forward one page in the web view's history.               | function | No       | iOS,android,macOS | yes                                                          |
| `requestFocus?`: () => void                        | Request the webView to ask for focus.                        | function | No       | iOS,android,macOS | yes                                                          |
| `clearCache?`: (includeDiskFiles: boolean) => void | Clears the resource cache.                                   | function | No       | iOS,android,macOS | yes                                                          |
| `clearHistory?`: () => void                        | Tells this WebView to clear its internal back/forward list.  | function | No       | android           | yes                                                          |
| `loadUrl?`: (url: string) => void                  | Loads a specified URL.                                       | function | No       | -                 | yes                                                          |
| `incognito?`                                       | Does not store any data within the lifetime of the WebView.  | boolean  | NO       | All               | yes                                                          |

## 遗留问题

- [ ]  webview 部分属性未实现鸿蒙化[issue#17](https://github.com/react-native-oh-library/react-native-webview/issues/17)
- [X]  中文乱码[issue#18](https://github.com/react-native-oh-library/react-native-webview/issues/18)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-webview/react-native-webview/blob/master/LICENSE) ，请自由地享受和参与开源。
[react-native-vconsole.md](react-native-vconsole.md)
