> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-send-intent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lucasferreira/react-native-send-intent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-send-intent)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-send-intent Releases](https://github.com/react-native-oh-library/react-native-send-intent/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-send-intent@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-send-intent@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```tsx
import React, { useState, useEffect } from "react";
import { Button, Text } from "react-native";
import NativeSendIntent from "react-native-send-intent";

function SendIntent() {
  return (
    <>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.sendPhoneDial</Text>
        <Button
          onPress={() => {
            NativeSendIntent.sendPhoneDial("10086", false);
          }}
          title=""
          color="#841584"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.sendSms</Text>
        <Button
          onPress={() => {
            NativeSendIntent.sendSms("100010", "text SMS");
          }}
          title=""
          color="#DC143C"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openCalendar</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openCalendar();
          }}
          title=""
          color="#D2691E"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.sendMail</Text>
        <Button
          onPress={() => {
            NativeSendIntent.sendMail(
              "mailto:someone@example.com",
              "This%20is%20the%20subject",
              "This%20is%20the%20body"
            );
          }}
          title=""
          color="#B8860B"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openMaps</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openMaps("Wuchang Railway Station");
          }}
          title=""
          color="#FF0000"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openCamera</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openCamera();
          }}
          title=""
          color="#FF1493"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.openSettings</Text>
        <Button
          onPress={() => {
            NativeSendIntent.openSettings("bluetooth_entry");
          }}
          title=""
          color="#8B4513"
        />
      </>
      <>
        <Text style={{ color: "red" }}>NativeSendIntent.gotoHomeScreen</Text>
        <Button
          onPress={() => {
            NativeSendIntent.gotoHomeScreen();
          }}
          title=""
          color="#006400"
        />
      </>
    </>
  );
}
export default SendIntent;
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
    "@react-native-oh-tpl/react-native-send-intent": "file:../../node_modules/@react-native-oh-tpl/react-native-send-intent/harmony/send_intent.har"
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

### 3. Introducing RNSendIntentPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import {RNSendIntentPackage} from '@react-native-oh-tpl/react-native-send-intent/ts';


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNSendIntentPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-send-intent Releases](https://github.com/react-native-oh-library/react-native-send-intent/releases)

## API

| Name                                   | Description                                            | Type     | Required | Platform | HarmonyOS Support |
| -------------------------------------- | ------------------------------------------------------ | -------- | -------- | -------- | ----------------- |
| sendText                               | Usage of Text (Share)                                  | Function | no       | Android  | yes               |
| sendMail                               | Usage of Send Mail (text/plain only)                   | Function | no       | Android  | yes               |
| sendSms                                | Usage of SMS                                           | Function | no       | Android  | yes               |
| sendPhoneCall                          | Usage of Phone Dial Screen                             | Function | no       | Android  | yes               |
| sendPhoneDial                          | sage of Phone Dial Screen                              | Function | no       | Android  | yes               |
| addCalendarEvent                       | Create Calendar Event                                  | Function | no       | Android  | no                |
| isAppInstalled                         | Check if an application is installed                   | Function | no       | Android  | no                |
| installRemoteApp                       | Install a remote APK                                   | Function | no       | Android  | no                |
| openApp                                | Open App                                               | Function | no       | Android  | yes               |
| openAppWithData                        | Open App with Data                                     | Function | no       | Android  | no                |
| openChromeIntent                       | browser opened                                         | Function | no       | Android  | yes               |
| openCalendar                           | Open Camera Intent                                     | Function | no       | Android  | yes               |
| openCamera                             | Open Camera                                            | Function | no       | Android  | yes               |
| openEmailApp                           | Open Email Application                                 | Function | no       | Android  | yes               |
| openAllEmailApp                        | Will open all the Email app's that available in device | Function | no       | Android  | yes               |
| openDownloadManager                    | Open Download Manager                                  | Function | no       | Android  | yes               |
| openChooserWithOptions                 | Open Share With dialog                                 | Function | no       | Android  | yes               |
| openChooserWithMultipleOptions         | Open Multiple Files Share With dialog                  | Function | no       | Android  | yes               |
| openMaps                               | Open Maps                                              | Function | no       | Android  | yes               |
| openMapsWithRoute                      | Open Maps With Route                                   | Function | no       | Android  | yes               |
| shareTextToLine                        | Share text to line                                     | Function | no       | Android  | no                |
| shareImageToInstagram                  | Share Image to Instagram                               | Function | no       | Android  | no                |
| openSettings                           | Open Settings                                          | Function | no       | Android  | yes               |
| getVoiceMailNumber                     | Get voiceMail number                                   | Function | no       | Android  | no                |
| openFileChooser                        | Open File Chooser                                      | Function | no       | Android  | yes               |
| openFilePicker                         | Opens Android own file selector callback path from     | Function | no       | Android  | yes               |
| getPhoneNumber                         | Get phone number                                       | Function | no       | Android  | no                |
| requestIgnoreBatteryOptimizations      | Request 'ignore battery optimizations'                 | Function | no       | Android  | yes               |
| showIgnoreBatteryOptimizationsSettings | Show battery optimizations settings                    | Function | no       | Android  | yes               |
| gotoHomeScreen                         | Jump to main screen                                    | Function | no       | Android  | yes               |
| openAppWithUri                         | Open the app and go to the app store                   | Function | no       | Android  | yes               |

## Known Issues

- [ ] react-native-send-intent 部分方法未实现 HarmonyOS 化 [issue#2](https://github.com/react-native-oh-library/react-native-send-intent/issues/2)

## Others

- installRemoteApp(); 不支持通过一个链接下载一个包，进行安装，只能通过应用市场
- shareTextToLine(); 共享的应用 android 源码为海外应用,无法打开
- shareImageToInstagram(); Instagram 为海外应用,无法打开
- getVoiceMailNumber(); ICCID 和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)
- getPhoneNumber(); ICCID 和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)

## License

This project is licensed under [The MIT License (MIT)](https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license).
