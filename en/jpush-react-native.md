> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>jpush-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jpush/jpush-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jpush/jpush-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/jpush-react-native)


## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/jpush-react-native Releases](https://github.com/react-native-oh-library/jpush-react-native/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/jpush-react-native
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/jpush-react-native
```
<!-- tabs:end -->

Additionally, it is necessary to follow the [Aurora Push SDK HarmonyOS Integration Guide]（ https://docs.jiguang.cn/jpush/client/HarmonyOS/hmos_guide ）Complete the configuration related to Aurora Push

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from 'react';
import { Text, View, Button } from 'react-native';
import JPush from 'jpush-react-native';

function App() {
    let localNotification = { messageID: '1', title: 'add local notification', content: 'Test adding a local notification', broadcastTime: new Date().getTime(), extras: { content: 'Additional content' } };
    return (
        <View>
                <Text style={{
                    color: "#555",
                    fontSize: 25,
                    marginTop: 100,
                    padding:20,
                    fontWeight: "500"
                }}>jpush-react-native</Text>
                <Text style={{
                    color: "#999",
                    fontSize: 15,
                    marginBottom:20,
                    padding:20,
                }}>Please go to your phone's "Settings" ->"Notifications and Status Bar" to open the notification for the test application first</Text>
                <View>
                     <Button
                        key="addLocalNotification"
                        title="addLocalNotification"
                        onPress={async () => {
                          JPush.addLocalNotification(localNotification);
                        }}
                     />
                </View>
        </View>
    );
}
export default App;
```
## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

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
    "@react-native-oh-tpl/jpush-react-native": "file:../../node_modules/@react-native-oh-tpl/jpush-react-native/harmony/jpush_react_native.har"
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


### 3. Introducing RNJPushPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
+ import {RNJPushPackage} from  "@react-native-oh-tpl/jpush-react-native/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNJPushPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/jpush-react-native Releases](https://github.com/react-native-oh-library/jpush-react-native/releases)

