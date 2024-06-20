> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-permissions</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/zoontek/react-native-permissions">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/zoontek/react-native-permissions/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-permissions)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-permissions Releases](https://github.com/react-native-oh-library/react-native-permissions/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-permissions@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-permissions@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import { ScrollView, StyleSheet, View, Text, Button } from "react-native";
import React from "react";
import RTNPermissions, { Permission } from "react-native-permissions";

const permissionNormal: Permission[] = [
  "ohos.permission.APPROXIMATELY_LOCATION",
  "ohos.permission.CAMERA",
  "ohos.permission.MICROPHONE",
  "ohos.permission.READ_CALENDAR",
  "ohos.permission.WRITE_CALENDAR",
  "ohos.permission.ACTIVITY_MOTION",
  "ohos.permission.READ_HEALTH_DATA",
  "ohos.permission.DISTRIBUTED_DATASYNC",
  "ohos.permission.READ_MEDIA",
  "ohos.permission.MEDIA_LOCATION",
  "ohos.permission.ACCESS_BLUETOOTH",
];

export function PermissionsExample() {
  return (
    <View style={styles.sectionContainer}>
      <Button
        title="查询相机权限"
        onPress={async () => {
          let check = await RTNPermissions.check("ohos.permission.CAMERA");
          console.info("RTNPermissions===== check", check);
        }}
      />
      <Button
        title="设置相机权限"
        onPress={async () => {
          let request = await RTNPermissions.request("ohos.permission.CAMERA");
          console.info("RTNPermissions===== request", request);
        }}
      />
      <Button
        label={"查询多个权限"}
        onPress={async () => {
          let checkMultiple = await RTNPermissions.checkMultiple(
            permissionNormal
          );
          console.info("RTNPermissions===== checkMultiple", checkMultiple);
        }}
      />
      <Button
        label={"设置多个权限"}
        onPress={async () => {
          let requestMultiple = await RTNPermissions.requestMultiple(
            permissionNormal
          );
          console.info("RTNPermissions===== requestMultiple", requestMultiple);
        }}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  view: {
    width: "100%",
    display: "flex",
    flexDirection: "row",
    justifyContent: "space-evenly",
    flexWrap: "wrap",
    margin: 5,
  },
});
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

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "react-native-permissions": "file:../../node_modules/@react-native-oh-tpl/react-native-permissions/harmony/permissions.har"
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

### 配置 CMakeLists 和引入 PermissionsPackage

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
+ add_subdirectory("${OH_MODULE_DIR}/react-native-permissions/src/main/cpp" ./permissions)
# RNOH_END: add_package_subdirectories

add_library(rnoh_app SHARED
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)

target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: link_packages
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC rnoh_permissions)
# RNOH_END: link_packages
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "PermissionsPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<PermissionsPackage>(ctx)
    };
}
```

### 在 ArkTs 侧引入 PermissionsPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import {PermissionsPackage} from 'react-native-permissions/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new PermissionsPackage(ctx),
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-permissions Releases](https://github.com/react-native-oh-library/react-native-permissions/releases)

### 权限申请使用的工作流程

应用在访问数据或者执行操作时，需要评估该行为是否需要应用具备相关的权限。如果确认需要目标权限，则需要在应用安装包中申请目标权限。

然后，需要判断目标权限是否属于用户授权类。如果是，应用需要使用动态授权弹框来提供用户授权界面，请求用户授权目标权限。

当用户授予应用所需权限后，应用可成功访问目标数据或执行目标操作。

```
   ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
   ┃ check(ohos.permission.CAMERA)    ┃
   ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                   │
       Is the feature available
           on this device ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                 ┌─────────────────────┐
                ╚═════╝                 │ RESULTS.UNAVAILABLE │
                   │                    └─────────────────────┘
           Is the permission
             requestable ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                  ┌───────────────────┐
                ╚═════╝                  │ RESULTS.BLOCKED / │
                   │                     │  RESULTS.GRANTED  │
                   │                     └───────────────────┘
  				   │
                   ▼
  	┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
  	┃ request(ohos.permission.CAMERA)    ┃
  	┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                   │
         Does the user accept
            the request ?
                   │           ╔════╗
                   ├───────────║ NO ║──────────────┐
                   │           ╚════╝              │
                ╔═════╗                            ▼
                ║ YES ║                   ┌─────────────────┐
                ╚═════╝                   │ RESULTS.BLOCKED │
                   │                      └─────────────────┘
                   ▼
          ┌─────────────────┐
          │ RESULTS.GRANTED │
          └─────────────────┘
```

### 权限要求

需要在`entry/src/main/module.json5`中声明权限并创建 reason string value。

```
"requestPermissions": [
      {
        "name" : "ohos.permission.PERMISSION1",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when":"inuse"
        }
      },
      {
        "name" : "ohos.permission.PERMISSION2",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when":"always"
        }
      }
]
```

reason 字段的内容写作规范及建议如下：

    保持句子简洁、不要加入多余的分割符号。

    建议句式：用于某事。

    示例：用于扫码拍照。

```
    {
      "name": "reason",
      "value": "允许应用使用相机。"
    },
