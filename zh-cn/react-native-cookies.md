> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>@react-native-cookies/cookies</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-cookies/cookies/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>




> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-cookies/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/cookies Releases](https://github.com/react-native-oh-library/react-native-cookies/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**
```bash
npm install @react-native-oh-tpl/cookies@file:#
```
**yarn**

```
yarn add @react-native-oh-tpl/cookies@file:#
```

<!-- tabs:end -->

HarmonyOS中使用react-native-cookies需要配合react-native-webview使用，具体请参考[@react-native-oh-tpl/react-native-webview](/zh-cn/react-native-webview.md)

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```ts
import React, { useState, useRef } from 'react';
import {ScrollView, StyleSheet, Text ,View, TouchableOpacity} from 'react-native';
import CookieManager from '@react-native-cookies/cookies';
import { WebView } from 'react-native-webview';

export interface Cookie {
  name: string;
  value: string;
  path?: string;
  domain?: string;
  version?: string;
  expires?: string;
  secure?: boolean;
  httpOnly?: boolean;
}

export interface Cookies {
  [key: string]: Cookie;
}

export function CookiesPage() {
  const httpUrl = 'https://www.baidu.com';
  const [result, setResult] = useState('请点击按钮，进行操作');
  const webViewRef = useRef(null);
  return (
    <View style={styles.container}>
      <View style={styles.pageArea}>
        <WebView source={{uri: httpUrl }}  ref={webViewRef} />;
      </View>
      
      <ScrollView style={styles.resultArea}>
        <Text>{result}</Text>
      </ScrollView>

      <TouchableOpacity style={styles.button} onPress={async() => {
        let cookieResult = await CookieManager.clearAll(true);
        let result = cookieResult ? '清除所有cookie成功' : '清除所有cookie失败';
        setResult(result + '');
      }} >
        <Text>clearAll()【清除所有cookie】</Text>
      </TouchableOpacity>
      
      <TouchableOpacity style={styles.button} onPress={async() => {
        let cookieResult = await CookieManager.get(httpUrl, true);
        setResult(JSON.stringify(cookieResult));
      }} >
        <Text>get()【根据url获取cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity style={styles.button} onPress={async() => {
        let curCookie: Cookie = {name: 'myAddCookie', value: 'myNewCookie'};
        let cookieResult = await CookieManager.set(httpUrl, curCookie, true);
        let result = cookieResult ? '根据url设置cookie成功' : '根据url设置cookie失败';
        setResult(result);
      }} >
        <Text>set()【根据url设置cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity style={styles.button} onPress={async() => {
         let cookieResult = await CookieManager.clearByName(httpUrl, 'myAddCookie', true);
         let result = cookieResult ? '根据名称删除cookie成功' : '根据名称删除cookie失败';
         setResult(result);
      }} >
        <Text>clearByName()【根据名称删除cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity style={styles.button} onPress={() => {
        CookieManager.flushForHarmony(() => {
          if (webViewRef.current) {
            webViewRef.current.reload();
          }
        });
        setResult('刷新cookie成功');
      }} >
        <Text>flush()【刷新cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity style={styles.button} onPress={async() => {
        let cookieResult = await CookieManager.removeSessionCookies();
        let result = cookieResult ? '清除会话cookie成功' : '清除会话cookie失败';
        setResult(result);
      }} >
        <Text>removeSessionCookies()【清除会话cookie】</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    height: '100%',
    alignItems: 'center'
  },
  pageArea: {
    width: '95%',
    height: 80
  },
  resultArea: {
    width: '95%',
    borderWidth: 2,
    borderColor: 'gray',
    borderRadius: 10,
    marginTop: 5
  },
  button: {
    backgroundColor: '#FF0000',
    paddingHorizontal: 16,
    paddingVertical: 10,
    borderRadius: 24,
    alignItems: 'center',
    justifyContent: 'center',
    elevation: 4,
    width: '80%',
    marginTop: 5
  },
});
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
    "rnoh": "file:../rnoh",
    "rnoh-cookies": "file:../../node_modules/@react-native-oh-tpl/cookies/harmony/rn_cookies.har",
    ...
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "rnoh": "file:../rnoh",
    "rnoh-cookies": "file:../../node_modules/@react-native-oh-tpl/cookies/harmony/rn_cookies",
    ...
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 配置 CMakeLists 和引入 cookies、webview

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(OH_MODULE_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
set(RNOH_CPP_DIR "${OH_MODULE_DIR}/rnoh/src/main/cpp")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-cookies/src/main/cpp" ./rn_cookies)
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-webview/src/main/cpp" ./rn_webview)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_cookies)
+ target_link_libraries(rnoh_app PUBLIC rnoh_webview)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "CookiesPacakge.h"
+ #include "WebViewPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<RNOHGeneratedPackage>(ctx), std::make_shared<SamplePackage>(ctx),
+     std::make_shared<CookiesPackage>(ctx), std::make_shared<WebViewPackage>(ctx)};
    };
}
```

### 在 ArkTs 侧引入 webView组件

找到 **function buildCustomComponent()**，一般位于 `entry/src/main/ets/pages/index.ets` 或 `entry/src/main/ets/rn/LoadBundle.ets`，添加：

```diff
...
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
    ...
+   else if (ctx.componentName === WEB_VIEW) {
+     WebView({
+       ctx: ctx.rnohContext,
+       tag: ctx.tag,
+       buildCustomComponent: buildCustomComponent
+     })
+   }
    ...
  }
  ...
```

### 在 ArkTs 侧引入 CookiesPackage和WebViewPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {CookiesPackage} from 'rnoh-cookies/ts';
+ import { WebViewPackage } from 'rnoh-webview/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx), 
+  	new CookiesPackage(ctx), 
+  	new WebViewPackage(ctx)
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

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/cookies Releases](https://github.com/react-native-oh-library/react-native-cookies/releases)

### 方法

| Name                 | Description | Platform    | HarmonyOS Support |
| -------------------- | ----------- | ----------- | ----------------- |
| clearAll             |             | ios,android | yes               |
| get                  |             | ios,android | yes               |
| set                  |             | ios,android | yes               |
| clearByName          |             | ios         | yes               |
| flush                |             | android     | yes               |
| removeSessionCookies |             | ios,android | yes               |
| getAll               |             | ios         | no                |
| setFromResponse      |             | ios         | no                |
| getFromResponse      |             | ios         | no                |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-cookies/blob/sig/LICENSE) ，请自由地享受和参与开源。