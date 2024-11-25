> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>@react-native-community/push-notification-ios</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/react-native-push-notification/ios">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-push-notification/ios/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-push-notification-ios)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/push-notification-ios Releases](https://github.com/react-native-oh-library/react-native-push-notification-ios/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/push-notification-ios
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/push-notification-ios
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React, { useState } from "react";
import { View, Text, Button } from "react-native";

import PushNotification from "@react-native-community/push-notification-ios";

export const App = () => {
  const [data, setData] = useState({});

  const addNotificationRequest = () => {
    PushNotification.addNotificationRequest({
      id: "test",
      title: "title",
      subtitle: "subtitle",
      body: "body",
      fireDate: new Date(new Date().valueOf() + 1000),
      repeats: true,
    });
  };

  const addSilentNotificationRequest = () => {
    PushNotification.addNotificationRequest({
      id: "test-4",
      title: "title",
      subtitle: "subtitle",
      body: "body",
      isSilent: true,
      fireDate: new Date(new Date().valueOf() + 2000),
      repeats: true,
      userInfo: {
        data: "123456",
      },
    });
  };

  const addMultipleRequests = () => {
    PushNotification.addNotificationRequest({
      id: "test-1",
      title: "First",
      subtitle: "subtitle",
      body: "First Notification out of 3",
      fireDate: new Date(new Date().valueOf() + 10000),
      repeats: true,
    });

    PushNotification.addNotificationRequest({
      id: "test-2",
      title: "Second",
      subtitle: "subtitle",
      body: "Second Notification out of 3",
      fireDate: new Date(new Date().valueOf() + 12000),
      repeats: true,
    });

    PushNotification.addNotificationRequest({
      id: "test-3",
      title: "Third",
      subtitle: "subtitle",
      body: "Third Notification out of 3",
      fireDate: new Date(new Date().valueOf() + 14000),
      repeats: true,
    });
  };

  const removeAllDeliveredNotifications = () => {
    PushNotification.removeAllDeliveredNotifications();
  };

  const removeDeliveredNotifications = () => {
    PushNotification.removeDeliveredNotifications(["test-1", "test-2"]);
  };

  const getDeliveredNotifications = () => {
    PushNotification.getDeliveredNotifications((data) => {
      if (data) {
        setData(data);
      } else {
        console.log("failed");
      }
    });
  };

  return (
    <View style={{ flexDirection: "column", justifyContent: "space-between" }}>
      <Button
        title="Add Notification Request"
        onPress={addNotificationRequest}
      />
      <Button
        title="Add Slient Notification Request"
        onPress={addSilentNotificationRequest}
      />
      <Button
        title="Add Multiple Notification Requests"
        onPress={addMultipleRequests}
      />
      <Button
        title="Set app's icon badge to 42"
        onPress={() => PushNotification.setApplicationIconBadgeNumber(42)}
      />
      <Button
        title="Clear app's icon badge"
        onPress={() => PushNotification.setApplicationIconBadgeNumber(0)}
      />
      <Button
        title="Remove All Delivered Notification Requests"
        onPress={removeAllDeliveredNotifications}
      />
      <Button
        title="Remove Delivered Notification Requests"
        onPress={removeDeliveredNotifications}
      />
      <View>
        <Button
          title="Get Delivered Notification"
          onPress={getDeliveredNotifications}
        />
        <Text>{JSON.stringify(data)}</Text>
      </View>
    </View>
  );
};
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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",

    "@react-native-oh-tpl/push-notification-ios": "file:../../node_modules/@react-native-oh-tpl/push-notification-ios/harmony/push_notification.har"
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

### 3.配置 CMakeLists 和引入 PushNotificationPackage

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
+ add_subdirectory("${OH_MODULES}/@react-native-oh-tpl/push-notification-ios/src/main/cpp" ./push_notification)
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
+ target_link_libraries(rnoh_app PUBLIC rnoh_push_notification)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

```diff
#include "RNOH/PackageProvider.h"
#include "SamplePackage.h"
+ #include "PushNotificationPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
      std::make_shared<SamplePackage>(ctx),
+     std::make_shared<PushNotificationPackage>(ctx)
    };
}
```

### 4.在 ArkTs 侧引入 PushNotificationPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { PushNotificationPackage } from '@react-native-oh-tpl/push-notification-ios/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new PushNotificationPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/push-notification-ios Releases](https://github.com/react-native-oh-library/react-native-push-notification-ios/releases)


## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                            | Description                                                                                                       | Type     | Required | Platform      | HarmonyOS Support |
| ------------------------------- | ----------------------------------------------------------------------------------------------------------------- | -------- | -------- | ------------- | ----------------- |
| addNotificationRequest          | Sends notificationRequest to notification center at specified firedate. Fires immediately if firedate is not set. | function | no       | iOS | yes               |
| getDeliveredNotifications       | Provides you with a list of the app’s notifications that are still displayed in Notification Center               | function | no       | iOS           | yes               |
| removeAllDeliveredNotifications | Remove all delivered notifications from Notification Center                                                       | function | no       | iOS           | yes               |
| removeDeliveredNotifications    | Removes the specified delivered notifications from Notification Center                                            | function | no       | iOS           | yes               |
| setApplicationIconBadgeNumber   | Sets the badge number for the app icon on the home screen                                                         | function | no       | iOS           | yes               |
| getApplicationIconBadgeNumber   | Gets the current badge number for the app icon on the home screen                                                         | function | no       | iOS           | no               |
| cancelLocalNotifications   | Cancel local notifications                                                         | function | no       | iOS           | no               |
| requestPermissions   | Requests notification permissions from iOS, prompting the user's dialog box. By default, it will request all notification permissions, but a subset of these can be requested by passing a map of requested permissions. The following permissions are supported                                                         | function | no       | iOS           | no               |
| abandonPermissions   | Unregister for all remote notifications received via Apple Push Notification service                                                         | function | no       | iOS           | no               |
| checkPermissions   | See what push permissions are currently enabled                                                         | function | no       | iOS           | no               |
| getInitialNotification   | This method returns a promise. If the app was launched by a push notification, this promise resolves to an object of type PushNotificationIOS. Otherwise, it resolves to null.                                                         | function | no       | iOS           | no               |
| getScheduledLocalNotifications   | Gets the local notifications that are currently scheduled                                                         | function | no       | iOS           | no               |

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


**Parameters:**

_NotificationRequest:_

| Name       | Description                                                       | Type    | Required | Platform | HarmonyOS Support |
| ---------- | ----------------------------------------------------------------- | ------- | -------- | -------- | ----------------- |
| `id`       | Identifier of the notification                                    | string  | yes      | All      | yes               |
| `title`    | A short description of the reason for the notification            | string  | yes      | All      | yes               |
| `subtitle` | A secondary description of the reason for the notification        | string  | no       | All      | no               |
| `body`     | The message displayed in the notificatio                          | string  | yes      | All      | yes               |
| `badge`    | The number to display as the app's icon badge                     | number  | no       | All      | yes               |
| `fireDate` | The date and time when the system should deliver the notification | object  | no       | All      | no               |
| `repeats`  | Sets notification to repeat                                       | boolean | no       | All      | no               |
| `repeatsComponent`  | An object indicating which parts of fireDate should be repeated                                       | object | no       | All      | no               |
| `sound`  | The sound played when the notification is fired                                       | string | no       | All      | no               |
| `category`  | The category of this notification, required for actionable notifications                                       | string | no       | All      | no               |
| `isSilent` | If true, the notification will appear without sound               | boolean | no       | All      | yes               |
| `isCritical` |  If true, the notification sound be played even when the device is locked, muted, or has Do Not Disturb enabled               | boolean | no       | All      | no               |
| `criticalSoundVolume` | A number between 0 and 1 for volume of critical notification. Default volume will be used if not specified               | number | no       | All      | no               |
| `userInfo` | An object containing additional notification data                 | object  | no       | All      | yes               |
| `isTimeZoneAgnostic` | If true, fireDate adjusted automatically upon time zone changes (e.g. for an alarm clock)                 | boolean  | no       | All      | no               |
| `interruptionLevel` | A string specifying the interruption level. Valid values are `'active'`, `'passive'`, `'timeSensitive'`, or `'critical'`                 | string  | no       | All      | no               |

## 遗留问题

- [ ] HarmonyOS 的 NotificationManager 的规格和 IOS 不一致，其 NotificationRequest 所含参数，在 HarmonyOS 上部分没有适配对应参数，问题: [issue#1](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/4)
- [ ] 原库部分接口在 HarmonyOS 中没有对应接口处理相关逻辑，问题: [issue#2](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-push-notification/ios/blob/master/LICENSE) ，请自由地享受和参与开源。