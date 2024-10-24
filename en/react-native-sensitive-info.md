Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-sensitive-info</code> </h1>
</p>

<p align="center">
    <a href="https://github.com/mCodex/react-native-sensitive-info">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/mCodex/react-native-sensitive-info/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-sensitive-info)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-sensitive-info Releases](https://github.com/react-native-oh-library/react-native-sensitive-info/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-sensitive-info@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-sensitive-info@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useCallback, useState } from "react";
import { Alert, Button, SafeAreaView, Text } from "react-native";
import SInfo from "react-native-sensitive-info";

const SensitiveInfoDemo = () => {
  const handleAddUsingSetItemOnPress = useCallback(() => {
    SInfo.setItem("key1", "value1", {
      sharedPreferencesName: "exampleApp",
      keychainService: "exampleApp",
    }).catch((err) => {
      Alert.alert("Error", err);
    });
  }, []);

  const handleReadingDataWithoutFingerprint = useCallback(async () => {
    try {
      const data = await SInfo.getItem("key1", {
        sharedPreferencesName: "exampleApp",
        keychainService: "exampleApp",
      });
      Alert.alert("Data stored:", data);
    } catch (err) {
      Alert.alert("Error", String(err));
    }
  }, []);

  const [logText, setLogText] = useState("");
  async function runTest() {
    const options = {
      sharedPreferencesName: "exampleAppTest",
      keychainService: "exampleAppTest",
    };
    let dbgText = "";
    dbgText += `setItem(key1, value1): ${await SInfo.setItem(
      "key1",
      "value1",
      options
    )}\n`;
    dbgText += `setItem(key2, value2): ${await SInfo.setItem(
      "key2",
      "value2",
      options
    )}\n`;
    dbgText += `setItem(key3, value3): ${await SInfo.setItem(
      "key3",
      "value3",
      options
    )}\n`;
    dbgText += `getItem(key2): ${await SInfo.getItem("key2", options)}\n`;
    dbgText += `delItem(key2): ${await SInfo.deleteItem("key2", options)}\n`;
    dbgText += `getAllItems():\n`;
    const allItems = await SInfo.getAllItems(options);
    for (const key in allItems) {
      dbgText += ` - ${key} : ${allItems[key]}\n`;
    }
    setLogText(dbgText);
  }
  runTest();

  return (
    <SafeAreaView style={{ margin: 10 }}>
      <Button
        title="Add item using setItem"
        onPress={handleAddUsingSetItemOnPress}
      />
      <Button
        title="Read data without fingerprint"
        onPress={handleReadingDataWithoutFingerprint}
      />
      <Text>{logText}</Text>
    </SafeAreaView>
  );
};
export default SensitiveInfoDemo;
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
    "@react-native-oh-tpl/react-native-sensitive-info": "file:../../node_modules/@react-native-oh-tpl/react-native-sensitive-info/harmony/react_native_sensitive_info.har"
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

### 3. Introducing RNSensitiveInfoPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
...

+ import { RNSensitiveInfoPackage } from '@react-native-oh-tpl/react-native-sensitive-info/ts';

@Builder
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNSensitiveInfoPackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-sensitive-info Releases](https://github.com/react-native-oh-library/react-native-sensitive-info/releases)

### Permission Requirements

在 YourProject/entry/src/main/module.json5 补上配置

```js
"requestPermissions": [ { "name": "ohos.permission.ACCESS_BIOMETRIC" }, ]
```

## API

[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                  | Description                                                                                | Type     | Required | Platform     | HarmonyOS Support |
| ------------------------------------- | ------------------------------------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| isSensorAvailable()                   | Indicates the overall availability of fingerprint sensor. It will resolve to true or false | function | no       | Android、iOS | yes               |
| cancelFingerprintAuth ()              | Canceling fingerprint authentication                                                       | function | no       | Android、iOS | yes               |
| hasEnrolledFingerprints ()            | It will return true if detected otherwise returns false                                    | function | no       | Android、iOS | yes               |
| setItem()                             | Insert new data into the storage.                                                          | function | yes      | Android、iOS | yes               |
| getItem()                             | Get an item from storage                                                                   | function | yes      | Android、iOS | yes               |
| getAllItems()                         | Get all items from storage.                                                                | function | yes      | Android、iOS | yes               |
| deleteItem()                          | Delete an item from storage                                                                | function | yes      | Android、iOS | yes               |
| setInvalidatedByBiometricEnrollment() | Set invalid enrollment by biometrics                                                       | function | yes      | Android      | yes               |

#### **Options**

[!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

[!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.
| Name | Description | Type | Required | Platform | HarmonyOS Support |
| ---------------- | ------------------------------------------------------------ | -------- | -------- | ------------ | ----------------- |
| kSecAccessControl | A secure storage area provided for storing sensitive information such as passwords, keys, etc | object | no | iOS | no |
| kSecAttrAccessible | Used to enhance data security | object | no | iOS | no |
| kSecAttrSynchronizable | Set when adding or querying Keychain data items | boolean | no | iOS | no |
| keychainService | A tool provided for securely storing sensitive information | string | no | iOS | no |
| sharedPreferencesName |The name parameter used to specify the file name | string | no | Android | yes |
| touchID | Unlock devices, verify identities, and make secure payments | boolean | no | Android、iOS | no |
| showModal | display a dialog box | boolean | no | iOS | no |
| kSecUseOperationPrompt | Use constants related to authentication | string | no | iOS | no |
| kLocalizedFallbackTitle | Handling biometric authentication attributes such as Touch ID and Face ID | string | no | iOS | no |
| strings | Android stores information | object | no | Android | no |

## Known Issues

## Others

由于 iOS 用的 Keychain 系统，kSecAccessControl、 kSecAttrAccessible、 kSecAttrSynchronizable、keychainService、showModal、kSecUseOperationPrompt、kLocalizedFallbackTitle 这些 Properties 是该系统独有，strings 里面的 header、description、hint、success、notRecognized、cancel、cancelled、这些是 Android 的 Keystore 系统所需要的，所以这里的 PropertiesHarmonyOS 不能统一支持

## License

This project is licensed under [The MIT License (MIT)](https://github.com/mCodex/react-native-sensitive-info).
