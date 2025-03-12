> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-user-agent</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/bebnev/react-native-user-agent">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/bebnev/react-native-user-agent/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>


> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-user-agent)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-user-agent Releases](https://github.com/react-native-oh-library/react-native-user-agent/releases).

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-user-agent
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-user-agent
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React, { useState, useEffect } from 'react';
import { View, Text } from 'react-native';
import UserAgent from 'react-native-user-agent';

// sync method:
let userAgent: string = UserAgent.getUserAgent();

export default function UserAgentExample() {
  const [webViewUserAgent, setWebViewUserAgent] = useState<string | null>(null);
  useEffect(() => {
    // async method:
    UserAgent.getWebViewUserAgent()
      .then(webViewUserAgent => {
        setWebViewUserAgent(webViewUserAgent);
        console.log(webViewUserAgent);
      })
      .catch(e => {
        console.error('Error getting WebView User Agent:', e);
      });
  }, []);
  return (
    <View>
      <Text>Sync method:</Text>
      <Text>{userAgent}</Text>

      <Text>Async method</Text>
      <Text>{webViewUserAgent}</Text>

      <Text>Property: </Text>
      <Text>systemName: {UserAgent.systemName}</Text>
      <Text>systemVersion: {UserAgent.systemVersion}</Text>
      <Text>applicationName: {UserAgent.applicationName}</Text>
      <Text>applicationVersion: {UserAgent.applicationVersion}</Text>
      <Text>buildNumber: {UserAgent.buildNumber}</Text>
    </View>
  );
};

```

## Use Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

### 1.Adding the overrides Field to oh-package.json5 File in the Root Directory of the Project

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony": "./react_native_openharmony"
  }
}
```

### 2.Introducing Native Code

Currently, two methods are available:

1.  (recommended): Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-user-agent": "file:../../node_modules/@react-native-oh-tpl/react-native-user-agent/harmony/user_agent.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code](/en/link-source-code.md).

### 3.Introducing RNUserAgentPackage Package  to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
  
+  import { RNUserAgentPackage } from '@react-native-oh-tpl/react-native-user-agent/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new RNUserAgentPackage(ctx)
  ];
}
```

### 4.Running

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library:   [@react-native-oh-tpl/react-native-user-agent Releases](https://github.com/react-native-oh-library/react-native-user-agent/releases)

## Properties

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name               | Description         | Type   | Required | Platform | HarmonyOS Support |
| ------------------ | ------------------- | ------ | -------- | -------- | ----------------- |
| systemName         | System Name         | string | no       | All      | yes               |
| systemVersion      | System Version      | string | no       | All      | yes               |
| applicationName    | Application Name    | string | no       | All      | yes               |
| applicationVersion | Application Version | string | no       | All      | yes               |
| buildNumber        | Build Number        | string | no       | All      | yes               |
| darwinVersion      | Darwin Version      | string | no       | iOS      | no                |
| cfnetworkVersion   | Cfnetwork Version   | string | no       | iOS      | no                |
| modelName          | Model Name          | string | no       | iOS      | no                |
| deviceName         | Device Name         | string | no       | iOS      | no                |

## API

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                   | Type    | Required | Platform | HarmonyOS Support |
| ------------------- | ----------------------------- | ------- | -------- | -------- | ----------------- |
| getUserAgent        | Get user agent synchronously  | string  | no       | All      | yes               |
| getWebViewUserAgent | Get user agent asynchronously | Promise | no       | All      | yes               |

## Known Issues

## Others

Depending on HarmonyOS NEXT Developer Beta3 version default UserAgent definition, word ArkWeb VersionCode (ArkWeb version number) has no receive method currently, waiting for completion afterwards.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/bebnev/react-native-user-agent/blob/master/LICENSE).
