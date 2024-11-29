> Template version: v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-idfa-aaid</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-idfa-aaid)

## Installation and Usage

Find the matching version information in the release address of a third-party library:[@react-native-oh-library/react-native-idfa-aaid Releases](https://github.com/react-native-oh-library/react-native-idfa-aaid/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### npm

```bash
npm install @react-native-oh-tpl/react-native-idfa-aaid
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-idfa-aaid
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```
import React, { useEffect } from 'react';
import type { PropsWithChildren } from 'react';
import {
  SafeAreaView,
  ScrollView,
  StatusBar,
  StyleSheet,
  Text,
  useColorScheme,
  View,
} from 'react-native';

import {
  Colors,
  DebugInstructions,
  Header,
  LearnMoreLinks,
  ReloadInstructions,
} from 'react-native/Libraries/NewAppScreen';

import ReactNativeIdfaAaid, {
  AdvertisingInfoResponse,
} from 'react-native-idfa-aaid';

type SectionProps = PropsWithChildren<{
  title: string;
}>;

function Section({ children, title }: SectionProps): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

  useEffect(() => {
    ReactNativeIdfaAaid.getAdvertisingInfo()
      .then((res: AdvertisingInfoResponse) =>
        console.log('Advertising info', res)
      )
      .catch(err => {
        console.log(err);
      });
  }, []);

  return (
    <View style={styles.sectionContainer}>
      <Text
        style={[
          styles.sectionTitle,
          {
            color: isDarkMode ? Colors.white : Colors.black,
          },
        ]}>
        {title}
      </Text>
      <Text
        style={[
          styles.sectionDescription,
          {
            color: isDarkMode ? Colors.light : Colors.dark,
          },
        ]}>
        {children}
      </Text>
    </View>
  );
}

function App(): React.JSX.Element {
  const isDarkMode = useColorScheme() === 'dark';

  const backgroundStyle = {
    backgroundColor: isDarkMode ? Colors.darker : Colors.lighter,
  };
  return (
    <SafeAreaView style={backgroundStyle}>
      <StatusBar
        barStyle={isDarkMode ? 'light-content' : 'dark-content'}
        backgroundColor={backgroundStyle.backgroundColor}
      />
      <ScrollView
        contentInsetAdjustmentBehavior="automatic"
        style={backgroundStyle}>
        <Header />
        <View
          style={{
            backgroundColor: isDarkMode ? Colors.black : Colors.white,
          }}>
          <Section title="Step One">
            Edit <Text style={styles.highlight}>App.tsx</Text> to change this
            screen and then come back to see your edits.
          </Section>
          <Section title="See Your Changes">
            <ReloadInstructions />
          </Section>
          <Section title="Debug">
            <DebugInstructions />
          </Section>
          <Section title="Learn More">
            Read the docs to discover what to do next:
          </Section>
          <LearnMoreLinks />
        </View>
      </ScrollView>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  sectionContainer: {
    marginTop: 32,
    paddingHorizontal: 24,
  },
  sectionTitle: {
    fontSize: 24,
    fontWeight: '600',
  },
  sectionDescription: {
    marginTop: 8,
    fontSize: 18,
    fontWeight: '400',
  },
  highlight: {
    fontWeight: '700',
  },
});

export default App;
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

### 2.Introducing Native Code

Currently, two methods are available:

1. Use the HAR file(recommended)；
2. Directly link to the source code.

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-idfa-aaid": "file:../../node_modules/@react-native-oh-tpl/react-native-idfa-aaid/harmony/getOaid.har"
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


### 3. Introducing GetOaidPackage Package to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
  
+  import { GetOaidPackage } from "@react-native-oh-tpl/react-native-idfa-aaid/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new GetOaidPackage(ctx),
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
Check the release version information in the release address of the third-party library: [@react-native-oh-library/react-native-idfa-aaid Releases](https://github.com/react-native-oh-library/react-native-idfa-aaid/releases)

### Permission Requirements (If Any)

[!TIP] "ohos.permission.APP_TRACKING_CONSENT"，"ohos.permission.APP_TRACKING_CONSENT"权限等级为<B>normal</B>，授权方式为<B>user_grant</B>[使用 ACL 签名的配置指导](https://developer.harmonyos.com/cn/docs/documentation/doc-guides-V3/signing-0000001587684945-V3#section157591551175916)

#### 在 entry 目录下的module.json5中添加权限
在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

+    "requestPermissions":[
+      {
+        "name" : "ohos.permission.APP_TRACKING_CONSENT",
+        "reason": "$string:page_show",
+        "usedScene": {
+          "abilities": [
+            "FormAbility"
+          ],
+          "when":"always"
+        }
+     }
+    ]
  }
}
```
在 `YourProject/entry/src/main/resources/base/element/string.json`补上配置

#### 在 entry 目录下添加申请权限的原因

打开 `entry/src/main/resources/base/element/string.json`，添加：

```diff
...
{
  "string": [
+    {
+      "name": "page_show",
+      "value": "page from npm package"
+    }
  ]
}
```
当前版本上，向用户申请此权限时，系统不会有弹框，而是直接将该应用的获取OAID的权限置为禁止。如有需要应用可自行弹框引导用户到设置界面手动开启该权限。为避免后续系统功能变化引发兼容性问题，应用应严格按照user_grant权限的申请流程进行申请。
[详情参考](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/permissions-for-all-V5#ohospermissionapp_tracking_consent)

## Static Methods (If Any)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getAdvertisingInfo  |Check the permission, apply for the permission, and obtain the OAID.         | Function  | yes | iOS/Android      | yes |
| getAdvertisingInfoAndCheckAuthorization  | The function is the same as above, and is used to keep the porting uniform.         | Function  | no | iOS/Android      | yes |

## Known Issues

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE)