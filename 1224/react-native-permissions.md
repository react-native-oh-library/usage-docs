> 模板版本：v0.1.3

<p align="center">
  <h1 align="center"> <code>react-native-permissions</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonday/react-native-permissions">
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

>[!WARNING] 使用时 import 的库名不变。

```js
import { ScrollView, StyleSheet, View, Text, Button } from 'react-native';
import React from 'react';
import RTNPermissions, { Permission } from 'react-native-permissions';

const permissionNormal: Permission[] = [
    'ohos.permission.APPROXIMATELY_LOCATION',
    'ohos.permission.CAMERA',
    'ohos.permission.MICROPHONE',
    'ohos.permission.READ_CALENDAR',
    'ohos.permission.WRITE_CALENDAR',
    'ohos.permission.ACTIVITY_MOTION',
    'ohos.permission.READ_HEALTH_DATA',
    'ohos.permission.DISTRIBUTED_DATASYNC',
    'ohos.permission.READ_MEDIA',
    'ohos.permission.MEDIA_LOCATION',
    'ohos.permission.ACCESS_BLUETOOTH',
]

export function PermissionsExample() {
    return (
        <View style={styles.sectionContainer}>
            <Button title='查询相机权限'
                onPress={async () => {
                    let check = await RTNPermissions.check('ohos.permission.CAMERA');
                    console.info('RTNPermissions===== check', check);
                }} />
            <Button title='设置相机权限'
                 onPress={async () => {
                    let request = await RTNPermissions.request('ohos.permission.CAMERA');
                    console.info('RTNPermissions===== request', request);
                 }} />
			<Button
                label={'查询多个权限'}
                onPress={async () => {
                    let checkMultiple = await RTNPermissions.checkMultiple(permissionNormal);
                    console.info('RTNPermissions===== checkMultiple', checkMultiple);
                }} />
           <Button
               label={'设置多个权限'}
               onPress={async () => {
                   let requestMultiple = await RTNPermissions.requestMultiple(permissionNormal);
                   console.info('RTNPermissions===== requestMultiple', requestMultiple);
               }} />
        </View>
    );
}

const styles = StyleSheet.create({
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
   	view: {
   	   width: '100%',
   	   display: 'flex',
   	   flexDirection: 'row',
   	   justifyContent: 'space-evenly',
   	   flexWrap: 'wrap',
   	   margin: 5,
    }
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
    "react-native-permissions": "file:../../node_modules/react-native-permissions/harmony/permissions.har"
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
    "react-native-permissions": "file:../../node_modules/react-native-permissions/harmony/permissions"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

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

### 权限要求

需要在`entry/src/main/oh-package.json5`中声明权限。

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

权限列表

```
'ohos.permission.APPROXIMATELY_LOCATION',
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
```



## 方法

| Name                       | Description | Platform    | HarmonyOS Support |
| -------------------------- | ----------- | ----------- | ----------------- |
| check                      |             | ios,android | yes               |
| checkNotifications         |             | ios,android | no                |
| getConstants               |             | ios,android | no                |
| openSettings               |             | ios,android | no                |
| request                    |             | ios,android | yes               |
| requestNotifications       |             | ios,android | yes               |
| checkMultiple              |             | android     | yes               |
| requestMultiple            |             | android     | yes               |
| shouldShowRequestRationale |             | android     | no                |
| checkLocationAccuracy      |             | ios         | no                |
| openPhotoPicker            |             | ios         | no                |
| requestLocationAccuracy    |             | ios         | no                |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-permissions/blob/master/LICENSE) ，请自由地享受和参与开源。

