> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-http-bridge)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-oh-tpl/react-native-http-bridge Releases](https://github.com/react-native-oh-library/react-native-http-bridge/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



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

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

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

## Use Codegen

If this repository has been adapted to `Codegen`, generate the bridge code of the third-party library by using the `Codegen`. For details, see [Codegen Usage Guide](/en/codegen.md).

## Link

The HarmonyOS implementation of this library depends on the native code from @ohos/polka. If this library is included into your HarmonyOS application, there is no need to include it again; you can skip the steps in this section and use it directly. 

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
    "@react-native-oh-tpl/react-native-http-bridge": "file:../../node_modules/@react-native-oh-tpl/react-native-http-bridge/harmony/http_bridge.har"
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

### 3. Introducing RNHttpBridgePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-http-bridge Releases](https://github.com/react-native-oh-library/react-native-http-bridge/releases)

###  Permission Requirements

#### Include applicable permissions in the module.json5 file within the entry directory.

Open  `entry/src/main/module.json5` and add the following code:

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

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## Known Issues

## Others

## License

This project is licensed under[The MIT License(MIT)](https://www.mit-license.org/).

