> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-push-notification-ios)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/push-notification-ios Releases](https://github.com/react-native-oh-library/react-native-push-notification-ios/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

    "@react-native-oh-tpl/push-notification-ios": "file:../../node_modules/@react-native-oh-tpl/push-notification-ios/harmony/push_notification.har"
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

### 3. Configuring CMakeLists and Introducing PushNotificationPackage

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

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

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

### 4.Introducing PushNotificationPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/push-notification-ios Releases](https://github.com/react-native-oh-library/react-native-push-notification-ios/releases)


## APIs

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Properties

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

- [ ] HarmonyOS 的 NotificationManager 的规格和 IOS 不一致，其 NotificationRequest 所含参数，在 HarmonyOS 上部分没有适配对应参数，问题: [issue#1](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/4)
- [ ] 原库部分接口在 HarmonyOS 中没有对应接口处理相关逻辑，问题: [issue#2](https://github.com/react-native-oh-library/react-native-push-notification-ios/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/react-native-push-notification/ios/blob/master/LICENSE).
