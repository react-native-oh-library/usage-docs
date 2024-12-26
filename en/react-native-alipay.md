> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-alipay</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/uiwjs/react-native-alipay">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/uiwjs/react-native-alipay/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-alipay/)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-alipay Releases](https://github.com/react-native-oh-library/react-native-alipay/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-alipay
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-alipay
```

The following code shows the basic use scenario of the repository:

>[!WARNING] The name of the imported repository remains unchanged.

```js

import React from 'react';
import { StyleSheet, Text, View, Button, } from 'react-native';
import Alipay from "react-native-alipay";
import { AFAuthServiceResponse, } from '@alipay/afservicesdk';

function App(): React.JSX.Element {
    const urlStr: string = 'https://authweb.alipay.com/auth?auth_type=PURE_OAUTH_SDK&app_id=2016051801417322&scope=auth_user&state=init';
    const bundleName: string = "com.example.harmony"; // Bundle name
    const moduleName: string = "entry";
    const abilityName: string = "EntryAbility";
    
    return (
        <View style={styles.container}>
            <Text style={styles.welcome}>
                ☆Alipay Example☆
            </Text>

            <Button
                title="Alipay"
                color="#841584"
                accessibilityLabel="Learn more about this purple button"
                onPress={ 
                    async () => {
                        let orderInfo: string = 'app_id=2014100900013222&biz_content=%7B%22timeout_express%22%3A%2230m%22%2C%22product_code%22%3A%22QUICK_MSECURITY_PAY%22%2C%22total_amount%22%3A%220.01%22%2C%22subject%22%3A%221%22%2C%22body%22%3A%22xxx%22%2C%22out_trade_no%22%3A%22723175011179269%22%7D&charset=utf-8&method=alipay.trade.app.pay&sign_type=RSA2&timestamp=2016-07-29%2016%3A55%3A53&version=1.0&sign=ClyziyfaiJtGd01HE1XmLbr%2BGy1JzBiH7QF69Qb66GvB%2BH6ULI5BeqEHeJIxVtKKgM%2F0ILEz7XjH2bvP1Fj52VUg5Gc5sg2reVHr8EhHqY7IiSAkEt3lNckWhfeVvdhjbQEKKZWMPgVC%2FVmMvMkkFzsP5S5Zz3aZKZWRp7xLApWtBZTeJj2Hd%2FDNhbEzvpTiQF9UDs1hPMmXmKLrNUmi0k4MQaeBCxXxmY9ITTmHofsju30rxo3q%2FYMYWD79ayxFmSO6adAXP9nLY%2B16VyeBCb53zxb%2BPWjV4CCVmit8YBOIOssAN4B0yLlmBOYWJS76MM46ADu%2FmiCwkdOnJduC6Q%3D%3D';
                        Alipay.alipay(orderInfo).then((result: any) => {
                            console.info('App alipay result: ' + result);
                        });
                    }
                }
            />

            <Button
                title="Login verification"
                color="#841584"
                accessibilityLabel="Learn more about this purple button"
                onPress={async () => {
                    Alipay.setAlipayScheme('scheme:demo');
                    await Alipay.authInfo(urlStr, true, bundleName, moduleName, abilityName, (response: AFAuthServiceResponse) => {
                        // Return value of the authorization request
                        console.info('========= response=' + JSON.stringify(response));
                    });
                }}
            />
        </View>
    );
};

const styles = StyleSheet.create({
    container: {
      flex: 1,
      justifyContent: 'center',
      alignItems: 'center',
      backgroundColor: '#F5FCFF',
    },
    welcome: {
      fontSize: 20,
      textAlign: 'center',
      margin: 10,
    },
  });

export default App;

```

## Use Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see[ Codegen Usage Guide](/en/codegen.md).

## Link

Currently, HarmonyOS does not support AutoLink. Therefore, you need to manually configure the linking.

Open the harmony directory of the HarmonyOS project in DevEco Studio.

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

1. Use the HAR file.
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-alipay": "file:../../node_modules/@react-native-oh-tpl/react-native-alipay/harmony/alipay.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see[Directly Linking Source Code](/en/link-source-code.md)


### 3. Introducing RNAlipayPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
+ import {RNAlipayPackage} from '@react-native-oh-tpl/react-native-alipay/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAlipayPackage(ctx),
  ];
}
```

### 4. Alipay login others config

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@alipay/afservicesdk": "file:../../node_modules/@react-native-oh-tpl/react-native-alipay/harmony/alipay/libs/AFServiceSDK.har",
  }
```

Open the `entry/src/main/module.json5` file and add **querySchemes**.

```
{
  "module": {
    "querySchemes": [
      "apmqpdispatch"
    ],
  }
}
```

Open the `entry\src\main\ets\entryability\EntryAbility.ets` file and add **onNewWant** callback result handling:

```diff
+ import { AbilityConstant, Want } from '@kit.AbilityKit';
+ import { AFServiceCenter } from '@alipay/afservicesdk/Index'

  onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
+    let r = AFServiceCenter.handleResponse(want);
  }
```

### 5. Running

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

Check the release version information in the release address of the third-party library: [react-native-alipay Releases](https://github.com/react-native-oh-library/react-native-alipay/releases)

## Static Methods

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name            | Description     | Type     | Required | Platform    | HarmonyOS Support |
| --------------- | --------------- | -------- | -------- | ----------- | ----------------- |
| alipay          | alipay          | function | no       | Android/IOS | yes               |
| authInfo        | login verify    | function | no       | Android/IOS | yes               |
| setAlipayScheme | scheme          | function | no       | IOS         | yes               |
| getVersion      | get sdk version | function | no       | Android/IOS | no                |

## Known Issues
- [ ] Alipay SDK for HarmonyOS currently does not support obtaining the SDK version number: [issue#3](https://github.com/react-native-oh-library/react-native-alipay/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/uiwjs/react-native-alipay/blob/master/LICENSE).
