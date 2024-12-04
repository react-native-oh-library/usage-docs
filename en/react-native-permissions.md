> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-permissions)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-permissions Releases](https://github.com/react-native-oh-library/react-native-permissions/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-permissions
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-permissions
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] 在使用import...from "react-native-permissions" 导入时因为原库没有抛出关于HarmonyOS有关字段,在使用PERMISSIONS.HARMONY.ACCESS_BLUETOOTH编辑器会报ts类型错误没有HARMONY字段（使用可以正常编译运行），所以想要使用PERMISSIONS.HARMONY.ACCESS_BLUETOOTH，可以使用 import...from "@react-native-oh-tpl/react-native-permissions"

```js
import { ScrollView, StyleSheet, View, Text, Button } from "react-native";
import React from "react";
import RTNPermissions, { Permission } from "@react-native-oh-tpl/react-native-permissions";

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
        title={"查询多个权限"}
        onPress={async () => {
          let checkMultiple = await RTNPermissions.checkMultiple(
            permissionNormal
          );
          console.info("RTNPermissions===== checkMultiple", checkMultiple);
        }}
      />
      <Button
        title={"设置多个权限"}
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

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 1. Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/react-native-permissions": "file:../../node_modules/@react-native-oh-tpl/react-native-permissions/harmony/permissions.har"
  }
```

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3. Configuring CMakeLists and Introducing PermissionsPackage

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/react-native-permissions/src/main/cpp" ./permissions)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_permissions)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4.Introducing PermissionsPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {PermissionsPackage} from '@react-native-oh-tpl/react-native-permissions/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new PermissionsPackage(ctx),
  ];
}
```

### 5.Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-permissions Releases](https://github.com/react-native-oh-library/react-native-permissions/releases)

### 权限申请使用的工作流程

应用在访问数据或者执行操作时，需要评估该行为是否需要应用具备相关的权限。如果确认需要目标权限，则需要在应用安装包中申请目标权限。

然后，需要判断目标权限是否属于用户授权类。如果是，应用需要使用动态授权弹框来提供用户授权界面，请求用户授权目标权限。

当用户授予应用所需权限后，应用可成功访问目标数据或执行目标操作。

```
 ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
 ┃ check(ohos.permission.CAMERA) ┃
 ┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛
                │                                ┌─────────────────────┐
     Is the feature available ──────── NO ─────▶ │ RESULTS.UNAVAILABLE │
        on this device ?                         └─────────────────────┘
                │
               YES
                │                                ┌─────────────────┐
        Is the permission ─────────── YES ─────▶ │ RESULTS.GRANTED │
        already granted ?                        └─────────────────┘
                │
                NO
                │
  Is the permission requestable ?
                │
               YES
                │
                ▼
       ┌────────────────┐
       │ RESULTS.DENIED │
       └────────────────┘
                │
                ▼
┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
┃ request(ohos.permission.CAMERA) ┃◀—————————————————————┐
┗━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┛                      │
                │                                       YES
                │                                        │
      Did the user see and ──────── NO ──────── Is the permission
      accept the request ?                      still requestable ?
                │                                        │
               YES                                       NO
                │                                        │
                ▼                                        ▼
        ┌─────────────────┐                     ┌─────────────────┐
        │ RESULTS.GRANTED │                     │ RESULTS.BLOCKED │
        └─────────────────┘                     └─────────────────┘
```

### 权限要求

需要在`entry/src/main/module.json5`中声明权限并创建 reason string value。

```
"requestPermissions": [
      {
        "name" : "ohos.permission.CAMERA",
        "reason": "$string:reason",
        "usedScene": {
          "abilities": [
            "FormAbility"
          ],
          "when":"inuse"
        }
      },
      {
        "name" : "ohos.permission.ACCESS_BLUETOOTH",
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

## APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                    | Description    | Type           | Required | Platform    | HarmonyOS Support        |
| ----------------------- | ------------------|----|---------| ----------- | ------------------------ |
| check                   | 检查单个权限    | Function          | no      | iOS,Android | yes                      |
| checkNotifications      | 检查通知权限    | Function          | no      | iOS,Android | yes                      |
| openSettings            | 打开设置页      | Function          | no      | iOS,Android | yes                      |
| request                 | 设置单个权限    | Function          | no      | iOS,Android | yes                      |
| requestNotifications    | 设置通知权限    | Function          | no      | iOS,Android | yes                      |
| checkMultiple           | 检查多个权限    | Function          | no      | Android     | yes                      |
| requestMultiple         | 设置多个权限    | Function          | no      | Android     | yes                      |
| checkLocationAccuracy   | 检查设备位置权限  | Function          | no      | iOS         | no(使用 check()查询权限) |
| requestLocationAccuracy | 请求访问设备位置的权限  | Function          | no      | iOS         | no(使用 request()设置权限) |
| openPhotoPicker         | 打开图片选择 | Function          | no      | iOS         | yes( iOS 需要在`PhotoLibrary`权限为`limited`才能调用，HarmonyOS不需要任何权限直接调用) |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-permissions/blob/master/LICENSE).
