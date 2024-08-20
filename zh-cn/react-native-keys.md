> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-keys</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/numandev1/react-native-keys">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/numandev1/react-native-keys/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>



> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-keys)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-keys Releases](https://github.com/react-native-oh-library/react-native-keys/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-keys@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-keys@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

1. Create a new file keys.development.json in the root of your React Native app and add Envs in secure object for protected envs variables and add Envs in public for public usage this:
 
```json
{
  "secure": {
    "GOOGLE_API": "ABCD",
    "BRANCH_API": "ABCDEF"
  },
  "public": {
    "APP_NAME": "Keys Example",
    "BUNDLE_ID": "com.example.rnkeys.dev",
    "ANDROID_CODE": "50",
    "PACKAGE_ID": "com.example.rnkeys.dev"
  }
}

```

2. Use Public Keys & Secure Keys

``` js
import Keys from 'react-native-keys';

Keys.API_URL;
Keys.URI_SCHEME;

Keys.secureFor('API_TOKEN');
Keys.secureFor('GOOGLE_API_KEY');
Keys.secureFor('SECRET_KEY');

```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides字段

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

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-keys": "file:../../node_modules/@react-native-oh-tpl/react-native-keys/harmony/rnoh_keys.har"
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

### 配置 CMakeLists 和引入 RNOHKeysPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-keys/src/main/cpp" ./rnohkeys)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_keys)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "RNKeysPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<RNOHKeysPackage>(ctx),
    };
}
```

### 在 ArkTs 侧引入 RNKeysPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNKeysPackage } from '@react-native-oh-tpl/react-native-keys';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNKeysPackage(ctx)
  ];
}
```

### 在 DevEco 创建运行前script（生成加解密代码和编译配置文件）

> [!TIP] 如下步骤中添加配置完成时记得点击Apply按钮让配置生效

1. 点击右上角 entry -> Edit Configurations... 打开配置面板
2. 点击面板左上角 + , 选择Shell Script, 打开新建 script的配置面板, 按如下图片提示进行配置  
   ![shell script config](../img/rnkeys/RNKeys_Script_Config.PNG)
3. 配置entry -> Before Lunch，点击加号选择 Run Another Configuration， 选择上一步配置的 Shell Script, 并将配置拖动到Hvigor-Build Make上方  
   ![entry config](../img/rnkeys/entry_config.PNG)

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-keys Releases](https://github.com/react-native-oh-library/react-native-keys/releases)

   
## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


| Name            | Description          | Type     | Required | Platform    | HarmonyOS Support |
|-----------------|----------------------|----------|----------|-------------|-------------------|
| Keys attributes | Get public value     | object   | no       | iOS/Android | yes               |
| Keys.publicKeys | Get all public value | function | no       | iOS/Android | yes               |
| Keys.secureFor  | Get secret value     | function | no       | iOS/Android | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/numandev1/react-native-keys/blob/main/LICENSE) ，请自由地享受和参与开源。