```

### 权限等级说明

根据权限对于不同等级应用有不同的开放范围，权限类型对应分为以下三种，等级依次提高。

- **normal 权限**

  normal 权限允许应用访问超出默认规则外的普通系统资源。这些系统资源的开放（包括数据和功能）对用户隐私以及其他应用带来的风险很小。

  该类型的权限仅向 APL 等级为 normal 及以上的应用开放。

- **system_basic 权限**

  system_basic 权限允许应用访问操作系统基础服务相关的资源。这部分系统基础服务属于系统提供或者预置的基础功能，比如系统设置、身份认证等。这些系统资源的开放对用户隐私以及其他应用带来的风险较大。

  该类型的权限仅向 APL 等级为 system_basic 及以上的应用开放。

```
normal权限列表
    'ohos.permission.APPROXIMATELY_LOCATION',
    'ohos.permission.LOCATION_IN_BACKGROUND'
    'ohos.permission.LOCATION'
    'ohos.permission.CAMERA',
    'ohos.permission.MICROPHONE',
    'ohos.permission.READ_CALENDAR',
    'ohos.permission.WRITE_CALENDAR',
    'ohos.permission.ACTIVITY_MOTION',
    'ohos.permission.READ_HEALTH_DATA',
    'ohos.permission.DISTRIBUTED_DATASYNC',
    'ohos.permission.READ_MEDIA',
    'ohos.permission.MEDIA_LOCATION',
    'ohos.permission.ACCESS_BLUETOOTH'

system_basic列表
    'ohos.permission.READ_WHOLE_CALENDAR'
    'ohos.permission.WRITE_WHOLE_CALENDAR'
    'ohos.permission.ANSWER_CALL'
    'ohos.permission.MANAGE_VOICEMAIL'
    'ohos.permission.READ_CONTACTS'
    'ohos.permission.WRITE_CONTACTS'
    'ohos.permission.READ_CALL_LOG'
    'ohos.permission.WRITE_CALL_LOG'
    'ohos.permission.READ_CELL_MESSAGES'
    'ohos.permission.READ_MESSAGES'
    'ohos.permission.RECEIVE_MMS'
    'ohos.permission.RECEIVE_SMS'
    'ohos.permission.RECEIVE_WAP_MESSAGES'
    'ohos.permission.SEND_MESSAGES'
    'ohos.permission.WRITE_AUDIO'
    'ohos.permission.READ_AUDIO'
    'ohos.permission.READ_DOCUMENT'
    'ohos.permission.WRITE_DOCUMENT'
    'ohos.permission.WRITE_IMAGEVIDEO'
    'ohos.permission.READ_IMAGEVIDEO'
    'ohos.permission.GET_INSTALLED_BUNDLE_LIST'

```

注：
ohos.permission.LOCATION_IN_BACKGROUND 允许应用在后台运行时获取设备位置信息。
由于安全隐私要求，应用不能通过弹窗的形式被授予后台位置权限，应用如果需要使用后台位置权限，需要引导用户到设置界面手动授予。
申请流程：
通过弹窗申请前台位置权限。存在两种允许情况：
申请前台模糊位置权限：ohos.permission.APPROXIMATELY_LOCATION。
申请前台精确位置权限：ohos.permission.APPROXIMATELY_LOCATION 和 ohos.permission.LOCATION。
当用户点击弹窗授予前台位置权限后，应用通过弹窗、提示窗等形式告知用户前往设置界面授予后台位置权限。
用户在设置界面中的选择“始终允许”应用访问位置信息权限，完成手动授予。

## 方法

| Name                    | Description                | Platform    | HarmonyOS Support        |
| ----------------------- | -------------------------- | ----------- | ------------------------ |
| check                   | 检查单个权限               | ios,android | yes                      |
| checkNotifications      | 检查通知权限               | ios,android | yes                      |
| openSettings            | 打开设置页                 | ios,android | yes                      |
| request                 | 设置单个权限               | ios,android | yes                      |
| requestNotifications    | 设置通知权限               | ios,android | yes                      |
| checkMultiple           | 检查多个权限               | android     | yes                      |
| requestMultiple         | 设置多个权限               | android     | yes                      |
| checkLocationAccuracy   | 检查设备位置权限           | ios         | no(使用 check()查询权限) |
| requestLocationAccuracy | 请求访问设备位置的权限     | ios         | no(使用 check()设置权限) |
| openPhotoPicker         | 请求访问设备本地图片的权限 | ios         | no(使用 check()设置权限) |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-permissions/blob/master/LICENSE) ，请自由地享受和参与开源。
