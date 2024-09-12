> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-apple-authentication</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/invertase/react-native-apple-authentication">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE">
        <img src="https://img.shields.io/badge/license-Apache%202.0-green.svg" alt="License" />
    </a>
</p>







> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-apple-authentication)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-apple-authentication Releases](https://github.com/react-native-oh-library/react-native-apple-authentication/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-apple-authentication@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-apple-authentication@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx
import React from 'react';
import { appleAuthHarmony, AppleButton } from '@invertase/react-native-apple-authentication';

const AppleAuthenticationDemo: React.FC = (): JSX.Element => {
    return (
        <>
            <AppleButton
                onPress={async () => {
                    appleAuthHarmony.configure({
                        // 以下配置请参考原库AppleId登录文档:
                        // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/INITIAL_SETUP.md
                        // https://github.com/invertase/react-native-apple-authentication/blob/main/docs/ANDROID_EXTRA.md
                        clientId: 'com.example.client', 
                        redirectUri: 'https://example.com'
                    })
                    const singInRes = await appleAuthHarmony.signIn()
                    console.log(singInRes)
                }}
            />
        </>
    )
}

export default AppleAuthenticationDemo;
```

## 使用 Codegen 
本库已经适配了 Codegen ，在使用前需要主动执行生成三方库桥接代码，详细请参考 [Codegen 文档](/zh-cn/codegen.md)。

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
    "@react-native-oh-tpl/react-native-apple-authentication": "file:../../node_modules/@react-native-oh-tpl/react-native-apple-authentication/harmony/react-native-apple-authentication.har"
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


### 3.在 ArkTs 侧引入 RNAppleAuthPackage

打开 `entry/src/main/ets/RNPackagesFactory.ets`，添加：

```diff
  ...
+ import { RNAppleAuthPackage } from '@react-native-oh-tpl/react-native-apple-authentication';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNAppleAuthPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-apple-authentication Releases](https://github.com/react-native-oh-library/react-native-apple-authentication/releases)。

## 属性

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**AppleButton**：Apple身份验证按钮组件。

| Name         | Description        | Type                                                         | Required | Platform | HarmonyOS Support |
| ------------ | ------------------ | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| style        | 按钮样式           | StyleProp< [ViewStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Fview%23props) > | no       | all      | yes               |
| textStyle    | 按钮内文字样式     | StyleProp< [TextStyle](https://gitee.com/link?target=https%3A%2F%2Freactnative.dev%2Fdocs%2Ftext%23props) > | no       | all      | yes               |
| cornerRadius | 按钮边框圆角弧度   | number                                                       | no       | all      | yes               |
| buttonStyle  | 按钮样式(预设枚举) | [AppleButtonStyle](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonStyle.md) | no       | all      | yes               |
| buttonType   | 按钮类型(预设枚举) | [AppleButtonType](https://gitee.com/link?target=https%3A%2F%2Fgithub.com%2Finvertase%2Freact-native-apple-authentication%2Fblob%2Fmain%2Ftypedocs%2Fenums%2FAppleButtonType.md) | no       | all      | yes               |
| onPress      | 按钮点击事件       | () => void                                                   | yes      | all      | yes               |
| leftView     | 按钮内左侧图标     | ReactNode                                                    | no       | all      | yes               |
| buttonText   | 按钮内文字内容     | string                                                       | no       | all      | yes               |

## API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

**appleAuthHarmony**：Apple身份验证对象，包含2个方法。

| Name      | Description                                             | Type                                                         | Required | Platform | HarmonyOS Support |
| --------- | ------------------------------------------------------- | ------------------------------------------------------------ | -------- | -------- | ----------------- |
| configure | 配置 Apple 身份验证的信息，此接口必须在 signIn 之前调用 | ([Config](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidConfig.md)) => void | no       | all      | yes               |
| signIn    | 弹出 webview 以进行 Apple 身份验证                      | () => Promise< [SigninResponse](https://github.com/invertase/react-native-apple-authentication/blob/main/typedocs/interfaces/AndroidSigninResponse.md) > | no       | all      | no                |

## 其他

## 遗留问题

- [ ] 由于 Apple 开发者账户验证问题，HarmonyOS暂无法实现的接口：[issue#1](https://github.com/react-native-oh-library/react-native-apple-authentication/issues/1)


## 开源协议

本项目基于 [Apache License 2.0](https://github.com/invertase/react-native-apple-authentication/blob/main/LICENSE) ，请自由地享受和参与开源。