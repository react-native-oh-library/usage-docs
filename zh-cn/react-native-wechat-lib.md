> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-wechat-lib</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/little-snow-fox/react-native-wechat-lib">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/little-snow-fox/react-native-wechat-lib/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-wechat-lib)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-ohos/react-native-wechat-lib Releases](https://github.com/react-native-oh-library/react-native-wechat-lib/releases)。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-wechat-lib
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-wechat-lib
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [tips] 下面 demo 在使用的过程中，请将 AppID 改为在[微信开放平台申请鸿蒙应用](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/ohos.html)的 AppID

```js
import * as React from 'react';

import { StyleSheet, View, Text, Button, Alert } from 'react-native';
import { getApiVersion, registerApp, openWXApp, sendAuthRequest, shareText } from 'react-native-wechat-lib';

export default function App() {
  const [versionNumber, setVersionNumber] = React.useState<string | undefined>();

  React.useEffect(() => {
    registerApp('AppID', 'universalLink').then((res) => {
      console.log("registerApp: " + res)
    });

  }, []);

  function onLogin() {
    sendAuthRequest('snsapi_userinfo', '')
      .then((response: any) => {
        Alert.alert('登录成功，code: ' + response.code)
      })
      .catch(error => {
        console.log(error)
        let errorCode = Number(error.code);
        if (errorCode === -2) {
          Alert.alert('已取消授权登录')
        } else {
          Alert.alert('微信授权登录失败')
        }
      });

  }

  function onShareText() {
    shareText({
      text: 'test content.',
      scene: 0
    }).then()
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Call wechat SDK demo</Text>
      <Text style={styles.versionBox}>
        Version: {versionNumber}
      </Text>
      <View style={styles.buttonGroup}>
        <View style={styles.button}>
          <Button title={'拉起微信'} onPress={() => { openWXApp().then() }} />
        </View>
        <View style={styles.button}>
          <Button title={'授权登录'} onPress={() => { onLogin() }} />
        </View>
        <View style={styles.button}>
          <Button title={'分享'} onPress={() => { onShareText() }} />
        </View>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    // flex: 1,
    alignItems: 'center',
    // justifyContent: 'center',
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
  title: {
    marginTop: 48,
    fontSize: 24,
    color: 'rgba(0, 0, 0, 0.6)',
  },
  versionBox: {
    color: 'rgba(0, 0, 0, 0.6)'
  },
  buttonGroup: {
    width: '100%',
    padding: 6,
    marginTop: 24,
  },
  button: {
    margin: 6,

  }
});
```

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

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
    "@react-native-ohos/react-native-wechat-lib": "file:../../node_modules/@react-native-ohos/react-native-wechat-lib/harmony/react_native_wechat_lib.har"
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

### 3.配置 EntryAbility

鸿蒙工程下 EntryAbility，一般位于 `entry\src\main\ets\entryability\EntryAbility.ets`

```diff
import {RNAbility} from '@rnoh/react-native-openharmony';
+ import { AbilityConstant, Want } from '@kit.AbilityKit';
+ import { WechatLibTurboModule } from '@react-native-ohos/react-native-wechat-lib';

export default class EntryAbility extends RNAbility {

+   onCreate(want: Want) {
+     super.onCreate(want)
+     this.handleWeChatCallIfNeed(want)
+   }

  getPagePath() {
    return 'pages/Index';
  }

+  onNewWant(want: Want, _launchParam: AbilityConstant.LaunchParam): void {
+    this.handleWeChatCallIfNeed(want)
+  }

+  private handleWeChatCallIfNeed(want: Want) {
+    WechatLibTurboModule.handleWant(want)
+  }}

```

### 4.配置 module.json5

打开 `entry/src/main/module.json5`，添加：

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",
    "description": "$string:module_desc",
    "mainElement": "EntryAbility",
    "deviceTypes": [
      "default"
    ],
+   "querySchemes": [
+     "weixin",
+   ],
    ...
  }
}
```

### 5.配置 CMakeLists 和引入 RNWechatLibPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-wechat-lib/src/main/cpp" ./wechat-lib)
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
+ target_link_libraries(rnoh_app PUBLIC wechat_lib)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNWechatLibPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNWechatLibPackage>(ctx),
    };
}
```

### 6.在 ArkTs 侧引入 WechatLibPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { WechatLibPackage } from '@react-native-ohos/react-native-wechat-lib/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new WechatLibPackage(ctx),
  ];
}
```

### 7.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-wechat-lib](https://github.com/react-native-oh-library/react-native-wechat-lib/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

> [!TIP] 移动应用跳转至小程序的规则，[请见APP拉起小程序的功能介绍](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Launching_a_Mini_Program/Launching_a_Mini_Program.html)

| Name                                          | Description        | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------------------------- | ------------------ | -------- | -------- | ----------- | ----------------- |
| registerApp(appid)                            | 注册               | Function | no       | Android/iOS | yes               |
| isWXAppInstalled()                            | 判断微信是否已安装 | Function | no       | Android/iOS | yes                |
| isWXAppSupportApi()                           | 检查支持情况       | Function | no       | Android/iOS | no                |
| getApiVersion()                               | 获取 API 版本号    | Function | no       | Android/iOS | no                |
| openWXApp()                                   | 打开微信           | Function | no       | Android/iOS | yes               |
| sendAuthRequest([scope[, state]])             | 微信授权登录       | Function | no       | Android/iOS | yes               |
| shareText(ShareTextMetadata)                  | 分享/收藏 文本     | Function | no       | Android/iOS | partially         |
| shareImage(ShareImageMetadata)                | 分享/收藏 图片     | Function | no       | Android/iOS | partially         |
| shareLocalImage(ShareImageMetadata)           | 分享/收藏 本地图片 | Function | no       | Android/iOS | partially         |
| shareFile(ShareFileMetadata)                  | 分享文件           | Function | no       | Android/iOS | no                |
| shareMusic(ShareMusicMetadata)                | 分享音频           | Function | no       | Android/iOS | no                |
| shareVideo(ShareVideoMetadata)                | 分享视频           | Function | no       | Android/iOS | no                |
| shareWebpage (ShareWebpageMetadata)           | 分享网页           | Function | no       | Android/iOS | no                |
| shareMiniProgram(ShareMiniProgramMetadata)    | 分享小程序         | Function | no       | Android/iOS | no                |
| launchMiniProgram (LaunchMiniProgramMetadata) | 跳到小程序         | Function | no       | Android/iOS | yes               |
| chooseInvoice (ChooseInvoice)                 | 选择发票           | Function | no       | Android/iOS | no                |
| pay(payload)                                  | 支付               | Function | no       | Android/iOS | yes               |
| subscribeMessage(SubscribeMessageMetadata)    | 一次性订阅消息     | Function | no       | Android/iOS | no                |

## 遗留问题

## 其他

- ShareText、ShareImage、ShareLocalImage 只支持分享，不支持收藏，原因为目前微信 Open SDK 还不支持 HarmonyOS 平台的收藏
- isWXAppSupportApi、getApiVersion、ShareFile、ShareMusic、ShareVideo、ShareWebpage 、ShareMiniProgram、ChooseInvoice、subscribeMessage 这些接口目前在 HarmonyOS 微信 Open SDK 还不支持

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/little-snow-fox/react-native-wechat-lib/blob/master/LICENSE) ，请自由地享受和参与开源。
