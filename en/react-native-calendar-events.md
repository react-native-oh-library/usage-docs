> Template version: v0.2.2

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

> [!tip] [Github address](https://github.com/react-native-oh-library/react-native-calendar-events)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-calendar-events Releases](https://github.com/react-native-oh-library/react-native-calendar-events/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-calendar-events
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-calendar-events
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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
import RNCalendarEvents from 'react-native-calendar-events';

const sourceStruct = {
    /** The Account name */
    name: "testName",
    /** The Account type */
    type: "testTyoe",
}

//saveEvent
const calendarOptions = {
    title: 'test1',
    type: 'local',
    displayName: "testSaveCalendar"
};

//saveEvent
const location = {
    location: "nanjin",
    longitude: 118,
    latitude: 31,
}
const eventService = {
    type: 'Meeting',
    uri: "",
    description: "testEventService",
}
const attendees = {
    name: "testAttendees",
    email: "testEmail",
}
const recurrenceRuleHarmony = {
    recurrenceFrequency: 2,
    expire: 0,
}
const eventDetails = {
    id: 1,
    type: 0,
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

## Use Codegen

This repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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
    "@react-native-oh-tpl/react-native-calendar-events": "file:../../node_modules/@react-native-oh-tpl/react-native-calendar-events/harmony/calendar_events.har"
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

### 3. Introducing  CalendarEventPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { CalendarEventPackage } from "@react-native-oh-tpl/react-native-calendar-events/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CalendarEventPackage(ctx),
  ];
}
```

### 4. Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-calendar-events Releases](https://github.com/react-native-oh-library/react-native-calendar-events/releases)

### Permission Requirements

#### Add permissions in the module.json5 file under the entry directory.

Open `entry/src/main/module.json5`, add the following permission:

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.READ_CALENDAR",
+    "reason": "$string:Access_calendar",
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

#### Add the description for requiring calendar permissions in the entry directory

Open `entry/src/main/resources/base/element/string.json`, add the following content:

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

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                  | Description                                                                                     | Type      | Required | Platform | HarmonyOS Support |
|-----------------------|-------------------------------------------------------------------------------------------------|-----------| -------- |----------|------------------|
| requestPermissions((readOnly = false))  | Request calendar authorization. Authorization must be granted before accessing calendar events. | function  | No       | All      | yes              |
| checkPermissions((readOnly = false))    | Get calendar authorization status.                                                              | function  | No       | All      | yes              |
| findCalendars()       | Finds all the calendars on the device.                                                          | function  | No       | All      | yes              |
| saveCalendar(calendar)        | Create a calendar.                                                                              | function  | No       | All      | yes              |
| removeCalendar(id)      | Removes a calendar.                                                                             | function  | No       | All      | yes              |
| findEventById(id)       | Find calendar  by id.                                                                           | function  | No       | All      | yes              |
| fetchAllEvents(startDate, endDate, calendars)      | Fetch all calendar events.                                                                      | function  | No       | All      | yes              |
| saveEvent(title, details, options)           | Creates or updates a calendar event. To update an event, the event id must be defined.          | function  | No       | All      | yes              |
| removeEvent(id, options)         | Removes calendar event.                                                                         | function  | No       | All      | yes              |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/wmcmahan/react-native-calendar-events/blob/master/LICENSE.md).
