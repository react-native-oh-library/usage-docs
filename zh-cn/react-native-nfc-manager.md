> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-nfc-manager</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/revtel/react-native-nfc-manager">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/revtel/react-native-nfc-manager/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-nfc-manager)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-nfc-manager Releases](https://github.com/react-native-oh-library/react-native-nfc-manager/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] #处替换为tgz包的路径

#### **npm**

```
npm install @react-native-oh-tpl/react-native-nfc-manager@file:#
```

#### **yarn**

```
yarn add @react-native-oh-tpl/react-native-nfc-manager@file:#
```

下面的代码展示了这个库的基本使用场景：

> [!TIP] 使用时 import 的库名不变。

```
import React from 'react';
import {View, Text, TouchableOpacity, StyleSheet} from 'react-native';
import NfcManager, {NfcTech} from 'react-native-nfc-manager';

// Pre-step, call this before any NFC operations
NfcManager.start();

function App() {
  async function readNdef() {
    try {
      // register for the NFC tag with NDEF in it
      await NfcManager.requestTechnology(NfcTech.Ndef);
      // the resolved tag object will contain `ndefMessage` property
      const tag = await NfcManager.getTag();
      console.warn('Tag found', tag);
    } catch (ex) {
      console.warn('Oops!', ex);
    } finally {
      // stop the nfc scanning
      NfcManager.cancelTechnologyRequest();
    }
  }

  return (
    <View style={styles.wrapper}>
      <TouchableOpacity onPress={readNdef}>
        <Text>Scan a Tag</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  wrapper: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
  },
});

export default App;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 harmony

```
在工程根目录的 oh-package.json 添加 overrides字段
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

## 配置Entry

本库主要用于操作及管理NFC Tag，提供后台读卡和前台应用优先分发两种读卡模式。后台读卡是指不需要打开应用程序，电子设备通过NFC读取标签卡片后，根据标签卡片的类型匹配到一个或多个应用程序。如果仅匹配到一个，则直接拉起应用程序的读卡页面；如果是多个则弹出应用选择器，让用户选择指定的读卡应用。前台读卡是指提前打开应用程序，并进入对应的NFC读卡页面后读卡，只会把读到的标签卡片信息分发给前台应用程序。

### 后台读卡方式的声明
**1.应用程序需要支持后台读卡时，需要在应用的属性配置文件中，声明与NFC相关的属性值。比如，在entry/src/main/module.json5文件中，声明下面属性值：**
```
{
    "module": {
        // other declared attributes.

        "abilities": [
            {
                "skills": [
                    {
                        "actions": [
                            // other declared actions,

                            // add the nfc tag action
                            "ohos.nfc.tag.action.TAG_FOUND"
                        ],
                        "uris": [
                            {
                                "type":"tag-tech/NfcA"
                            },
                            {
                                "type":"tag-tech/IsoDep"
                            }
                            // Add other technology if neccessary,
                            // such as: NfcB/NfcF/NfcV/Ndef/MifareClassic/MifareUL/NdefFormatable
                        ]
                    }
                ]
            }
        ],
        "requestPermissions": [
            {
                "name": "ohos.permission.NFC_TAG",
                "reason": "$string:app_name",
            }
        ]
    }
}
```
**2.在对相关Tag类型卡片进行读写之前，必须先获取TagInfo相关属性值，以确认设备读取到的Tag卡片支持哪些技术类型。可以将以下内容添加到EntryAbility**

```
import {RNAbility} from 'rnoh';
import Want from '@ohos.app.ability.Want';
import { RNNfcManagerModule } from '@react-native-oh-tpl/react-native-nfc-manager';
import AbilityConstant from '@ohos.app.ability.AbilityConstant';

export default class EntryAbility extends RNAbility {

  onCreate(want: Want): void {
    super.onCreate(want);
    RNNfcManagerModule.registerAbilityEvents(this.context,'onCreate',want);
  }

  onForeground(): void {
    super.onForeground();
  }

  onBackground(): void {
    super.onBackground();
  }

  onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
    super.onNewWant(want,launchParam);
    RNNfcManagerModule.registerAbilityEvents(this.context,'onNewWant',want);
  }

  getPagePath() {
    return 'pages/Index';
  }

  onDestroy(): void {
    super.onDestroy();
    RNNfcManagerModule.unRegisterAbilityEvents(this.context);
  }
}

```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入。
2. 直接链接源码。

