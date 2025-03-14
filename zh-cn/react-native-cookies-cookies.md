> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-cookies/cookies</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/react-native-cookies/cookies/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-cookies/cookies/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-cookies/tree/sig)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/cookies Releases](https://github.com/react-native-oh-library/react-native-cookies/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/cookies
```

#### **yarn**

```
yarn add @react-native-oh-tpl/cookies
```

<!-- tabs:end -->

HarmonyOS 中使用 react-native-cookies 需要配合 react-native-webview 使用，具体请参考[@react-native-oh-tpl/react-native-webview](/zh-cn/react-native-webview.md)

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState, useRef } from "react";
import {
  ScrollView,
  StyleSheet,
  Text,
  View,
  TouchableOpacity,
} from "react-native";
import CookieManager from "@react-native-cookies/cookies";
import { WebView } from "react-native-webview";

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

export default function CookiesPage() {
  const httpUrl = "https://www.baidu.com";
  const [result, setResult] = useState("请点击按钮，进行操作");
  const webViewRef = useRef(null);
  return (
    <View style={styles.container}>
      <View style={styles.pageArea}>
        <WebView source={{ uri: httpUrl }} ref={webViewRef} />;
      </View>

      <ScrollView style={styles.resultArea}>
        <Text>{result}</Text>
      </ScrollView>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.clearAll(true);
          let result = cookieResult
            ? "清除所有cookie成功"
            : "清除所有cookie失败";
          setResult(result + "");
        }}
      >
        <Text>clearAll()【清除所有cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.get(httpUrl, true);
          setResult(JSON.stringify(cookieResult));
        }}
      >
        <Text>get()【根据url获取cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let curCookie: Cookie = { name: "myAddCookie", value: "myNewCookie" };
          let cookieResult = await CookieManager.set(httpUrl, curCookie, true);
          let result = cookieResult
            ? "根据url设置cookie成功"
            : "根据url设置cookie失败";
          setResult(result);
        }}
      >
        <Text>set()【根据url设置cookie】</Text>
      </TouchableOpacity>

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.clearByName(
            httpUrl,
            "myAddCookie",
            true
          );
          let result = cookieResult
            ? "根据名称删除cookie成功"
            : "根据名称删除cookie失败";
          setResult(result);
        }}
      >
        <Text>clearByName()【根据名称删除cookie】</Text>
      </TouchableOpacity>   

      <TouchableOpacity
        style={styles.button}
        onPress={async () => {
          let cookieResult = await CookieManager.removeSessionCookies();
          let result = cookieResult
            ? "清除会话cookie成功"
            : "清除会话cookie失败";
          setResult(result);
        }}
      >
        <Text>removeSessionCookies()【清除会话cookie】</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: "100%",
    height: "100%",
    alignItems: "center",
  },
  pageArea: {
    width: "95%",
    height: 80,
  },
  resultArea: {
    width: "95%",
    borderWidth: 2,
    borderColor: "gray",
    borderRadius: 10,
    marginTop: 5,
  },
  button: {
    backgroundColor: "#FF0000",
    paddingHorizontal: 16,
    paddingVertical: 10,
    borderRadius: 24,
    alignItems: "center",
    justifyContent: "center",
    elevation: 4,
    width: "80%",
    marginTop: 5,
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

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    ...
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/cookies": "file:../../node_modules/@react-native-oh-tpl/cookies/harmony/rn_cookies.har",
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

### 3.配置 CMakeLists 和引入 CookiesPackage

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${OH_MODULES}/rnoh/src/main/cpp")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/cookies/src/main/cpp" ./rn_cookies)
# RNOH_BEGIN: manual_package_linking_1

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
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
...

+ #include "CookiesPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      ...
+     std::make_shared<CookiesPackage>(ctx),
    };
}
```

### 4.在 ArkTs 侧引入 CookiesPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {CookiesPackage} from '@react-native-oh-tpl/cookies/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    ...
+  	new CookiesPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/cookies Releases](https://github.com/react-native-oh-library/react-native-cookies/releases)

## 静态方法
> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                 | Description                                   | Type     | Required | Platform    | HarmonyOS Support |
| -------------------- | --------------------------------------------- | ---------|----------| ------------|-------------------|
| clearAll             |  Clear all cookies                            |function  |     NO   |iOS,Android  | yes               |
| get                  |  Get cookies based on url                     |function  |     NO   | iOS,Android | yes               |
| set                  |  Set cookie based on url                      |function  |     NO   | iOS,Android | yes               |
| clearByName          |  Delete cookies by name                       |function  |     NO   | iOS         | yes               |
| flush                |  Refresh cookies                              |function  |     NO   | Android     | no                |
| removeSessionCookies |  Clear session cookies                        |function  |     NO   | iOS,Android | yes               |
| getAll               |  Get all cookies                              |function  |     NO   | iOS         | no                |
| setFromResponse      |  Set cookies from a response header           |function  |     NO   | iOS         | no                |
| getFromResponse      |  Get cookies from a response header           |function  |     NO   | iOS         | no                |

## 遗留问题

- [ ] 这四个方法getAll,setFromResponse,getFromResponse,flush 在ios是可用的andriod不可用，Harmony没有对应的api 问题: [issue#1](https://github.com/react-native-oh-library/react-native-cookies/issues/1)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-cookies/cookies/blob/master/LICENSE) ，请自由地享受和参与开源。
