> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>rn-bugly</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yz1311/rn-bugly">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/rn-bugly)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/rn-bugly Releases](https://github.com/react-native-oh-library/rn-bugly/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/rn-bugly
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/rn-bugly
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import {
    ScrollView,
    View,
    Button
} from 'react-native';
import RNBugly from 'rn-bugly';
export default class BuglyExample extends React.Component {
    _init() {
        RNBugly.init("appid", "appkey");
    }
    _setUserId() {
        RNBugly.setUserId("123456");
    }
    _setDeviceID() {
        RNBugly.setDeviceID("666666677777");
    }
    _setDeviceModel() {
        RNBugly.setDeviceModel("HUAWEI Mate 60 Pro");
    }
    _setAppVersion() {
        RNBugly.setAppVersion("2.0.2");
    }
    _setAppChannel() {
        RNBugly.setAppChannel("HarmonyOS");
    }
    _putUserData() {
        RNBugly.putUserData("name", "xiaoli");
    }
    _postException() {
        RNBugly.postException({ category: 1, errorType: "test", errorMsg: "throw new err" });
    }
    render() {
        return (
            <View
                style={{ flex: 1, backgroundColor: 'green', justifyContent: 'center', alignItems: 'center' }}
            >
                <ScrollView
                    style={{ flex: 1, width: '100%', height: '100%', marginTop: 150 }}
                >
                    <Button title='setAppVersion' onPress={this._setAppVersion} />
                    <Button title='setAppChannel' onPress={this._setAppChannel} />
                    <Button title='setUserId' onPress={this._setUserId} />
                    <Button title='setDeviceID' onPress={this._setDeviceID} />
                    <Button title='setDeviceModel' onPress={this._setDeviceModel} />
                    <Button title='init' onPress={this._init} />
                    <Button title='putUserData' onPress={this._putUserData} />
                    <Button title='postException' onPress={this._postException} />
                </ScrollView>
            </View>
        );
    }
}
```
## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`

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
    "@react-native-oh-tpl/rn-bugly": "file:../../node_modules/@react-native-oh-tpl/rn-bugly/harmony/bugly.har"
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

### 3.配置 CMakeLists 和引入 RNBuglyPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/rn-bugly/src/main/cpp" ./bugly)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_bugly)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNBuglyPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNBuglyPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 RNBuglyPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import {RNBuglyPackage} from '@react-native-oh-tpl/rn-bugly/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNBuglyPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/rn-bugly Releases](https://github.com/react-native-oh-library/rn-bugly/releases)

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- |-------- | -------- | ------------------ |
| init | Initialize SDK | function  |Yes | Android | Yes |
| setUserId | Set the current user ID | function  |No       | iOS/Android     | Yes      |
| setAppVersion | Set custom version information | function  |No       | iOS/Android      | Yes      |
| setDeviceID | Set device ID | function  |Yes | Android | Yes |
| setDeviceModel| Set device model | function  |No | Android | Yes |
| setAppChannel | Set channel name | function  |No | Android | Yes |
| setAppPackage | Set custom package name | function  |No | Android | No |
| setTag | Custom tags | function  |No | iOS/Android | No |
| startCrashReport | Open CrashReport | function  |No | Android | No |
| closeCrashReport| Close CrashReport | function  |No | iOS/Android | No |
| getCurrentTag | Get the current setting label | function  |No | iOS/Android | No |
| getUserData | Obtain key data | function  |No | iOS/Android | No |
| getBuglyVersion | Get the version of SDK | function  |No | iOS/Android | No |
| putUserData | Custom Map parameters can save some custom environment information when a crash occurs | function  |No | iOS/Android | Yes |
| getUpgradeInfo | Retrieve the existing upgrade strategy locally                 | function  |No | Android | No |
| checkUpgrade | Check for version updates | function  |No | Android | No |
| log | Print log | function  |No | Android | No |
| postException | Report custom exceptions | function  |No | iOS/Android | Yes |

## 遗留问题

- [ ] setAppPackage不支持[issue#1](https://github.com/react-native-oh-library/rn-bugly/issues/1)
- [ ] setTag不支持[issue#2](https://github.com/react-native-oh-library/rn-bugly/issues/2)
- [ ] startCrashReport不支持[issue#3](https://github.com/react-native-oh-library/rn-bugly/issues/3)
- [ ] closeCrashReport不支持[issue#4](https://github.com/react-native-oh-library/rn-bugly/issues/4)
- [ ] getCurrentTag不支持[issue#5](https://github.com/react-native-oh-library/rn-bugly/issues/5)
- [ ] getUserData不支持[issue#6](https://github.com/react-native-oh-library/rn-bugly/issues/6)
- [ ] getBuglyVersion不支持[issue#7](https://github.com/react-native-oh-library/rn-bugly/issues/7)
- [ ] getUpgradeInfo不支持[issue#8](https://github.com/react-native-oh-library/rn-bugly/issues/8)
- [ ] checkUpgrade不支持[issue#9](https://github.com/react-native-oh-library/rn-bugly/issues/9)
- [ ] log不支持[issue#10](https://github.com/react-native-oh-library/rn-bugly/issues/10)


## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://mit-license.org/) ，请自由地享受和参与开源。