## Static Methods

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| -------------------- | ------------------- | ------ | ------ | ---------- | ----------- |
|   setLoggerEnable(enable: boolean): void  |   To set the debug mode, which is disabled by default, and if the RN (React Native) side configuration does not work, please follow the [ JPush SDK-HarmonyOS Integration Guide](https://docs.jiguang.cn/jpush/client/HarmonyOS/hmos_guide)for proper setup.    | function   | no | iOS,Android      | yes |
|  init(params: {appKey: string;channel:string;production:string;}): void  |If the initialization of JPush on the RN (React Native) side is not working, please follow the integration instructions provided in the[JPush SDK-HarmonyOS Integration Guide](https://docs.jiguang.cn/jpush/client/HarmonyOS/hmos_guide)to properly set it up.  |  function   | yes | iOS,Android      | yes |
|  getRegistrationID(callback: Callback<{ registerID: string }>): void  |  Retrieve the RegistrationID corresponding to the application  | function   | no | iOS,Android      | yes |
|  addTags(params: {"sequence":number,"tags":string[]}): void  |   Add a tag   |function   | no | iOS,Android      | yes |
|   updateTags(params: {"sequence":number,"tags":string[]}): void  | Overwrite tags  | function   | no | iOS,Android      |yes |
|  deleteTag(params: {"sequence":number,"tags":string[]}): void  | Delete a specified tag  | function  | no | iOS,Android      |yes |
|  deleteTags(params: {"sequence":number}): void  | Clear all tags  | function  | no | iOS,Android      |yes |
|   queryTag(params:{"sequence":number,"tag":string}): void  | Query the binding status of a specified tag with the current user  | function  | no | iOS,Android      |yes |
|  queryTags(params: {"sequence":number}): void  | Query all tags.  | function  | no | iOS,Android      |yes |
|  setAlias(params: {"sequence":number,"alias":string}): void  | Set an alias.  | function  | no | iOS,Android      |yes |
|  deleteAlias({"sequence":number}): void  | Delete an alias.  | function  | no | iOS,Android      |yes |
|  queryAlias(params: {"sequence":number}): void  | Query an alias.  | function  | no | iOS,Android      |yes |
|   setProperties(params:{pros:any}):void; |   Set personalized push attributes/update user-specified personalized push attributes.   |function   | no | iOS,Android     | no |
|   deleteProperties(params:{pros:any}):void; |   Delete specified personalized push attributes.   |function   | no | iOS,Android     | no |
|  cleanProperties():void; |   Clear all personalized push attributes.  |function   | no | iOS,Android     | no |
|  pageEnterTo(pageName: string): void  | Enter a page.  | function  | no | iOS,Android      |no |
|  pageLeave(pageName: string): void  | Leave a page.  | function  | no | iOS,Android      |no |
|  setMobileNumber(params: {"sequence":number,"mobileNumber":string}): void  | Set a phone number. This interface controls the call frequency, with a maximum of 3 calls within 10 seconds.  | function  | no | iOS,Android      |yes |
|  initCrashHandler(): void  | Enable CrashLog reporting.  | function  | no | iOS,Android      |no |
|  setPowerSaveMode(enable: boolean):void  | Enable or disable power-saving mode for the Push SDK (default: disabled).  | function  | no | Android      |no |
|  isNotificationEnabled(callback: Callback<boolean>): void  | Check if the notification switch for the current application is enabled.  | function  | no | iOS,Android      |yes |
|  addLocalNotification(params:{messageID: stringtitle: string;content: string;extras: Extra}): void  | Add a local notification.  | function  | no | iOS,Android      |yes |
|   removeLocalNotification(params: { messageID: string }): void  | Remove a specified local notification.  | function  | no | iOS,Android      |yes |
|  clearLocalNotifications(): void  | Remove all local notifications.  | function  | no | iOS,Android      |yes |
|  clearAllNotifications():void  | Clear all JPush-displayed notifications (excluding those not displayed by the JPush SDK).  | function  | no | Android      |no |
|  clearNotificationById(params: {notificationId:number}):void  | Delete a specified notification.  | function  | no | iAndroid      |no |
|  setMaxGeofenceNumber(params: {geoFenceMaxNumber:number}): void  | Set the maximum number of allowed geofences. When exceeding this limit, the earliest created geofence will be deleted first if new ones are created. The default number is 10, with a minimum of 1 and a maximum of 100 allowed.  | function  | no | iOS,Android      |no |
|  deleteGeofence(params: { geoFenceID: string }): void |  Delete a geofence with a specified ID.  | function  | no | iOS,Android      |no |
|  addConnectEventListener(callback: Callback<{connectEnable: boolean }>): void  | Monitor connection status.  | function  | no | iOS,Android      |yes |
|  addCommandEventListener(callback: Callback<{ cmd:number, errorCode:number,msg:string,extra:Extra}>): void  | CommandEvent callback.  | function  | no | iOS,Android      |yes |
|   addNotificationListener(callback: Callback <{messageID:string;title:string;content:string;extras:Extra;notificationEventType: "notificationArrived" "notificationOpened"}>):void  | Remote notification event.  | function  | no | iOS,Android      |no |
|  addLocalNotificationListener(callback: Callback <{messageID:string;title:string;content:string;extras:Extra;notificationEventType: "notificationArrived" "notificationOpened"}>  | Local notification event.  | function  | no | iOS,Android      |yes |
|  addCustomMessageListener(callback: Callback<{messageID: string;content: string;extras: Extra;title:string}>):void  | Custom message notification callback.  | function  | no | iOS,Android      |yes |
| addInappMessageListener(callback: Callback<{mesageId: string;title: string;content: string;target:string;clickAction: string;extras:Extra:inappEventType: "inappShow"  "inappClick"}>):void| In-app message event.  | function  | no | iOS,Android      |no |
|  addTagAliasListener(callback: Callback<{ code: number;tagEnable: boolean;Tags:string[];alias:string;sequence:number}>): void  | Tag/alias event.  | function  | no | iOS,Android      |yes |
|  addMobileNumberListener(callback: Callback<{ code: number;sequence:number }>): void  | Phone number event.  | function  | no | iOS,Android      |yes |
|  removeListener(callback: Function): void  | Remove event listeners.  | function  | no | iOS,Android      |yes |
|  requestPermission(): void  | Certain permissions need to be requested on systems running Android 6.0 and above.  | function  | no | Android   |no |
|  stopPush(): void  | Stop the push service.  | function  | no | Android      |yes |
|  resumePush(): void  | Resume the push service.  | function  | no | iAndroid      |yes |
|  isPushStopped(callback: Callback<boolean>): void | Check if the Push Service has been stopped.  | function  | no | Android      |yes |
|  setPushTime(params: {pushTimeDays: number[];pushTimeStartHour: number;pushTimeEndHour: number;}):void  | Set allowed push times.  | function  | no | Android      |no |
|  setSilenceTime(params: {silenceTimeStartHour: number;silenceTimeStartMinute: number;silenceTimeEndHour: number; silenceTimeEndMinute: number;}): void | Set the number of recently retained notifications (duplicate setting mentioned).  | function  | no | Android    |no |
|  setLatestNotificationNumber(params: {notificationMaxNumber: number;}): void  |   Set the number of recently retained notifications (duplicate setting mentioned).   |function   | no | Android      | no |
|  setChannel(params: { channel: string }): void  |   Dynamically configure channels with higher priority than those configured in the AndroidManifest.  |function   | no | Android      | no |
|  setBadge(params: {badge: number;appBadge: number;}):void  |   Set the Badge.   |function   | no | iOS,Android     | yes |
|  setChannelAndSound(params: {channel:string;sound:string;channelId:string}):void  |   Set notification channel sounds.   |function   | no | Android     | no |
|  setLinkMergeEnable(enable:boolean):void |   Enable or disable notification bundling.   |function   | no | Android     | no |
|  setSmartPushEnable(enable:boolean):void |   Enable or disable intelligent push.   |function   | no | iOS,Android     | no |
|  setGeofenceEnable(enable:boolean):void |   Enable or disable geofencing.   |function   | no |Android     | no |
|  setCollectControl(enable:boolean):void |   Enable or disable centralized control.   |function   | no | iOS、Android     | no |

## Known Issues
- [ ] setProperties、deleteProperties、cleanProperties、pageEnterTo、pageLeave、initCrashHandler、setMaxGeofenceNumber、deleteGeofence、addNotificationListener、addInappMessageListener，setCollectControl、setSmartPushEnable These methods are currently not supported in the Aurora Push HarmonyOS SDK[issue#1](https://github.com/react-native-oh-library/jpush-react-native/issues/1)

## Others


## License

This project is licensed under [The MIT License (MIT)](https://github.com/jpush/jpush-react-native/blob/master/LICENSE).