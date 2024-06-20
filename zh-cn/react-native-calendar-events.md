<!-- {% raw %} -->
> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-calendar-events</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wmcmahan/react-native-calendar-events">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/wmcmahan/react-native-calendar-events/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-calendar-events)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-calendar-events Releases](https://github.com/react-native-oh-library/react-native-calendar-events/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-calendar-events@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-calendar-events@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js

import React from 'react';
import {
    SafeAreaView,
    StyleSheet,
    ScrollView,
    View,
    Text,
    StatusBar,
    Button,
    Alert,
    Platform,
} from 'react-native';
import {Header, Colors} from 'react-native/Libraries/NewAppScreen';
import RNCalendarEvents from '@react-native-oh-tpl/react-native-calendar-events';
import {CalendarType, EventType, ServiceType, RecurrenceFrequency} from "@react-native-oh-tpl/react-native-calendar-events/src/calendarType"

const sourceStruct = {
    /** The Account name */
    name: "testName",
    /** The Account type */
    type: "testTyoe",
}

//saveEvent
const calendarOptions = {
    title: 'test1',
    type: CalendarType.LOCAL,
    displayName: "testSaveCalendar"
};

//saveEvent
const location = {
    location: "nanjin",
    longitude: 118,
    latitude: 31,
}
const eventService = {
    type: ServiceType.MEETING,
    uri: "",
    description: "testEventService",
}
const attendees = {
    name: "testAttendees",
    email: "testEmail",
}
const recurrenceRuleHarmony = {
    recurrenceFrequency: RecurrenceFrequency.WEEKLY,
    expire: 0,
}
const eventDetails = {
    id: 1,
    type: EventType.NORMAL,
    title: 'testEvent',
    location: location,
    startTime: new Date().getTime() + 60 * 60 * 1000 * 3,
    endTime: new Date().getTime() + 60 * 60 * 1000 * 10,
    isAllDay: false,
    attendee: [attendees],
    timeZone: "beijing",
    reminderTime: [new Date().getTime()],
    recurrenceRule: recurrenceRuleHarmony,
    description: "test",
    service: eventService,
};

const fetchAllEventStartTime: string = (new Date().getTime() + 60 * 60 * 1000).toString()
const fetchAllEventEndTime: string = (new Date().getTime() + 60 * 60 * 1000 * 15).toString()
function CalendarDemo() {
    return (
        <>
            <StatusBar barStyle="dark-content" />
            <SafeAreaView>
                <ScrollView
                    contentInsetAdjustmentBehavior="automatic"
                    style={styles.scrollView}>
                    <Header />
                    <View style={styles.engine}>
                        <Text style={styles.footer}>Engine: Hermes</Text>
                    </View>
    
                    <View style={styles.body}>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>Read/Write Auth</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="Request auth"
                                    onPress={() => {
                                        RNCalendarEvents.requestPermissions().then(
                                            (result) => {
                                                Alert.alert('Auth requested', result);
                                            },
                                            (result) => {
                                                console.error(result);
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>check auth</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="Check auth"
                                    onPress={() => {
                                        RNCalendarEvents.checkPermissions().then(
                                            (result) => {
                                                Alert.alert('Auth check', result);
                                            },
                                            (result) => {
                                                console.error(result);
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>Calendars</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="Find calendars"
                                    onPress={() => {
                                        RNCalendarEvents.findCalendars().then(
                                            (result) => {
                                                Alert.alert(
                                                    'Calendars',
                                                    result.reduce((acc: string[], cal) => {
                                                        acc.push(cal.title);
                                                        return acc;
                                                    }, []).join('\n'),
                                                );
                                            },
                                            (result) => {
                                                console.error(result);
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                    </View>
                </ScrollView>
            </SafeAreaView>
        </>
    );
};

const styles = StyleSheet.create({
    scrollView: {
        backgroundColor: Colors.lighter,
    },
    engine: {
        position: 'absolute',
        right: 0,
    },
    body: {
        backgroundColor: Colors.white,
    },
    sectionContainer: {
        marginTop: 32,
        paddingHorizontal: 24,
    },
    sectionTitle: {
        fontSize: 24,
        fontWeight: '600',
        color: Colors.black,
    },
    sectionDescription: {
        marginTop: 8,
        fontSize: 18,
        fontWeight: '400',
        color: Colors.dark,
    },
    highlight: {
        fontWeight: '700',
    },
    footer: {
        color: Colors.dark,
        fontSize: 12,
        fontWeight: '600',
        padding: 4,
        paddingRight: 12,
        textAlign: 'right',
    },
});

export default CalendarDemo;
```

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-calendar-events": "file:../../node_modules/@react-native-oh-tpl/react-native-calendar-events/harmony/calendar-events.har"
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

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 CalendarEventPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
import { CalendarEventPackage } from "@react-native-oh-tpl/react-native-calendar-events/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CalendarEventPackage(ctx),
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
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

本文档内容基于以下版本验证通过：

RNOH：0.72.23; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.19

### 权限要求

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.READ_CALENDAR",
+    "reason": "$string:calendarPermission",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when":"inuse"
+    }
+  },
+  {
+    "name": "ohos.permission.WRITE_CALENDAR",
+    "reason": "$string:Access_calendar",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when":"inuse"
+    }
+  }
]
```

#### 在 entry 目录下添加申请日历权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "Access_calendar",
+      "value": "access calendar"
+    }
  ]
}
```

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                  | Description                                                                                     | Type      | Required | Platform | HarmonyOS Support |
|-----------------------|-------------------------------------------------------------------------------------------------|-----------| -------- |----------|------------------|
| requestPermissions()  | Request calendar authorization. Authorization must be granted before accessing calendar events. | function  | No       | All      | yes              |
| checkPermissions()    | Get calendar authorization status.                                                              | function  | No       | All      | yes              |
| findCalendars()       | Finds all the calendars on the device.                                                          | function  | No       | All      | yes              |
| saveCalendar()        | Create a calendar.                                                                              | function  | No       | All      | yes              |
| removeCalendar()      | Removes a calendar.                                                                             | function  | No       | All      | yes              |
| findEventById()       | Find calendar  by id.                                                                           | function  | No       | All      | yes              |
| fetchAllEvents()      | Fetch all calendar events.                                                                      | function  | No       | All      | yes              |
| saveEvent()           | Creates or updates a calendar event. To update an event, the event id must be defined.          | function  | No       | All      | yes              |
| removeEvent()         | Removes calendar event.                                                                         | function  | No       | All      | yes              |

## 遗留问题
- 无

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wmcmahan/react-native-calendar-events/blob/master/LICENSE.md) ，请自由地享受和参与开源。
<!-- {% endraw %} -->