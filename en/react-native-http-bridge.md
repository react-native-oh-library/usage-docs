> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-http-bridge</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/alwx/react-native-http-bridge">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://www.mit-license.org/">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-http-bridge)

## 安装与使用

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-http-bridge Releases](https://github.com/react-native-oh-library/react-native-http-bridge/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-http-bridge
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-http-bridge
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx
import React, { useState ,useEffect } from "react";
import { ScrollView, Text, Button, View, StyleSheet } from 'react-native';

var httpBridge = require('react-native-http-bridge');

const HttpBridgeDemo = () => {
  const [getRequestResult, setGetRequestResult] = useState('');
  const [postRequestResult, setPostRequestResult] = useState('');
  const GetMothedExample = () => {
    fetch('http://127.0.0.1:8888/student/getStuInfo?value=GET', {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
      }
    })
  }

  const PostMothedExample = () => {
    fetch('http://127.0.0.1:8888/student/postStuInfo', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        firstParam: 'yourValue',
        secondParam: 'yourOtherValue',
      })
    })
  }
  useEffect(() => {
    httpBridge.start(8888, 'http_service', (request: any) => {
      switch (request.type) {
        case 'GET':
          setGetRequestResult('requestId: ' + request.requestId + '\ntype: ' +
            request.type + '\nurl: ' + request.url + '\npostData: ' + request.postData);
          break;
        case 'POST':
          setPostRequestResult('requestId: ' + request.requestId + '\ntype: ' +
            request.type + '\nurl: ' + request.url + '\npostData: ' + request.postData);
          break;
      }
      if (request.type === "GET" && request.url.split("/")[1] === "user") {
        httpBridge.respond(request.requestId, 200, "application/json", "{\"message\": \"OK\"}");
      } else {
        httpBridge.respond(request.requestId, 400, "application/json", "{\"message\": \"Bad Request\"}");
      }
    });
    return () => {
      httpBridge.stop();
    }
  }, []);

  return (
  	<ScrollView>
      <View>
      <Text style={styles.text}>httpBridgeExample Port : 8888</Text>
        <View>
          <Text style={styles.text}>Method：GET</Text>
          <Button
            title="GET"
            color="#9a73ef"
            onPress={GetMothedExample}
          />
          <Text style={styles.result} allowFontScaling>{getRequestResult}</Text>
        </View>

        <View>
          <Text style={styles.text}>Method：POST</Text>
          <Button
            title="POST"
            color="#9a73ef"
            onPress={PostMothedExample}
          />
          <Text style={styles.result} allowFontScaling>{postRequestResult}</Text>
        </View>
      </View>
    </ScrollView>
 )
};

const styles = StyleSheet.create({
  text: {
    fontSize: 18,
    marginBottom: 10,
    color: 'red',
  },
  result: {
    marginTop: 10,
    fontSize: 18,
    marginBottom: 10,
    color: 'white',
  }
});
export default HttpBridgeDemo;
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

本库 HarmonyOS 侧实现依赖@ohos/polka 的原生端代码，已在 HarmonyOS 工程中引入过该库，无需再次引入，可跳过本章节步骤，直接使用。

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json` 添加 overrides 字段

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-http-bridge": "file:../../node_modules/@react-native-oh-tpl/react-native-http-bridge/harmony/http_bridge.har"
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

### 3.在 ArkTs 侧引入 RNHttpBridgePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { RNHttpBridgePackage } from "@react-native-oh-tpl/react-native-http-bridge/ts";


export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+    new RNHttpBridgePackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-http-bridge Releases](https://github.com/react-native-oh-library/react-native-http-bridge/releases)

###  权限要求


#### 在 entry 目录下的module.json5中添加权限

打开 `entry/src/main/module.json5`，添加：

```diff
...
"requestPermissions": [
+  {
+    "name": "ohos.permission.KEEP_BACKGROUND_RUNNING",
+    "reason": "$string:app_name",
+    "usedScene": {
+      "abilities": [
+        "FormAbility"
+      ],
+      "when": "always"
+    }
+  },
]
```

##  API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name    | Description            | Type     | Required | Platform    | HarmonyOS Support |
| ------- | ---------------------- | -------- | -------- | ----------- | ----------------- |
| start   | Start the HTTP server  | callback | no       | Android/iOS | yes               |
| respond | Server Response Result | void     | no       | Android/iOS | yes               |
| stop    | Stop the HTTP server   | void     | no       | Android/iOS | yes               |

#### start
```js
start(port:number, serviceName:string, callback): void;
```
| Name        | Description             | Type   | Required | Platform    | HarmonyOS Support |
| ----------- | ----------------------- | ------ | -------- | ----------- | ----------------- |
| port        | HTTP Server port number | number | Yes      | iOS/Android | Yes               |
| serviceName | HTTP Server Name        | string | Yes      | iOS/Android | Yes               |

#### respond

```js
respond(requestId:string, code:number, type:string, body:string): void;
```

| Name      | Description                                    | Type   | Required | Platform    | HarmonyOS Support |
| --------- | ---------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| requestId | HTTP Server request ID                         | string | Yes      | iOS/Android | Yes               |
| code      | Code of the response from the server           | number | Yes      | iOS/Android | Yes               |
| type      | `Content-Type` in the response from the server | string | Yes      | iOS/Android | Yes               |
| body      | Body of the response from the server           | string | Yes      | iOS/Android | Yes               |

## 遗留问题

## 其他

## 开源协议

本项目基于[The MIT License(MIT)](https://www.mit-license.org/) ，请自由地享受和参与开源。

