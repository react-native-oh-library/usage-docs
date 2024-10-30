> Template version：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-wechat-lib</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/little-snow-fox/react-native-wechat-lib">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/little-snow-fox/react-native-wechat-lib/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github address](https://github.com/react-native-oh-library/react-native-wechat-lib)

## Installation and Usage

Find the matching version information in the release address of a third-party library：[@react-native-ohos/react-native-wechat-lib Releases](https://github.com/react-native-oh-library/react-native-wechat-lib/releases)。

Go to the project directory and execute the following instruction:：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-wechat-lib
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-wechat-lib
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository：

> [!WARNING] The name of the imported repository remains unchanged.

> [tips] When using the demo below, please change the AppID to the AppID of the HarmonyOS application applied for on the [WeChat open platform](https://developers.weixin.qq.com/doc/oplatform/Mobile_App/Access_Guide/ohos.html).

```js
import * as React from 'react';

import { StyleSheet, View, Text, Button, Alert } from 'react-native';
import { getApiVersion, registerApp, openWXApp, sendAuthRequest, shareText } from 'react-native-wechat-lib';

export default function App() {
  const [versionNumber, setVersionNumber] = React.useState<string | undefined>();

  React.useEffect(() => {
    registerApp('AppID', 'universalLink').then((res) => {
      console.log("registerApp: " + res)
    });

  }, []);

  function onLogin() {
    sendAuthRequest('snsapi_userinfo', '')
      .then((response: any) => {
        Alert.alert('Login successful, code' + response.code)
      })
      .catch(error => {
        console.log(error)
        let errorCode = Number(error.code);
        if (errorCode === -2) {
          Alert.alert('Authorized login has been canceled')
        } else {
          Alert.alert('WeChat authorized login failed')
        }
      });

  }

  function onShareText() {
    shareText({
      text: 'test content.',
      scene: 0
    }).then()
  }

  return (
    <View style={styles.container}>
      <Text style={styles.title}>Call wechat SDK demo</Text>
      <Text style={styles.versionBox}>
        Version: {versionNumber}
      </Text>
      <View style={styles.buttonGroup}>
        <View style={styles.button}>
          <Button title={'Open WeChat'} onPress={() => { openWXApp().then() }} />
        </View>
        <View style={styles.button}>
          <Button title={'Authorized login'} onPress={() => { onLogin() }} />
        </View>
        <View style={styles.button}>
          <Button title={'Share Text'} onPress={() => { onShareText() }} />
        </View>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    width: '100%',
    // flex: 1,
    alignItems: 'center',
    // justifyContent: 'center',
  },
  box: {
    width: 60,
    height: 60,
    marginVertical: 20,
  },
  title: {
    marginTop: 48,
    fontSize: 24,
    color: 'rgba(0, 0, 0, 0.6)',
  },
  versionBox: {
    color: 'rgba(0, 0, 0, 0.6)'
  },
  buttonGroup: {
    width: '100%',
    padding: 6,
    marginTop: 24,
  },
  button: {
    margin: 6,

  }
});
```

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
    "@react-native-ohos/react-native-wechat-lib": "file:../../node_modules/@react-native-ohos/react-native-wechat-lib/harmony/react_native_wechat_lib.har"
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

### 3. Configuring EntryAbility

Open `entry\src\main\ets\entryability\EntryAbility.ets` and add the following code:

```diff
import {RNAbility} from '@rnoh/react-native-openharmony';
+ import { AbilityConstant, Want } from '@kit.AbilityKit';
+ import { WechatLibTurboModule } from '@react-native-ohos/react-native-wechat-lib';

export default class EntryAbility extends RNAbility {

+   onCreate(want: Want) {
+     super.onCreate(want)
+     this.handleWeChatCallIfNeed(want)
+   }

  getPagePath() {
    return 'pages/Index';
  }

+  onNewWant(want: Want, _launchParam: AbilityConstant.LaunchParam): void {
+    this.handleWeChatCallIfNeed(want)
+  }

+  private handleWeChatCallIfNeed(want: Want) {
+    WechatLibTurboModule.handleWant(want)
+  }}

```

### 4. Configuring CMakeLists and Introducing BaseReactNativeWechatLibPackage

open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
project(rnapp)
cmake_minimum_required(VERSION 3.4.1)
set(CMAKE_SKIP_BUILD_RPATH TRUE)
set(RNOH_APP_DIR "${CMAKE_CURRENT_SOURCE_DIR}")
set(NODE_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../node_modules")
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")
set(RNOH_CPP_DIR "${CMAKE_CURRENT_SOURCE_DIR}/../../../../../../react-native-harmony/harmony/cpp")
set(LOG_VERBOSITY_LEVEL 1)
set(CMAKE_ASM_FLAGS "-Wno-error=unused-command-line-argument -Qunused-arguments")
set(CMAKE_CXX_FLAGS "-fstack-protector-strong -Wl,-z,relro,-z,now,-z,noexecstack -s -fPIE -pie")
set(WITH_HITRACE_SYSTRACE 1) # for other CMakeLists.txt files to use
add_compile_definitions(WITH_HITRACE_SYSTRACE)

add_subdirectory("${RNOH_CPP_DIR}" ./rn)

# RNOH_BEGIN: manual_package_linking_1
add_subdirectory("../../../../sample_package/src/main/cpp" ./sample-package)
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-wechat-lib/src/main/cpp" ./wechat-lib)
# RNOH_END: manual_package_linking_1

file(GLOB GENERATED_CPP_FILES "./generated/*.cpp")

add_library(rnoh_app SHARED
    ${GENERATED_CPP_FILES}
    "./PackageProvider.cpp"
    "${RNOH_CPP_DIR}/RNOHAppNapiBridge.cpp"
)
target_link_libraries(rnoh_app PUBLIC rnoh)

# RNOH_BEGIN: manual_package_linking_2
target_link_libraries(rnoh_app PUBLIC rnoh_sample_package)
+ target_link_libraries(rnoh_app PUBLIC wechat_lib)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
#include "SamplePackage.h"
+ #include "BaseReactNativeWechatLibPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
        std::make_shared<SamplePackage>(ctx),
+       std::make_shared<BaseReactNativeWechatLibPackage>(ctx),
    };
}
```

### 5. Introducing WechatLibPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { WechatLibPackage } from '@react-native-ohos/react-native-wechat-lib/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new WechatLibPackage(ctx),
  ];
}
```

### 6. Running

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

Check the release version information in the release address of the third-party library：[@react-native-ohos/react-native-wechat-lib](https://github.com/react-native-oh-library/react-native-wechat-lib/releases)

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                                          | Description        | Type     | Required | Platform    | HarmonyOS Support |
| --------------------------------------------- | ------------------ | -------- | -------- | ----------- | ----------------- |
| registerApp(appid)                            | register               | Function | no       | Android/iOS | yes               |
| isWXAppInstalled()                            | Determine whether WeChat is installed | Function | no       | Android/iOS | no                |
| isWXAppSupportApi()                           | Check support       | Function | no       | Android/iOS | no                |
| getApiVersion()                               | Get API version number    | Function | no       | Android/iOS | no                |
| openWXApp()                                   | Open WeChat           | Function | no       | Android/iOS | yes               |
| sendAuthRequest([scope[, state]])             | WeChat authorized login       | Function | no       | Android/iOS | yes               |
| authByScan([scope, nonceStr, onQRGet])        | WeChat scan code to authorize login   | Function | no       | Android/iOS | yes               |
| shareText(ShareTextMetadata)                  | Share/Collect Text     | Function | no       | Android/iOS | partially         |
| shareImage(ShareImageMetadata)                | Share Image     | Function | no       | Android/iOS | partially         |
| shareLocalImage(ShareImageMetadata)           | Share LocalImage | Function | no       | Android/iOS | partially         |
| shareFile(ShareFileMetadata)                  | Share File           | Function | no       | Android/iOS | no                |
| shareMusic(ShareMusicMetadata)                | Share Music           | Function | no       | Android/iOS | no                |
| shareVideo(ShareVideoMetadata)                | Share Video           | Function | no       | Android/iOS | no                |
| shareWebpage (ShareWebpageMetadata)           | Share Webpage           | Function | no       | Android/iOS | no                |
| shareMiniProgram(ShareMiniProgramMetadata)    | Share MiniProgram         | Function | no       | Android/iOS | no                |
| launchMiniProgram (LaunchMiniProgramMetadata) | Launch MiniProgram         | Function | no       | Android/iOS | no                |
| chooseInvoice (ChooseInvoice)                 | Select invoice           | Function | no       | Android/iOS | no                |
| pay(payload)                                  | pay               | Function | no       | Android/iOS | yes               |
| subscribeMessage(SubscribeMessageMetadata)    | 
One-time subscription to messages     | Function | no       | Android/iOS | no                |

## Known Issues

## Others

- ShareText、ShareImage、ShareLocalImage: Only sharing is supported, collection is not supported, because the WeChat Open SDK currently does not support collection on the HarmonyOS platform.
- isWXAppInstalled: The reason why it is not supported is that HarmonyOS does not support obtaining the application list data installed on the device.
- isWXAppSupportApi、getApiVersion、ShareFile、ShareMusic、ShareVideo、ShareWebpage 、ShareMiniProgram、LaunchMiniProgram、ChooseInvoice、subscribeMessage. These interfaces are currently not supported by HarmonyOS WeChat Open SDK.

## License

This project is licensed under [The MIT License (MIT)](https://github.com/little-snow-fox/react-native-wechat-lib/blob/master/LICENSE).
