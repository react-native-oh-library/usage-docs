> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-send-intent)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-send-intent Releases](https://github.com/react-native-oh-library/react-native-send-intent/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-send-intent@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-send-intent@file:#
```

<!-- tabs:end -->


下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState, useEffect } from 'react';
import {Button, Text} from 'react-native';
import NativeSendIntent from 'react-native-send-intent'

function SendIntent() {

    return (
        <>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.sendPhoneDial</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.sendPhoneDial('10086', false);
                    }}
                    title=""
                    color="#841584"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.sendSms</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.sendSms('100010', 'text SMS');
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
                        NativeSendIntent.sendMail('mailto:someone@example.com', 'This%20is%20the%20subject', 'This%20is%20the%20body');
                    }}
                    title=""
                    color="#B8860B"
                />
            </>
            <>
                <Text style={{ color: "red" }}>NativeSendIntent.openMaps</Text>
                <Button
                    onPress={() => {
                        NativeSendIntent.openMaps('武昌火车站');
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
                        NativeSendIntent.openSettings('bluetooth_entry');
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
};
export default SendIntent;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

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

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-send-intent": "file:../../node_modules/@react-native-oh-tpl/react-native-send-intent/harmony/send_intent.har"
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

### 3.在 ArkTs 侧引入 RNSendIntentPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 4.运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-send-intent Releases](https://github.com/react-native-oh-library/react-native-send-intent/releases)

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

## 遗留问题
 - [ ] react-native-send-intent部分方法未实现HarmonyOS化 [issue#2](https://github.com/react-native-oh-library/react-native-send-intent/issues/2) 

## 其他
- installRemoteApp(); 不支持通过一个链接下载一个包，进行安装，只能通过应用市场
- shareTextToLine(); 共享的应用android源码为海外应用,无法打开
- shareImageToInstagram(); Instagram为海外应用,无法打开
- getVoiceMailNumber(); ICCID和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)
- getPhoneNumber(); ICCID和号码信息为敏感数据，不开放(https://developer.huawei.com/consumer/cn/doc/harmonyos-references-V5/js-apis-sim-V5)

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/lucasferreira/react-native-send-intent?tab=readme-ov-file#license) ，请自由地享受和参与开源。
