> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-ssl-pinning</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/MaxToyberman/react-native-ssl-pinning">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://github.com/MaxToyberman/react-native-ssl-pinning/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-ssl-pinning)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-ssl-pinning Releases](https://github.com/react-native-oh-library/react-native-ssl-pinning/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-ssl-pinning@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-ssl-pinning@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

> [!TIP] 本示例依赖 react-native-file-selector 库，参照 [@react-native-oh-tpl/react-native-file-selector](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/react-native-file-selector.md) 文档进行引入。

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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

## Link

目前HarmonyOS暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的HarmonyOS工程 `harmony`


### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```
目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 2.引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-ssl-pinning": "file:../../node_modules/@react-native-oh-tpl/react-native-ssl-pinning/harmony/ssl_pinning.har"
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

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 3.在 ArkTs 侧引入 SslPinningPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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
要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-ssl-pinning Releases](https://github.com/react-native-oh-library/react-native-ssl-pinning/releases)

### 权限要求

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

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                | Description                                    | Type      | Required | Platform   | HarmonyOS Support |
|-------------------------------------|------------------------------------------------|-----------| -------- |------------|-------------------|
| removeCookieByName(cookieName)      | remove Cookies by cookieName                   | function  | No       | All        | yes               |
| getCookies(domain)                  | query cookies by domain                        | function  | No       | All        | yes               |
| fetch(hostname, options, callback)  | Initiate a fetch request with the certificate. | function  | No       | All        | yes               |


## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/MaxToyberman/react-native-ssl-pinning/blob/master/LICENSE) ，请自由地享受和参与开源。
