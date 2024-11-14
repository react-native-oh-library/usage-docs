> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>jpush-react-native</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/jpush/jpush-react-native">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/jpush/jpush-react-native/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/jpush-react-native)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/jpush-react-native Releases](https://github.com/react-native-oh-library/jpush-react-native/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：
<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/jpush-react-native
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/jpush-react-native
```
<!-- tabs:end -->

另外还需按照[极光推送SDK-HarmonyOS集成指南](https://docs.jiguang.cn/jpush/client/HarmonyOS/hmos_guide)完成极光推送相关的配置

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { Text, View, Button } from 'react-native';
import JPush from 'jpush-react-native';

function App() {
    let localNotification = { messageID: '1', title: 'add local notification', content: '测试添加一个本地通知', broadcastTime: new Date().getTime(), extras: { content: '附加内容' } };
    return (
        <View>
                <Text style={{
                    color: "#555",
                    fontSize: 25,
                    marginTop: 100,
                    padding:20,
                    fontWeight: "500"
                }}>jpush-react-native</Text>
                <Text style={{
                    color: "#999",
                    fontSize: 15,
                    marginBottom:20,
                    padding:20,
                }}>请先前往手机"设置"-->"通知和状态栏"打开测试应用的通知</Text>
                <View>
                     <Button
                        key="addLocalNotification"
                        title="addLocalNotification"
                        onPress={async () => {
                          JPush.addLocalNotification(localNotification);
                        }}
                     />
                </View>
        </View>
    );
}
export default App;
```
## 使用 Codegen

