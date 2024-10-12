> Template version: v0.2.2

<p align="center">
  <h1 align="center">react-native-ssl-pinning</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/MaxToyberman/react-native-ssl-pinning">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/MaxToyberman/react-native-ssl-pinning/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-ssl-pinning)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-safe-ssl-pinning Releases](https://github.com//releases).

Go to the project directory and execute the following instruction:

[!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-spring-scrollview@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-spring-scrollview@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

> [!TIP] This example relies on react-native-file-selector and is introduced by referring to document [@react-native-oh-tpl/react-native-file-selector](https://gitee.com/react-native-oh-library/usage-docs/blob/master/en/react-native-file-selector.md).

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
} from 'react-native';
import {Colors} from 'react-native/Libraries/NewAppScreen';
import {getCookies, fetch, removeCookieByName} from 'react-native-ssl-pinning';
import FileSelector from '@react-native-oh-tpl/react-native-file-selector';
function SslPingDemo() : React.JSX.Element{
    return (
        <>
        <StatusBar barStyle="dark-content" />
            <SafeAreaView>
                <ScrollView contentInsetAdjustmentBehavior="automatic" style={styles.scrollView}>
                    <View style={styles.body}>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>fetch bY Public Key</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={() => {
                                        fetch("https://jsnjlq.cn", {
                                            method: "GET" ,
                                            timeoutInterval: 10000, // milliseconds
                                            pkPinning: true,
                                            sslPinning: {
                                                certs: ["sha256/kPwnudZVhc+iC/fTd3OPph8uugk1YN5ZsJDAeM2P4UU="]
                                            },
                                            headers: {
                                                Accept: "application/json; charset=utf-8", "Access-Control-Allow-Origin": "*", "e_platform": "mobile",
                                            }
                                        }).then(
                                            (result) => {
                                                Alert.alert(JSON.stringify(result));
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>fetch bY Certificate</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={() => {
                                        fetch("https://jsnjlq.cn", {
                                            method: "POST" ,
                                            timeoutInterval: 10000, // milliseconds
                                            sslPinning: {
                                                certs: ["cert"]
                                            },
                                            headers: {
                                                Accept: "application/json; charset=utf-8", "Access-Control-Allow-Origin": "*", "e_platform": "mobile",
                                            }
                                        }).then(response => {
                                            Alert.alert(JSON.stringify(response));
                                        }).catch(err => {
                                            console.log(`error: ${err}`)
                                        })
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <FileSelector
                                onDone={(path: string[]) => {
                                    filePath = path
                                }}
                                onCancel={() => {console.log("cancelled");}}
                            />
                            <Text style={styles.sectionTitle} >Multipart request</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={() => {
                                        let formData = new FormData()
                                        formData.append('username', 'Chris');
                                        let filePathArray = filePath.length > 0 ?filePath[0].split("/") : ["test"]
                                        Alert.alert(JSON.stringify(filePathArray[filePathArray.length - 1]));
                                        formData.append('file', {
                                            name: encodeURIComponent(filePathArray[filePathArray.length - 1]),
                                            fileName: encodeURIComponent(filePathArray[filePathArray.length - 1]),
                                            type: "multipart/form-data",
                                            uri: filePath[0]
                                        })
                                        fetch("http://123.249.28.4:8888/handerOkhttpRequest/parse", {
                                            method: "POST" ,
                                            timeoutInterval: 10000, // milliseconds
                                            body: {
                                                formData: formData,
                                            },
                                            sslPinning: {
                                                certs: ["cert"]
                                            },
                                            headers: {
                                                accept: 'application/json, text/plain, /',
                                            }
                                        })
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>getCookies</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={async () => {
                                        getCookies("jsnjlq.cn").then(
                                            (result) => {
                                                Alert.alert(JSON.stringify(result));
                                            },
                                        );
                                    }}
                                />
                            </Text>
                        </View>
                        <View style={styles.sectionContainer}>
                            <Text style={styles.sectionTitle}>remove Cookie</Text>
                            <Text style={styles.sectionDescription}>
                                <Button
                                    title="fetch"
                                    onPress={async () => {
                                        removeCookieByName("jsnjlq.cn").then(
                                            (result) => {
                                                Alert.alert(JSON.stringify(result));
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

export default SslPingDemo;
```

## Use Codegen

If this repository has been adapted to Codegen, generate the bridge code of the third-party library by using the Codegen. For details, see Codegen Usage Guide.

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

### 2.Introducing Native Code

Currently, two methods are available:

1. Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the harmony directory in the installation path of the third-party library.

Open entry/oh-package.json5 file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-ssl-pinning": "file:../../node_modules/@react-native-oh-tpl/react-native-ssl-pinning/harmony/ssl_pinning.har"
  }
```

Click the sync button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Method 2: Directly link to the source code.

> [!TIP] For details, see [Directly Linking Source Code.](/zh-cn/link-source-code.md)

### 3.Introducing SslPinningPackage Package to ArkTS

Open the entry/src/main/ets/RNPackagesFactory.ts file and add the following code:

```diff
  ...
+ import { SslPinningPackage } from "@react-native-oh-tpl/react-native-ssl-pinning/ts"

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new SslPinningPackage(ctx),,
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

Check the release version information in the release address of the third-party library:：[@react-native-oh-tpl/react-native-ssl-pinning Releases](https://github.com/react-native-oh-library/react-native-ssl-pinning/releases)

### Permission Requirements

#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.INTERNET",
+  }
]
```

## APIs

> [!tip] The Platform column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of HarmonyOS Support is yes, it means that the HarmonyOS platform supports this property; no means the opposite; partially means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                | Description                                    | Type      | Required | Platform   | HarmonyOS Support                     |
|-------------------------------------|------------------------------------------------|-----------| -------- |------------|---------------------------------------|
| removeCookieByName(cookieName)      | remove Cookies by cookieName                   | function  | No       | All        | yes                                   |
| getCookies(domain)                  | query cookies by domain                        | function  | No       | All        | yes                                   |
| fetch(hostname, options, callback)  | Initiate a fetch request with the certificate. | function  | No       | All        | 1:目前只支持key-value格式 2：文件格式存在bug，还在解决   |


## Known Issues
- [ ] fetch interface, file upload is not supported at present. [issue#1](https://github.com/react-native-oh-library/react-native-ssl-pinning/issues/4)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/MaxToyberman/react-native-ssl-pinning/blob/master/LICENSE)
