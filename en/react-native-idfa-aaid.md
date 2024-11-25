> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-idfa-aaid)

## 安装与使用

Find the matching version information in the release address of a third-party library:[@react-native-oh-library/react-native-idfa-aaid Releases](https://github.com/react-native-oh-library/react-native-idfa-aaid/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides 字段

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
    "@react-native-oh-tpl/react-native-idfa-aaid": "file:../../node_modules/@react-native-oh-tpl/react-native-idfa-aaid/harmony/getOaid.har"
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


### 3.在 ArkTs 侧引入 GetOaidPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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
请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-idfa-aaid Releases](https://github.com/react-native-oh-library/react-native-idfa-aaid/releases)

### 权限要求

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

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| getAdvertisingInfo  |Check the permission, apply for the permission, and obtain the OAID.         | Function  | yes | iOS/Android      | yes |
| getAdvertisingInfoAndCheckAuthorization  | The function is the same as above, and is used to keep the porting uniform.         | Function  | no | iOS/Android      | yes |

## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/sparkfabrik/sparkfabrik-react-native-idfa-aaid/blob/main/LICENSE) ，请自由地享受和参与开源。