本库已经适配了 `Codegen` ，在使用前需要主动执行生成三方库桥接代码，详细请参考[ Codegen 使用文档](https://gitee.com/react-native-oh-library/usage-docs/blob/master/zh-cn/codegen.md)。

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 1. 在工程根目录的 `oh-package.json` 添加 overrides 字段

```json
{
  ...
  "overrides": {
     "@rnoh/react-native-openharmony" : "./react_native_openharmony"
  }
}
```

### 2. 引入原生端代码

目前有两种方法：

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）；

2. 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json

"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/jpush-react-native": "file:../../node_modules/@react-native-oh-tpl/jpush-react-native/harmony/jpush_react_native.har"
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


### 3. 在 ArkTs 侧引入 RNJPushPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，由于引入的是ets文件，请将RNPackagesFactory.ts文件名后缀  ts 修改为 ets，添加：

```diff
+ import {RNJPushPackage} from  "@react-native-oh-tpl/jpush-react-native/ts";

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNJPushPackage(ctx)
  ];
}
```

### 4. 运行

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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/jpush-react-native Releases](https://github.com/react-native-oh-library/jpush-react-native/releases)

## 静态方法

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| -------------------- | ------------------- | ------ | ------ | ---------- | ----------- |
|   setLoggerEnable(enable: boolean): void  |   设置调试模式，默认关闭状态，RN侧调用不起作用，请按照[极光推送SDK-HarmonyOS集成指南](https://docs.jiguang.cn/jpush/client/HarmonyOS/hmos_guide)调用    | function   | no | iOS,Android      | yes |
|  init(params: {appKey: string;channel:string;production:string;}): void  |初始化极光推送，RN侧调用不起作用，请按照[极光推送SDK-HarmonyOS集成指南](https://docs.jiguang.cn/jpush/client/HarmonyOS/hmos_guide)文档中集成调用  |  function   | yes | iOS,Android      | yes |
|  getRegistrationID(callback: Callback<{ registerID: string }>): void  |  调用此 API 来取得应用程序对应的 RegistrationID。   | function   | no | iOS,Android      | yes |
|  addTags(params: {"sequence":number,"tags":string[]}): void  |   新增标签   |function   | no | iOS,Android      | yes |
|   updateTags(params: {"sequence":number,"tags":string[]}): void  | 覆盖标签  | function   | no | iOS,Android      |yes |
|  deleteTag(params: {"sequence":number,"tags":string[]}): void  | 删除指定标签  | function  | no | iOS,Android      |yes |
|  deleteTags(params: {"sequence":number}): void  | 清除所有标签  | function  | no | iOS,Android      |yes |
|   queryTag(params:{"sequence":number,"tag":string}): void  | 查询指定 tag 与当前用户绑定的状态  | function  | no | iOS,Android      |yes |
|  queryTags(params: {"sequence":number}): void  | 查询所有标签  | function  | no | iOS,Android      |yes |
|  setAlias(params: {"sequence":number,"alias":string}): void  | 设置别名  | function  | no | iOS,Android      |yes |
|  deleteAlias({"sequence":number}): void  | 删除别名  | function  | no | iOS,Android      |yes |
|  queryAlias(params: {"sequence":number}): void  | 查询别名  | function  | no | iOS,Android      |yes |
|   setProperties(params:{pros:any}):void; |   设置推送个性化属性/更新用户指定推送个性化属性   |function   | no | iOS,Android     | no |
|   deleteProperties(params:{pros:any}):void; |   删除指定推送个性化属性   |function   | no | iOS,Android     | no |
|  cleanProperties():void; |   清除所有推送个性化属性  |function   | no | iOS,Android     | no |
|  pageEnterTo(pageName: string): void  | 进入页面  | function  | no | iOS,Android      |no |
|  pageLeave(pageName: string): void  | 离开页面  | function  | no | iOS,Android      |no |
|  setMobileNumber(params: {"sequence":number,"mobileNumber":string}): void  | 设置手机号码。该接口会控制调用频率,频率为 10s 之内最多 3 次  | function  | no | iOS,Android      |yes |
|  initCrashHandler(): void  | 开启 CrashLog 上报  | function  | no | iOS,Android      |no |
|  setPowerSaveMode(enable: boolean):void  | Push SDK 开启和关闭省电模式，默认为关闭  | function  | no | Android      |no |
|  isNotificationEnabled(callback: Callback<boolean>): void  | 检查当前应用的通知开关是否开启  | function  | no | iOS,Android      |yes |
|  addLocalNotification(params:{messageID: stringtitle: string;content: string;extras: Extra}): void  | 添加一个本地通知  | function  | no | iOS,Android      |yes |
|   removeLocalNotification(params: { messageID: string }): void  | 移除指定的本地通知  | function  | no | iOS,Android      |yes |
|  clearLocalNotifications(): void  | 移除所有的本地通知  | function  | no | iOS,Android      |yes |
|  clearAllNotifications():void  | 清除所有 JPush 展现的通知（不包括非 JPush SDK 展现的）  | function  | no | Android      |no |
|  clearNotificationById(params: {notificationId:number}):void  | 删除指定的通知  | function  | no | iAndroid      |no |
|  setMaxGeofenceNumber(params: {geoFenceMaxNumber:number}): void  | 设置最多允许保存的地理围栏数量,超过最大限制后,如果继续创建先删除最早创建的地理围栏。 默认数量为10个,允许设置最小1个,最大100个。  | function  | no | iOS,Android      |no |
|  deleteGeofence(params: { geoFenceID: string }): void |  删除指定id的地理围栏  | function  | no | iOS,Android      |no |
|  addConnectEventListener(callback: Callback<{connectEnable: boolean }>): void  | 监听连接状态  | function  | no | iOS,Android      |yes |
|  addCommandEventListener(callback: Callback<{ cmd:number, errorCode:number,msg:string,extra:Extra}>): void  | CommandEvent 事件回调  | function  | no | iOS,Android      |yes |
|   addNotificationListener(callback: Callback <{messageID:string;title:string;content:string;extras:Extra;notificationEventType: "notificationArrived" "notificationOpened"}>):void  | 远程通知事件  | function  | no | iOS,Android      |no |
|  addLocalNotificationListener(callback: Callback <{messageID:string;title:string;content:string;extras:Extra;notificationEventType: "notificationArrived" "notificationOpened"}>  | 本地通知事件  | function  | no | iOS,Android      |yes |
|  addCustomMessageListener(callback: Callback<{messageID: string;content: string;extras: Extra;title:string}>):void  | 自定义信息通知回调  | function  | no | iOS,Android      |yes |
| addInappMessageListener(callback: Callback<{mesageId: string;title: string;content: string;target:string;clickAction: string;extras:Extra:inappEventType: "inappShow"  "inappClick"}>):void| inapp消息事件  | function  | no | iOS,Android      |no |
|  addTagAliasListener(callback: Callback<{ code: number;tagEnable: boolean;Tags:string[];alias:string;sequence:number}>): void  | tag alias事件  | function  | no | iOS,Android      |yes |
|  addMobileNumberListener(callback: Callback<{ code: number;sequence:number }>): void  | 手机号码事件  | function  | no | iOS,Android      |yes |
|  removeListener(callback: Function): void  | 移除事件  | function  | no | iOS,Android      |yes |
|  requestPermission(): void  | 在 Android 6.0 及以上的系统上,需要去请求一些用到的权限  | function  | no | Android   |no |
|  stopPush(): void  | 停止推送服务  | function  | no | Android      |yes |
|  resumePush(): void  | 恢复推送服务  | function  | no | iAndroid      |yes |
|  isPushStopped(callback: Callback<boolean>): void | 用来检查 Push Service 是否已经被停止  | function  | no | Android      |yes |
|  setPushTime(params: {pushTimeDays: number[];pushTimeStartHour: number;pushTimeEndHour: number;}):void  | 设置允许推送时间  | function  | no | Android      |no |
|  setSilenceTime(params: {silenceTimeStartHour: number;silenceTimeStartMinute: number;silenceTimeEndHour: number; silenceTimeEndMinute: number;}): void | 设置保留最近通知条数  | function  | no | Android    |no |
|  setLatestNotificationNumber(params: {notificationMaxNumber: number;}): void  |   设置保留最近通知条数   |function   | no | Android      | no |
|  setChannel(params: { channel: string }): void  |   动态配置 channel,优先级比 AndroidManifest 里配置的高   |function   | no | Android      | no |
|  setBadge(params: {badge: number;appBadge: number;}):void  |   设置 Badge   |function   | no | iOS,Android     | yes |
|  setChannelAndSound(params: {channel:string;sound:string;channelId:string}):void  |   设置通知渠道声音   |function   | no | Android     | no |
|  setLinkMergeEnable(enable:boolean):void |   是否开启通知合并   |function   | no | Android     | no |
|  setSmartPushEnable(enable:boolean):void |   是否开启智能推送   |function   | no | iOS,Android     | no |
|  setGeofenceEnable(enable:boolean):void |   是否开启地理围栏   |function   | no |Android     | no |
|  setCollectControl(enable:boolean):void |   是否开启集中控制   |function   | no | iOS、Android     | no |

## 遗留问题
- [ ] setProperties、deleteProperties、cleanProperties、pageEnterTo、pageLeave、initCrashHandler、setMaxGeofenceNumber、deleteGeofence、addNotificationListener、addInappMessageListener，setCollectControl、setSmartPushEnable这些方法在极光推送harmonyOS-SDK中暂未支持[issue#1](https://github.com/react-native-oh-library/jpush-react-native/issues/1)

## 其他


## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/jpush/jpush-react-native/blob/master/LICENSE) ，请自由地享受和参与开源。