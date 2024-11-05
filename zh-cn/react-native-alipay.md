> 模板版本：v0.2.2

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

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-alipay/)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-alipay Releases](https://github.com/react-native-oh-library/react-native-alipay/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-alipay@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-alipay@file:#
```

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```js

import React from 'react';
import { StyleSheet, Text, View, Button, } from 'react-native';
import Alipay from "react-native-alipay";
import { AFAuthServiceResponse, } from '@alipay/afservicesdk';

function App(): React.JSX.Element {
    const urlStr: string = 'https://authweb.alipay.com/auth?auth_type=PURE_OAUTH_SDK&app_id=2016051801417322&scope=auth_user&state=init';
    const bundleName: string = "com.example.harmony"; // 包名
    const moduleName: string = "entry";
    const abilityName: string = "EntryAbility";
    
    return (
        <View style={styles.container}>
            <Text style={styles.welcome}>
                ☆Alipay Example☆
            </Text>

            <Button
                title="支付宝支付"
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
                title="登录验证"
                color="#841584"
                accessibilityLabel="Learn more about this purple button"
                onPress={async () => {
                    Alipay.setAlipayScheme('scheme:demo');
                    await Alipay.authInfo(urlStr, true, bundleName, moduleName, abilityName, (response: AFAuthServiceResponse) => {
                        //授权返回值
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

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json5` 添加 overrides 字段

```json
{
  ...
  "overrides": {
    "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-alipay": "file:../../node_modules/@react-native-oh-tpl/react-native-alipay/harmony/alipay.har"
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


### 在 ArkTs 侧引入 RNAlipayPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

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

### 支付宝登录其他配置

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@alipay/afservicesdk": "file:../../node_modules/@react-native-oh-tpl/react-native-alipay/harmony/alipay/libs/AFServiceSDK.har",
  }
```

增加协议，打开`entry/src/main/module.json5`，增加 querySchemes

```
{
  "module": {
    // 新增
    "querySchemes": [
      "apmqpdispatch"
    ],
  }
}
```

回调处理,打开`entry\src\main\ets\entryability\EntryAbility.ets`，增加onNewWant回调结果处理

```diff
+ import { AbilityConstant, Want } from '@kit.AbilityKit';
+ import { AFServiceCenter } from '@alipay/afservicesdk/Index'

  onNewWant(want: Want, launchParam: AbilityConstant.LaunchParam): void {
+    let r = AFServiceCenter.handleResponse(want);
  }
```

### 运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[react-native-alipay Releases](https://github.com/react-native-oh-library/react-native-alipay/releases)

## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
|  alipay  | 支付宝支付  | function  | no | Android/IOS | yes |
|  authInfo  | 登录验证  | function  | no | Android/IOS | yes |
|  setAlipayScheme  | scheme  | function  | no | IOS | yes |
|  getVersion  | 获取SDK版本  | function  | no | Android/IOS | no |

## 遗留问题
- [ ]  获取SDK版本号，支付宝鸿蒙sdk里面未实现鸿蒙化[issue#3](https://github.com/react-native-oh-library/react-native-alipay/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/uiwjs/react-native-alipay/blob/master/LICENSE) ，请自由地享受和参与开源。
