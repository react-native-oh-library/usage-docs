> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-fingerprint-scanner</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/hieuvp/react-native-fingerprint-scanner">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
        <a href="https://www.mit-license.org">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!tip] [Github 地址](https://github.com/react-native-oh-library/react-native-fingerprint-scanner)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-fingerprint-scanner Releases](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-fingerprint-scanner
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-fingerprint-scanner
```

<!-- tabs:end -->

快速使用：

> [!WARNING] 使用时 import 的库名不变。

```js
import { View, Button } from "react-native";
import FingerprintScanner from 'react-native-fingerprint-scanner';

export default function App() {
    const handleClick = () => {
    FingerprintScanner
      .isSensorAvailable()
      .then((Biometrics) => {
      }).catch((err) => {
      });
  }
  const handleScanner = () => {
    FingerprintScanner.authenticate({title: '1111'})
      .then(() => {
      }).catch((err) => {
      });
  }
  const handleAttempt = () => {
    let eror = FingerprintScanner.onAttempt()
  }
  const handleRelease = () => {
    FingerprintScanner.release()
  }
  return (
    <View>
       <Button title="authenticate"
          onPress={() => handleScanner()}
        />
      <Button title="isSensorAvailable"
          onPress={() => handleClick()}
        />
        <Button title="onAttempt"
          onPress={() => handleAttempt()}
        />
        <Button title="release"
          onPress={() => handleRelease()}
        />
    </View>
  );
}
```

## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1.在工程根目录的 `oh-package.json5` 添加 overrides字段

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
    "@react-native-oh-tpl/react-native-fingerprint-scanner": "file:../../node_modules/@react-native-oh-tpl/react-native-fingerprint-scanner/harmony/fingerprint_scanner.har"
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

### 3.在 ArkTs 侧引入 FingerprintScannerPackage


打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...

+ import { RNFingerprintScannerPackage } from '@react-native-oh-tpl/react-native-fingerprint-scanner/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNFingerprintScannerPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-fingerprint-scanner Releases](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/releases)


### 权限要求
> [!tip] "ohos.permission.ACCESS_BIOMETRIC"权限等级为<B>system_basic</B>
在 `YourProject/entry/src/main/module.json5`补上配置

```diff
{
  "module": {
    "name": "entry",
    "type": "entry",

  ···

    "requestPermissions": [
+     { "name": "ohos.permission.ACCESS_BIOMETRIC" },
    ]
  }
}
```


## 静态方法

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name                                              | Description                                | Type     | Required | Platform | HarmonyOS Support |
| ------------------------------------------------- | ------------------------------------------ | -------- | -------- | -------- | ----------------- |
| `authenticate: (value: authenticate) => Promise<void>;`           | Starts Fingerprint authentication       | function | No       | All      | YES                |
| `isSensorAvailable: () => Promise<string>` | Checks if Fingerprint Scanner is able to be used by now.        | function | No       | All      | YES                |
| `release: () => void`   | Stops fingerprint scanner listener, releases cache of internal state in native code | function | No       | All      | YES                |
| `onAttempt: () => {message?: string}`   | when users are trying to scan their fingerprint but failed | function | No       | HarmonyOS      | YES                |

###### authenticate方法参数
| Name                           | Description                                                                               | Type             | Required | Platform | HarmonyOS Support |
| ------------------------------ | ----------------------------------------------------------------------------------------- | ---------------- | -------- | -------- | ----------------- |
| `title`                   | the title text to display in the native                                                      | string           | no      | Android      | yes               |
| `subTitle`              | the sub title text to display in the native                  | string           | no      | Android      | no               |
| `description`             | the description text to display in the native                                                                      | string             | no       | All      | no                |
| `cancelButton`                | e cancel button text to display in the native                                                             | string             | no       | Android      | no                |
| `onAttempt`               | a callback function when users are trying to scan their fingerprint but failed.                                                        | function           | no      | Android      | no               |
| `fallbackEnabled`                  | default to true, whether to display fallback button                                                              | boolean            | no      | IOS      | no               |

## 遗留问题

- [ ] Harmony的指纹认证只支持title修改，并没有subTitle，description，cancelButton，fallbackEnabled参数， [issue#8](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/issues/8) 
- [ ] authenticate的参数不支持onAttempt，authenticate的参数onAttempt为回调方法，接口type形式不支持function,所以将onAttempt方法单独抽离出来 [issue#7](https://github.com/react-native-oh-library/react-native-fingerprint-scanner/issues/7) 



## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://www.mit-license.org) ，请自由地享受和参与开源。