方法一：通过 har 包引入 (推荐)

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-nfc-manager": "file:../../node_modules/@react-native-oh-tpl/react-native-nfc-manager/harmony/nfc_manager.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 在 ArkTs 侧引入 RNNfcManagerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNNfcManagerPackage } from '@react-native-oh-tpl/react-native-nfc-manager/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNNfcManagerPackage(ctx),
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```
cd entry
ohpm install
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-nfc-manager Releases](https://github.com/react-native-oh-library/react-native-nfc-manager/releases)

### 权限要求
打开 `entry/src/main/module.json5`，添加以下权限配置

```
"requestPermissions": [
    {
        "name": "ohos.permission.NFC_TAG",
        "reason": "$string:app_name",
    }
]
```

## Nfc Compatibility

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name        | Description                                                  | Type     | Required | Platform    | HarmonyOS Support |
| ----------- | ------------------------------------------------------------ | -------- | -------- | ----------- | ----------------- |
| Ndef  |   NFC A type Tag object, through which the Ndef technology type Tag can be accessed                   | Technologies | no       | iOS/Android | yes               |
| NfcA  |   NFC A type Tag object, through which the NfcA technology type Tag can be accessed                   | Technologies | no       | iOS/Android | yes               |
| IsoDep  |   NFC A type Tag object, through which the IsoDep technology type Tag can be accessed                   | Technologies | no       | iOS/Android | yes               |
| NfcF  |   NFC A type Tag object, through which the NfcF technology type Tag can be accessed                   | Technologies | no       | Android | yes               |
| NfcV  |   NFC A type Tag object, through which the NfcV technology type Tag can be accessed                   | Technologies | no       | Android | yes               |
| NfcB  |   NFC A type Tag object, through which the NfcB technology type Tag can be accessed                   | Technologies | no       | Android | yes               |
| MifareClassic  |   NFC A type Tag object, through which the MifareClassic technology type Tag can be accessed                   | Technologies | no       | Android | yes               |
| MifareUltralight  |   NFC A type Tag object, through which the MifareUltralight technology type Tag can be accessed                   | Technologies | no       | Android | yes               |
| MifareIOS  |   NFC A type Tag object, through which the MifareIOS technology type Tag can be accessed                   | Technologies | no       | iOS | no               |
| iso15693  |   NFC A type Tag object, through which the iso15693 technology type Tag can be accessed                   | Technologies | no       | iOS | no               |
| felica  |   NFC A type Tag object, through which the felica technology type Tag can be accessed                   | Technologies | no       | iOS | no               |
| NdefFormatable  |   NFC A type Tag object, through which the NdefFormatable technology type Tag can be accessed                   | Technologies | no       | Android | yes               |

## API
**common tech handler getters for both iOS / Android**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| start  | Start nfc scan       | function | NO | iOS / Android      | yes |
| isSupported  | Does the device support nfc       | function | NO | iOS / Android      | yes |
| isEnabled  | Is the nfc switch turned on       | function | NO | iOS / Android      | yes |
| registerTagEvent  | Register to monitor NFC Tag card reading events to achieve priority distribution of front-end applications. Set the supported card reading technology type through discTech, and obtain the TagInfo information of the read Tag through the Callback method.       | function | NO | iOS / Android      | yes |
| unregisterTagEvent  | Cancel monitoring of NFC Tag card reading events       | function | NO | iOS / Android      | yes |
| setEventListener  | Set up monitoring       | function | NO | iOS / Android      | yes |
| getBackgroundTag  | Start nfc in the background and obtain the Tag data object provided by the NFC service when the Tag is distributed.       | function | NO | iOS / Android      | yes |
| clearBackgroundTag  | After starting nfc in the background, clear Tag information of different technology types       | function | NO | iOS / Android      | yes |
| requestTechnology  | Start scanning       | function | NO | iOS / Android      | yes |
| cancelTechnologyRequest  | Cancel scan       | function | NO | iOS / Android      | yes |
| getTag  | Get the Tag data object provided by the NFC service when the Tag is distributed       | function | NO | iOS / Android      | yes |

**NdefHandler**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| writeNdefMessage| Write NDEF Message data object to label        | function  | NO | Android      | yes |
| getNdefMessage| Get the Message read from the tag when the NDEF tag is found        | function  | NO | iOS / Android      | yes |
| makeReadOnly| Set NDEF tag to read-only        | function  | NO | iOS / Android      | yes |
| getNdefStatus| Check if the NDEF tag can be set to read-only and get the maximum data length that can be sent to the tag        | function  | NO | iOS / Android      | yes |
| getCachedNdefMessageAndroid| Get the Tag data object provided by the NFC service when the Tag is distributed        | function  | NO | iOS / Android      | yes |

**NfcAHandler**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| transceive | Send instructions to Tag        | function  | NO | iOS / Android      | yes |

**IsoDepHandler**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| transceive | Send instructions to Tag        | function  | NO | iOS / Android      | yes |

**iOS only**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| setAlertMessage | Set a warning message for a certain session (possibly an NFC session or similar) | function  | NO | iOS      | NO |
| getBackgroundNdef | Scan NFC tag from lock screen        | function  | NO | iOS      | NO |
| invalidateSessionIOS | Initialize tag session        | function  | NO | iOS      | NO |
| invalidateSessionWithErrorIOS | Initializing the tag session may throw an exception        | function  | NO | iOS      | NO |
| sendCommandAPDUIOS | Send specific APDU commands        | function  | NO | iOS      | NO |
| restartTechnologyRequestIOS | Restart NFC session        | function  | NO | iOS      | NO |

**MifareIOS**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| sendMifareCommandIOS | Send specific MIFARE commands        | function  | NO | iOS      | NO |

**FelicaIOS**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| sendFelicaCommandIOS | Send specific Felica commands        | function  | NO | iOS      | NO |

**Iso15693**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getSystemInfo | Obtain system information of RFID tags        | function  | NO | iOS      | NO |
| readSingleBlock | Read the content stored in a block of tags        | function  | NO | iOS      | NO |
| readMultipleBlocks | Read the content stored in multiple blocks of the tag        | function  | NO | iOS      | NO |
| writeSingleBlock | Write content to a block in the tag storage        | function  | NO | iOS      | NO |
| lockBlock | Lock specific data blocks on tags        | function  | NO | iOS      | NO |
| writeAFI | Write the specified AFI value into the RFID tag        | function  | NO | iOS      | NO |
| lockAFI | Used to lock the AFI field in RFID tags to prevent it from being altered        | function  | NO | iOS      | NO |
| writeDSFID | Write the specified DSFID value into the RFID tag        | function  | NO | iOS      | NO |
| lockDSFID | Used to lock the AFI field in DSFID tags to prevent it from being altered         | function  | NO | iOS      | NO |
| resetToReady | Reset the RFID tag from the current state to the ready state, ready to receive new commands         | function  | NO | iOS      | NO |
| select | Place specific RFID tags in the selected state  | function  | NO | iOS      | NO |
| stayQuite | Put the tag into a quiet state, in which the tag will not respond to any requests with inventory_flag, but will respond to requests with addressing flags  | function  | NO | iOS      | NO |
| customCommand | Send custom binary data to RFID tags  | function  | NO | iOS      | NO |
| sendRequest | Send one or more commands or data requests to RFID tags  | function  | NO | iOS      | NO |
| extendedReadSingleBlock | Read the content of a specified single data block from an RFID tag  | function  | NO | iOS      | NO |
| extendedWriteSingleBlock | Write the content of a specified single data block from an RFID tag  | function  | NO | iOS      | NO |
| extendedLockBlock | Lock one or more data blocks in the RFID tag to prevent them from being further written or modified  | function  | NO | iOS      | NO |

**Android only**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| goToNfcSetting | Guide users to the NFC settings interface of the device        | function  | NO | Android      | yes |
| getLaunchTagEvent | Retrieve events or data when an application is launched (or reactivated) due to NFC tag scanning        | function  | NO | Android      | yes |
| transceive | Send instructions to Tag         | function  | NO | Android      | yes |
| getMaxTransceiveLength | Query the maximum data length that can be sent to a label         | function  | NO | Android      | yes |
| setTimeout | Set the timeout for sending data to Tag         | function  | NO | Android      | yes |
| connect | Establish a connection with the tag         | function  | NO | Android      | yes |
| close | Close tag connection        | function  | NO | Android      | yes |

**NfcVHandler**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| transceive | Send instructions to Tag        | function  | NO | Android      | yes |

**MifareClassicHandlerAndroid**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| mifareClassicSectorToBlock | Obtain the sequence number of the first block in a specific sector        | function  | NO | Android      | yes |
| mifareClassicReadBlock | Read the content stored in a block of tags, with a block size of 16 bytes        | function  | NO | Android      | yes |
| mifareClassicWriteBlock | Write content to a block in the tag, with a block size of 16 bytes        | function  | NO | Android      | yes |
| mifareClassicIncrementBlock | Add the specified value to the content of the specified block and store the result in the internal transmission buffer   | function  | NO | Android      | yes |
| mifareClassicDecrementBlock | Reduce the specified value for the content of the specified block and store the result in an internal transfer buffer    | function  | NO | Android      | yes |
| mifareClassicTransferBlock | Transfer the value of the temporary register to the specified block   | function  | NO | Android      | yes |
| mifareClassicGetSectorCount | Get the number of sectors in the MIFARE Classic tag   | function  | NO | Android      | yes |
| mifareClassicAuthenticateA | Use a key to authenticate sectors, only sectors that have been successfully authenticated can perform operations, and the key type is A   | function  | NO | Android      | yes |
| mifareClassicAuthenticateB | Use a key to authenticate sectors, only sectors that have been successfully authenticated can perform operations, and the key type is B   | function  | NO | Android      | yes |

**MifareUltralightHandlerAndroid**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| mifareUltralightReadPages | Read 4 pages of data from the tag, totaling 16 bytes of data. Each page has a data size of 4 bytes    | function  | NO | Android      | yes |
| mifareUltralightWritePage | Write one page of data with a size of 4 bytes   | function  | NO | Android      | yes |

**NdefFormatableHandlerAndroid**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| formatNdef | Format tags as NDEF tags and write NDEF messages into NDEF tags   | function  | NO | Android      | yes |

## 属性
**RegisterTagEventOpts**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| alertMessage   | Specify a warning or prompt message to be displayed when an NFC tag is read         | string  | NO | iOS      | NO |
| invalidateAfterFirstRead   | NFC tags should be considered invalid after being read for the first time     | boolean  | NO | iOS      | NO |
| isReaderModeEnabled   | This option is used to indicate whether NFC's' Reader Mode 'is enabled         | boolean  | NO | Android      | yes |
| readerModeFlags   | This option allows you to specify the flag for the reader mode         | number  | NO | Android      | yes |
| readerModeDelay   | This option allows you to specify how long to delay processing an NFC tag after it is detected   | number  | NO | Android      | NO |

**NfcEvents**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| DiscoverTag   | When the NFC Manager (NfcManager) detects and successfully reads an NFC tag, this event will be triggered     | enum  | NO | iOS/Android      | yes |
| DiscoverBackgroundTag   | When the application is in the background, the NFC Manager (NfcManager) detects and successfully reads an NFC tag, triggering this event     | enum  | NO | iOS/Android      | yes |
| SessionClosed   | Trigger this event when NFC session is closed     | enum  | NO | iOS      | NO |
| StateChanged   | This event is triggered when the enabled state of NFC changes    | enum  | NO | iOS/Android      | yes |

**NfcTech**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| Ndef  |  NDEF (NFC Data Exchange Format) is a standard format used for storing and exchanging data on NFC tags  | enum | no       | iOS/Android | yes               |
| NfcA  |  NfcA stands for ISO 14443-3 Type A technology, which is a widely used NFC tag type that supports fast data transmission and high security     | enum | no       | iOS/Android | yes               |
| IsoDep  |  IsoDep represents the ISO/IEC 7816-4 standard, which defines the communication protocol between smart cards and readers     | enum | no       | iOS/Android | yes               |
| NfcF  |   NfcF stands for ISO 14443-4 Type F technology, which supports high-speed data transmission and more complex encryption functions  | enum | no       | Android | yes               |
| NfcV  |  NfcV stands for ISO 15693 technology, also known as VICC (Vicinity Integrated Circuit Card), mainly used for low-frequency NFC tags with a longer reading distance.      | enum | no       | Android | yes               |
| NfcB  |  NfcB stands for ISO 14443-3 Type B technology, similar to NfcA but with different physical characteristics and communication protocols.     | enum | no       | Android | yes               |
| MifareClassic  |  Mifare Classic is a popular NFC tag type produced by NXP Semiconductors (now renamed NXP), widely used in fields such as access control systems, bus cards, and payment applications | enum | no       | Android | yes               |
| MifareUltralight  |  Mifare Ultralight is a low-cost NFC tag in the Mifare series, suitable for applications that require fast reading and writing but do not require high security.   | enum | no       | Android | yes               |
| MifareIOS  |   NFC A type Tag object, through which the MifareIOS technology type Tag can be accessed                   | enum | no       | iOS | no               |
| iso15693  |   NFC A type Tag object, through which the iso15693 technology type Tag can be accessed                   | enum | no       | iOS | no               |
| felica  |   NFC A type Tag object, through which the felica technology type Tag can be accessed                   | enum | no       | iOS | no               |
| NdefFormatable  |  NdefFormatable represents an NFC tag that has not yet been formatted as NDEF   | enum | no       | Android | yes               |

## 返回值
**NdefStatus**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| NotSupported   | When NFC tags do not support NDEF format, this status will be returned   | enum  | NO | iOS/Android      | yes |
| ReadWrite   | When NFC tags support NDEF format and allow read and write operations, this status will be returned    | enum  | NO | iOS/Android      | yes |
| ReadOnly   | When NFC tags support NDEF format but only allow read operations, this status will be returned   | enum  | NO | iOS/Android      | yes |

**TagEvent**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| ndefMessage   | Retrieve all records from NDEF messages   | NdefRecord[]  | NO | iOS/Android      | yes |
| maxSize   | This attribute represents the maximum number of bytes that can be stored on an NFC tag  | number  | NO | iOS/Android      | yes |
| type   | The 'type' attribute may be used to identify the type or format of NFC tags   | string  | NO | iOS/Android      | yes |
| techTypes   | This is an array containing strings used to identify the technology types supported by NFC tags    | string[]  | NO | iOS/Android      | yes |
| id   | The id attribute represents the unique identifier of the NFC tag | string  | NO | iOS/Android      | yes |

**NdefRecord**
| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| id   | This is an optional byte array used as an identifier for NDEF records   | number[]  | NO | iOS/Android      | yes |
| tnf   | TNF (Type Name Format) is an enumeration or type used to indicate the interpretation of the type field   | number  | NO | iOS/Android      | yes |
| type   | This attribute can be a byte array (number []) or a string, depending on the value of the TNF field   | number[]  | NO | iOS/Android      | yes |
| payload   | Payload is the actual data portion recorded by NDEF  | number[]  | NO | iOS/Android      | yes |

## 遗留问题


## 其他
本库是一个为 React Native 开发者提供的 NFC（近场通信）管理库，它允许开发者在 React Native 应用中轻松集成 NFC 功能。这个库支持 iOS 、 Android 和HarmonyOS NEXT平台,使得开发者可以跨平台地实现 NFC 相关的功能，如读取和写入 NFC 标签、进行智能卡模拟等。因平台不同，iOS 、Android 和HarmonyOS NEXT在NFC（近场通信）技术中对标签和协议类型存在兼容性。本库的设计考虑到了Android 和HarmonyOS NEXT兼容性较高，核心功能在两个平台上都能实现，并且表现一致。该库提供了多种 NFC 技术的支持，包括但不限于 NDEF、NfcA、IsoDep 和 NfcV 等。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/react-native-oh-library/react-native-nfc-manager/blob/main/LICENSE) ，请自由地享受和参与开源。
