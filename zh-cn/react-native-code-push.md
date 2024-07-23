<!-- {% raw %} -->

> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-code-push</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/microsoft/react-native-code-push">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/microsoft/react-native-code-push/blob/master/LICENSE.md">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-code-push)

## 前期准备

### code-push-cli

1.下载[code-push-cli](https://github.com/react-native-oh-library/code-push-cli)

2.npm install -g <code-push-cli文件夹目录>

3.常用命令：

```
code-push -v
code-push login <服务器地址>
code-push app list //列出账号下面的所有app
code-push app add <apppname> harmony react-native //创建应用
code-push release <AppName> <bundle.harmony.js> "<版本号>" --description "<v1.0.0 测试更新>" -m //发包命令，加-m是强制更新, * 代表所有版本，例如：code-push release CodePush_Local ./bundle.harmony.js "*" --description "v1.0.0 测试更新"
```

### code-push-server

下载并搭建[code-push-server](https://github.com/react-native-oh-library/code-push-server) 服务

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-code-push Releases](https://github.com/react-native-oh-library/react-native-code-push/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-code-push@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-code-push@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```tsx

import React, {Component} from 'react'
import {View, Text, StyleSheet, TouchableOpacity} from 'react-native'
import CodePush from 'react-native-code-push';
class App extends Component<any,any>{
    constructor(props:any) {
        super(props);
        this.state={
            syncMessage:'',
            progress:{}
        }
    }
    componentDidMount() {
        console.log('开始检查更新')
        this.syncImmediate(); //开始检查更新
    }
    syncImmediate() {
        CodePush.sync(
            {
                updateDialog: {
                    appendReleaseDescription: true, //是否显示更新description，默认为false
                    descriptionPrefix: '更新内容：', //更新说明的前缀。 默认是” Description:
                    mandatoryContinueButtonLabel: '立即更新', //强制更新的按钮文字，默认为continue
                    mandatoryUpdateMessage: '', //- 强制更新时，更新通知. Defaults to “An update is available that must be installed.”.
                    optionalIgnoreButtonLabel: '稍后', //非强制更新时，取消按钮文字,默认是ignore
                    optionalInstallButtonLabel: '后台更新', //非强制更新时，确认文字. Defaults to “Install”
                    optionalUpdateMessage: '有新版本了，是否更新？', //非强制更新时，更新通知. Defaults to “An update is available. Would you like to install it?”.
                    title: '更新提示', //要显示的更新通知的标题. Defaults to “Update available”.
                },
            },
            this.codePushStatusDidChange.bind(this),
            this.codePushDownloadDidProgress.bind(this),
        );
    }

    codePushStatusDidChange(syncStatus:string|number) {
        switch (syncStatus) {
            case CodePush.SyncStatus.CHECKING_FOR_UPDATE:
                this.setState({syncMessage: 'Checking for update.'});
                break;
            case CodePush.SyncStatus.DOWNLOADING_PACKAGE:
                this.setState({syncMessage: 'Downloading package.',progressModalVisible:true});
                break;
            case CodePush.SyncStatus.AWAITING_USER_ACTION:
                this.setState({syncMessage: 'Awaiting user action.'});
                break;
            case CodePush.SyncStatus.INSTALLING_UPDATE:
                this.setState({syncMessage: 'Installing update.',progressModalVisible:true});
                break;
            case CodePush.SyncStatus.UP_TO_DATE:
                this.setState({syncMessage: 'App up to date.', progress: false});
                break;
            case CodePush.SyncStatus.UPDATE_IGNORED:
                this.setState({syncMessage: 'Update cancelled by user.', progress: false,});
                break;
            case CodePush.SyncStatus.UPDATE_INSTALLED:
                this.setState({syncMessage: 'Update installed and will be applied on restart.', progress: false,});
                break;
            case CodePush.SyncStatus.UNKNOWN_ERROR:
                this.setState({syncMessage: 'An unknown error occurred.', progress: false,});
                break;
        }
    }

    codePushDownloadDidProgress(progress:any) {
        this.setState({progress});
    }

    render(){
        return(
            <View style={styles.container}>
                <Text style={styles.welcome}>欢迎使用热更新--test!</Text>
                <Text>SyncStatus: { this.state.syncMessage}</Text>
                <Text>{this.state.progressModalVisible.toString()}</Text>
                <TouchableOpacity onPress={this.syncImmediate.bind(this)}>
                    <Text style={styles.syncButton}>Press for dialog-driven sync</Text>
                </TouchableOpacity>
            </View>
        )
    }
}

const styles = StyleSheet.create({
    container:{
        flex: 1,
        alignItems: 'center',
        backgroundColor: '#F5FCFF',
        paddingTop: 10,
    },
    welcome:{
        fontSize: 20,
        textAlign: 'center',
        margin: 10,
    },
    syncButton: {
        color: 'green',
        fontSize: 17,
    },
})

let codePushOptions = {checkFrequency: CodePush.CheckFrequency.MANUAL};


export default CodePush(codePushOptions)(App);

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

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-code-push": "file:../../node_modules/@react-native-oh-tpl/react-native-code-push/harmony/codePush.har"
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

### 在 ArkTs 侧引入 CodePushPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { CodePushPackage } from "@react-native-oh-tpl/react-native-code-push/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new CodePushPackage(ctx)
  ];
}
```

### 运行

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

修改`tester\harmony\entry\src\main\ets\pages\Index.ets`文件

```diff
...
+ import common from '@ohos.app.ability.common';
+ let context = getContext(this) as common.UIAbilityContext;
+ import BuildProfile from 'BuildProfile';
+ interface CodePushConfig{
+  Staging:String;
+  Production:String;
+  ServerUrl:String;
+  PublicKey:String;
+ }
struct Index {
  @StorageLink('RNOHCoreContext') private rnohCoreContext: RNOHCoreContext | undefined = undefined
  @State shouldShow: boolean = false
  private logger!: RNOHLogger
+ bundlePath:string = 'bundle.harmony.js'
aboutToAppear() {
     ...
+   this.setCodeConfig()
    this.shouldShow = true
    stopTracing()
  }
+ setCodeConfig(){
+    const CodePushConfig: CodePushConfig = {
+      Staging:BuildProfile.Staging,
+      Production:BuildProfile.Production,
+      ServerUrl:BuildProfile.ServerUrl,
+      PublicKey:BuildProfile.PublicKey
+    }
+    AppStorage.SetOrCreate('CodePushConfig',CodePushConfig)
+  }
build() {
   Column() {
    ...
    RNApp({
    jsBundleProvider:new TraceJSBundleProviderDecorator(
            new AnyJSBundleProvider([
              new MetroJSBundleProvider(),
              // NOTE: to load the bundle from file, place it in
              // `/data/app/el2/100/base/com.rnoh.tester/files/bundle.harmony.js`
              // on your device. The path mismatch is due to app sandboxing on HarmonyOS
+              new FileJSBundleProvider(context.filesDir + '/' + this.bundlePath),
              new FileJSBundleProvider('/data/storage/el2/base/files/bundle.harmony.js'),
              new ResourceJSBundleProvider(this.rnohCoreContext.uiAbilityContext.resourceManager, 'hermes_bundle.hbc'),
              new ResourceJSBundleProvider(this.rnohCoreContext.uiAbilityContext.resourceManager, 'bundle.harmony.js')
            ]),
            this.rnohCoreContext.logger),
    })

   }

}
```

打开`tester/harmony/entry/build-profile.json5`，添加配置

```diff
{
  "apiType": 'stageMode',
  "buildOption": {
    "externalNativeOptions": {
      "path": "./src/main/cpp/CMakeLists.txt",
      "arguments": "",
      "cppFlags": "-s",
    },
+    "arkOptions": {
+      "buildProfileFields": {
+        "Staging": "", //测试环境Key
+        "Production": "",//生产环境Key
+        "ServerUrl": "",//服务端地址
+        "PublicKey": "PublicKey"
      }
    }
  },
  "targets": [
    {
      "name": "default",
      "runtimeOS": "HarmonyOS"
    },
    {
      "name": "ohosTest",
    }
  ]
}
```

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-code-push Releases](https://github.com/react-native-oh-library/react-native-code-push/releases)

## API

| Name              | Description                                                                                                                  | Type     | Required | Platform                                | HarmonyOS Support |
| ----------------- | ---------------------------------------------------------------------------------------------------------------------------- | -------- | -------- | --------------------------------------- | ----------------- |
| sync              | sync方法，自动模式更新                                                                                                                | function | yes      | Android IOS | yes               |
| getUpdateMetadata | 获取当前已安装更新的元数据(RemotePackage),当使用sync方法时，不需要调用本方法，因为sync会自动调用                                                                 | function | no       | Android iOS                             | yes               |
| DownloadProgress  | 下载中的进度回调，当使用sync方法时，不需要调用本方法，因为sync会自动调用                                                                                     | function | no       | Android iOS                             | yes               |
| restartApp        | 重启App，当使用sync方法时，不需要调用本方法，因为sync会自动调用                                                                                        | function | no       | Android iOS                             | yes               |
| getCurrentPackage | 获取应用版本信息，当使用sync方法时，不需要调用本方法，因为sync会自动调用                                                                                     | function | no       | Android iOS                             | yes               |
| getConfiguration  | 获取应用配置信息，appVersion（版本号），deploymentKey（deploymentKey），serverUrl（服务器地址），clientUniqueId（唯一标识码）,当使用sync方法时，不需要调用本方法，因为sync会自动调用 | function | no       | Android iOS                             | yes               |

**updateDialog**

当使用**CodePush.updateDialog**方法时，updateDialog以下参数都是可选的，代表更新的对话框，默认是null, 

| Name                         | Description                                                                      | Type    | Required | Platform    | HarmonyOS Support |
| ---------------------------- | -------------------------------------------------------------------------------- | ------- | -------- | ----------- | ----------------- |
| appendReleaseDescription     | 是否显示更新description，默认为false                                                       | boolean | no       | Android iOS | yes               |
| descriptionPrefix            | 更新说明的前缀。 默认是” Description:                                                       | string  | no       | Android iOS | yes               |
| mandatoryContinueButtonLabel | 强制更新的按钮文字，默认为continue                                                            | string  | no       | Android iOS | yes               |
| mandatoryUpdateMessage       | 强制更新时，更新通知. Defaults to “An update is available that must be installed.”         | string  | no       | Android iOS | yes               |
| optionalIgnoreButtonLabel    | updateDialog非强制更新时，取消按钮文字,默认是ignore                                              | string  | no       | Android iOS | yes               |
| optionalInstallButtonLabel   | 非强制更新时，确认文字. Defaults to “Install”                                               | string  | no       | Android iOS | yes               |
| optionalUpdateMessage        | 非强制更新时，更新通知. Defaults to “An update is available. Would you like to install it?” | string  | no       | Android iOS | yes               |
| title                        | 要显示的更新通知的标题. Defaults to “Update available”.                                     | string  | no       | Android iOS | yes               |

**SyncStatus**

当使用**CodePush.SyncStatus**时，codePushStatusDidChange回调函数中获取应用状态

| Name                 | Description                                                         | Type   | Required | Platform    | HarmonyOS Support |
| -------------------- | ------------------------------------------------------------------- | ------ | -------- | ----------- | ----------------- |
| UP_TO_DATE           | 值为0，代表应用程序已完全更新到配置的部署,                                              | number | no       | Android iOS | yes               |
| UPDATE_INSTALLED     | 值为1，已安装可用更新，并将在syncStatusChangedCallback函数返回后立即运行或在下次应用程序恢复/重新启动时运行 | number | no       | Android iOS | yes               |
| UNKNOWN_ERROR        | 值为3，同步操作发现未知错误                                                      | number | no       | Android iOS | yes               |
| CHECKING_FOR_UPDATE  | 值为5，正在查询 CodePush 服务器是否有更新                                          | number | no       | Android iOS | yes               |
| AWAITING_USER_ACTION | 值为6，有更新可用，并向最终用户显示确认对话框。（仅在updateDialog使用时适用）                       | number | no       | Android iOS | yes               |
| DOWNLOADING_PACKAGE  | 值为7，在从 CodePush 服务器下载可用更新                                           | number | no       | Android iOS | yes               |
| INSTALLING_UPDATE    | 值为8，已下载可用更新并将安装                                                     | number | no       | Android iOS | yes               |



## 遗留问题

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/microsoft/react-native-code-push/blob/master/LICENSE.md) ，请自由地享受和参与开源。

<!-- {% endraw %} -->
