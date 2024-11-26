> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>mixpanel-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/mixpanel/mixpanel-react-native/tree/master">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mixpanel/mixpanel-react-native/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-Apache%202.0-blue.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/mixpanel-react-native)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/mixpanel-react-native Releases](https://github.com/react-native-oh-library/mixpanel-react-native/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/mixpanel-react-native
```


#### **yarn**

```bash
yarn add @react-native-oh-tpl/mixpanel-react-native
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.
> [!WARNING] The token value used in the code needs to be obtained from the project settings on the[ Mixpanel website](https://mixpanel.com),After an event is sent, you can view the corresponding data in the project analytics on the[ Mixpanel website](https://mixpanel.com)

```js
import React from 'react';
import {Button, SafeAreaView} from 'react-native';
import {Mixpanel} from 'mixpanel-react-native';

const trackAutomaticEvents = false;
const token = 'Your Project Token';
const mixpanel = new Mixpanel(token, trackAutomaticEvents);
mixpanel.init();

export default function MixpanelDemo() {
    return (
    <SafeAreaView>
        <Button
    title="Select Premium Plan"
    onPress={() => mixpanel.track('Plan Selected', {Plan: 'Premium'})}
/>
    </SafeAreaView>
);
}
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

### 2.Introducing Native Code

Currently, two methods are available:

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
"@rnoh/react-native-openharmony": "file:../react_native_openharmony",
"@react-native-oh-tpl/mixpanel-react-native": "file:../../node_modules/@react-native-oh-tpl/mixpanel-react-native/harmony/mixpanel.har"
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

### 3. Introducing MixpanelPackage to ArkTS

 Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { MixpanelPackage } from '@react-native-oh-tpl/mixpanel-react-native/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new MixpanelPackage(ctx)
  ];
}
```

### 4.Running

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/mixpanel-react-native Releases](https://github.com/react-native-oh-library/mixpanel-react-native/releases)

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

#### Mixpanel

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---- | ----------- | ---- |----------| -------- |-------------------|
| init(): void; | Initialize a Mixpanel instance. | function | yes      | iOS,Android | yes               |
| setServerURL(serverURL: string): void; | Set the base URL for Mixpanel API requests. | function | no       | iOS,Android | yes               |
| setLoggingEnabled(loggingEnabled: boolean): void; | Enable or disable logging. | function | no       | iOS,Android | yes               |
| setFlushOnBackground(flushOnBackground: boolean): void; | On iOS, allow or disable Mixpanel from flushing events when the app enters the background. | function | no       | iOS | no                |
| setUseIpAddressForGeolocation(useIpAddressForGeolocation: boolean): void; | Enable or disable sending the IP address as a basis for geolocation. | function | no       | iOS,Android | yes               |
| setFlushBatchSize(flushBatchSize: number): void; | Set the number of events to send in a single network request to Mixpanel. | function | no       | iOS,Android | yes               |
| hasOptedOutTracking(): Promise<boolean>; | Check if a user has opted out of tracking. | function | no       | iOS,Android | yes               |
| optInTracking(): void; | User has opted to be tracked. | function | no       | iOS,Android | yes               |
| optOutTracking(): void; | User has opted out of tracking. | function | no       | iOS,Android | yes               |
| identify(distinctId: string): Promise<void>; | Associate future track calls with the following user identifier. | function | no       | iOS,Android | yes               |
| alias(alias: string, distinctId: string): void; | Create a mapping to associate a new identifier with the user's original distinct_id. | function | no       | iOS,Android | yes               |
| track(eventName: string, properties?: MixpanelProperties): void; | Send an event. | function | yes      | iOS,Android | yes               |
| getPeople(): People; | Obtain a People instance. | function | no       | iOS,Android | yes               |
| trackWithGroups(eventName: string, properties?: MixpanelProperties, groups?: MixpanelProperties): void; | Track events specific to a group of people. | function | no       | iOS,Android | no                |
| setGroup(groupKey: string, groupID: MixpanelType): void; | Set the group that a user belongs to. | function | no       | iOS,Android | no                |
| getGroup(groupKey: string, groupID: MixpanelType): MixpanelGroup; | Obtain a Group instance. | function | no       | iOS,Android | yes               |
| addGroup(groupKey: string, groupID: MixpanelType): void; | Add a group. | function | no       | iOS,Android | no                |
| removeGroup(groupKey: string, groupID: MixpanelType): void; | Remove a group. | function | no       | iOS,Android | no                |
| deleteGroup(groupKey: string, groupID: MixpanelType): void; | Delete a group. | function | no       | iOS,Android | no                |
| registerSuperProperties(properties: MixpanelProperties): void; | Register global properties that are common to all users.| function | no       | iOS,Android | yes               |
| registerSuperPropertiesOnce(properties: MixpanelProperties): void; | Register global properties that are common to all users without overwriting existing properties.| function | no       | iOS,Android | yes               |
| unregisterSuperProperty(propertyName: string): void; | Delete a specified registered global property. | function | no       | iOS,Android | yes               |
| getSuperProperties(): Promise<MixpanelProperties>; | Retrieve registered global properties. | function | no       | iOS,Android | yes               |
| clearSuperProperties(): void; | Delete all registered global properties. | function | no       | iOS,Android | yes               |
| timeEvent(eventName: string): void; | Send a timing event. | function | no       | iOS,Android | yes               |
| eventElapsedTime(eventName: string): Promise<number>; | Get the current timing for a specified event. | function | no       | iOS,Android | yes               |
| reset(): void; | Reset a user's related information. | function | no       | iOS,Android | yes               |
| getDistinctId(): Promise<string>; | Get the unique identifier. | function | no       | iOS,Android | yes               |
| getDeviceId(): Promise<string>; | Get the device identifier. | function | no       | iOS,Android | yes               |
| flush(): void; | Push all events and user information to the server. | function | no       | iOS,Android | yes               |


#### People

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set(prop: string, to: MixpanelType): void; | Set a user's property. | function | no | iOS,Android | yes |
| set(properties: MixpanelProperties): void; | Set a user's property. | function | no | iOS,Android | yes |
| setOnce(prop: string, to: MixpanelType): void; | Set a user's property without overwriting an existing value.| function | no | iOS,Android | yes |
| setOnce(properties: MixpanelProperties): void; | Set a user's property without overwriting an existing value.| function | no | iOS,Android | yes |
| increment(prop: string, by: number): void; | Increment the value of a numerical user property, typically used for counting or accumulating occurrences of a behavior. | function | no | iOS,Android | yes |
| increment(properties: MixpanelProperties): void; | Increment the value of a numerical user property, typically used for counting or accumulating occurrences of a behavior. | function | no | iOS,Android | yes |
| append(name: string, value: MixpanelType): void; | Add a value to a user's property, appending it to the existing value if the property already exists. | function | no | iOS,Android | yes |
| union(name: string, value: Array<MixpanelType>): void; | Add a value to a user's property, merging the newly added data with the existing value if the property already has a value. | function | no | iOS,Android | yes |
| remove(name: string, value: MixpanelType): void; | Remove a specified value from a user's property. | function | no | iOS,Android | yes |
| unset(name: string): void; | Delete a user's property and its value. | function | no | iOS,Android | yes |
| trackCharge(charge: number, properties: MixpanelProperties): void; | Track a user's transaction. | function | no | iOS,Android | yes |
| clearCharges(): void; | Permanently clear a user's historical transaction records. | function | no | iOS,Android | yes |
| deleteUser(): void; | Permanently delete a user from People analytics. | function | no | iOS,Android | yes |


#### MixpanelGroup

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| set(prop: string, to: MixpanelType): void; | Set a group's property. | function | no | iOS,Android | no |
| setOnce(prop: string, to: MixpanelType): void; | Set a group's property without overwriting an existing value. | function | no | iOS,Android | no |
| unset(prop: string): void; | Delete a group's property. | function | no | iOS,Android | no |
| remove(name: string, value: MixpanelType): void; | Remove a specified value from a group's property. | function | no | iOS,Android | no |
| union(name: string, value: MixpanelType): void; | Add a value to a group's property, merging the newly added data with the existing value | function | no | iOS,Android | no |


## Known Issues
- [ ] Some interfaces have not been developed yet: [issue#5](https://github.com/react-native-oh-library/mixpanel-react-native/issues/5)

## Others

## License

This project is licensed under [Apache License2.0](https://github.com/mixpanel/mixpanel-react-native/blob/master/LICENSE.md).

