> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-exception-handler</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/a7ul/react-native-exception-handler">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/a7ul/react-native-exception-handler/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-exception-handler)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-exception-handler Releases](https://github.com/react-native-oh-library/react-native-exception-handler/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-exception-handler@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-exception-handler@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

To catch <b>JS_Exceptions</b>

<!-- {% raw %} -->
```typescript
import {
  setJSExceptionHandler,
  getJSExceptionHandler,
} from "react-native-exception-handler";

// For most use cases:
// registering the error handler (maybe u can do this in the index.android.js or index.ios.js)
setJSExceptionHandler((error, isFatal) => {
  // This is your custom global error handler
  // You do stuff like show an error dialog
  // or hit google analytics to track crashes
  // or hit a custom api to inform the dev team.
});
//=================================================
// ADVANCED use case:
const exceptionhandler = (error, isFatal) => {
  // your error handler function
};
setJSExceptionHandler(exceptionhandler, allowInDevMode);
// - exceptionhandler is the exception handler function
// - allowInDevMode is an optional parameter is a boolean.
//   If set to true the handler to be called in place of RED screen
//   in development mode also.

// getJSExceptionHandler gives the currently set JS exception handler
const currentHandler = getJSExceptionHandler();
```

To catch <b>Native_Exceptions</b>

```typescript
import { setNativeExceptionHandler } from "react-native-exception-handler";

//For most use cases:
setNativeExceptionHandler((exceptionString) => {
  // This is your custom global error handler
  // You do stuff likehit google analytics to track crashes.
  // or hit a custom api to inform the dev team.
  //NOTE: alert or showing any UI change via JS
  //WILL NOT WORK in case of NATIVE ERRORS.
});
//====================================================
// ADVANCED use case:
const exceptionhandler = (exceptionString) => {
  // your exception handler code here
};
setNativeExceptionHandler(
  exceptionhandler,
  forceAppQuit,
  executeDefaultHandler
);
// - exceptionhandler is the exception handler function
// - forceAppQuit is an optional ANDROID specific parameter that defines
//    if the app should be force quit on error.  default value is true.
//    To see usecase check the common issues section.
// - executeDefaultHandler is an optional boolean (both IOS, ANDROID)
//    It executes previous exception handlers if set by some other module.
//    It will come handy when you use any other crash analytics module along with this one
//    Default value is set to false. Set to true if you are using other analytics modules.
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```diff
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

+   "rnoh-exception-handler": "file:../../node_modules/@react-native-oh-tpl/react-native-exception-handler/harmony/exception_handler.har",
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

### 配置 CMakeLists 和引入 ExceptionHandlerPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/rnoh-exception-handler/src/main/cpp" ./exception_handler)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_exception_handler)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "ExceptionHandlerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<ExceptionHandlerPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 ExceptionHandlerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
import type {RNPackageContext, RNPackage} from 'rnoh/ts';
import {SamplePackage} from 'rnoh-sample-package/ts';
+ import {ExceptionHandlerPackage} from 'rnoh-exception-handler/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new ExceptionHandlerPackage(ctx)
  ];
}
```

### 异常信息页面配置

在 `YourProject/entry/src/main/ets/pages` 目录下,新建文件`ExceptionView.ets`

```typescript
import { ExceptionComponent } from 'rnoh-exception-handler';
import router from '@ohos.router';

interface RouterParam {
  errMsg: string
}

@Entry
@Component
struct ExceptionView {
  @State errMsg: string = ''

  aboutToAppear() {
    let params = router.getParams() as RouterParam
    this.errMsg = params.errMsg
    router.clear()
  }

  build() {
    Column() {
      ExceptionComponent({ errMsg: this.errMsg })
    }
    .width('100%')
    .height('100%')
  }
}
```

在 `YourProject/entry/src/main/resources/base/profile/main_pages.json5`补上配置

```diff
{
  "src": [
    "pages/Index",
+   "pages/ExceptionView"
  ]
}
```

### 应用重启使能

在 `YourProject/entry/src/main/ets/app` 目录下,新建文件`MyAbilityStage.ets`

```typescript
import AbilityStage from "@ohos.app.ability.AbilityStage";
import appRecovery from "@ohos.app.ability.appRecovery";
import Want from "@ohos.app.ability.Want";

export default class MyAbilityStage extends AbilityStage {
  onCreate() {
    appRecovery.enableAppRecovery();
    let want: Want = {
      bundleName: this.context.applicationInfo.name,
      abilityName: this.context.currentHapModuleInfo.mainElementName,
    };
    appRecovery.setRestartWant(want);
  }
}
```
<!-- {% endraw %} -->

在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",
+   "srcEntry": "./ets/app/MyAbilityStage.ets",
    "description": "$string:module_desc",
    "mainElement": "EntryAbility",

  ···

  "abilities": [
      {
        "name": "EntryAbility",
        "srcEntry": "./ets/entryability/EntryAbility.ets",
        "description": "$string:EntryAbility_desc",
        "icon": "$media:icon",
        "label": "$string:EntryAbility_label",
        "startWindowIcon": "$media:icon",
        "startWindowBackground": "$color:start_window_background",
+       "recoverable": true,
        "exported": true,
        "skills": [
          {
            "entities": [
              "entity.system.home"
            ],
            "actions": [
              "action.system.home"
            ]
          }
        ]
      }
    ]
  }
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/reace-native-exception-handler Releases](https://github.com/react-native-oh-library/react-native-exception-handler/releases)

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                    | Description          | Type     | Required | Platform | HarmonyOS Support |
| ----------------------- | -------------------- | -------- | -------- | -------- | ----------------- |
| `setJSExceptionHandler` | 设置 JS 异常处理方法 | function | no       | All      | yes               |
| `getJSExceptionHandler` | 获取 JS 异常处理方法 | function | no       | All      | yes               |

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                        | Description              | Type     | Required | Platform | HarmonyOS Support |
| --------------------------- | ------------------------ | -------- | -------- | -------- | ----------------- |
| `setNativeExceptionHandler` | 设置 native 异常处理方法 | function | no       | All      | yes               |

## 遗留问题

- [ ] Harmony 没有异常默认处理机制

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/a7ul/react-native-exception-handler/blob/master/LICENSE) ，请自由地享受和参与开源。
