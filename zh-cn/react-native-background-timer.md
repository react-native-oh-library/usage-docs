
> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-background-timer</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/ocetnik/react-native-background-timer">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/ocetnik/react-native-background-timer/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-background-timer)


## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-background-timer Releases](https://github.com/react-native-oh-library/react-native-background-timer/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

> [!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-background-timer@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-background-timer@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```js
import {View, Button, StyleSheet, Text,TextInput} from 'react-native';
import React, {useState} from 'react';
import BackgroundTimer from "react-native-background-timer";
export function BackgroundTimerExample() {
  let [count, setCount] = useState(0);
  let [text, setText] = useState("");
  // BackgroundTimer延时
  let [delay, setDelay] = useState("1000");
  // setTimeout延时
  let [timeoutDelay, setTimeoutDelay] = useState("1000");
  // setInterval延时
  let [intervalDelay, setIntervalDelay] = useState("1000");
  let timeoutList:number[] = []
  let [intervalList, setIntervalList] = useState<number[]>([]);
 
  // runBackgroundTimer
  function onPressStart(){
    setText("开启定时器...")
    BackgroundTimer.runBackgroundTimer(()=>{
      setCount(count+=1)
    },parseInt(delay))
  }
  function onPressStop(){
    setText("结束定时器")
    BackgroundTimer.stopBackgroundTimer()
  }

  // setTimeout
  function setTimeoutStart(){
    setText("开启定时器...")
    let timeoutId = BackgroundTimer.setTimeout(()=>{
      setCount(count+=1)
    },parseInt(timeoutDelay))
    timeoutList.push(timeoutId)
  }
  function setTimeoutStop(){
    setText("结束定时器")
    if(timeoutList.length>0){
      BackgroundTimer.clearTimeout(timeoutList[0])
      timeoutList.shift()
    }
  }

  // setInterval
  function setIntervalStart(){
    setText("开启定时器...")
    let intervalId = BackgroundTimer.setInterval(()=>{
      setCount(count+=1)
    },parseInt(intervalDelay))
    setIntervalList([...intervalList,intervalId])
  }
  function setIntervalStop(){
    setText("结束定时器")
    if(intervalList.length>0){
      BackgroundTimer.clearInterval(intervalList[0])
      intervalList.shift()
    }
  }
  function resetNumber(){
    setCount(0)
    setText("")
  }
  return (
    <View style={{flexDirection: 'column', flex: 1,backgroundColor:'white'}}>
      <View style={styles.container}>
        <View style={styles.viewStyle}>
          <Button
            onPress={onPressStart}
            title="runBackgroundTimer"
          />
          <TextInput
            style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
            placeholder="BackgroundTimer延时"
            onChangeText={(value)=>{setDelay(value)}}
            value={delay}
          />
        </View>
        <View style={[styles.viewStyle]}>
          <Button
            onPress={onPressStop}
            title="stopBackgroundTimer"
          />
        </View>
      </View>
      
      <View style={styles.container}>
        <View style={styles.viewStyle}>
          <Button
            onPress={setTimeoutStart}
            title="setTimeout"
          />
          <TextInput
            style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
            placeholder="setTimeout延时"
            onChangeText={(value)=>{setTimeoutDelay(value)}}
            value={timeoutDelay}
          />
        </View>
        <View style={[styles.viewStyle]}>
          <Button
            onPress={setTimeoutStop}
            title="clearTimeout"
          />
        </View>
      </View>
      
      <View style={styles.container}>
        <View style={styles.viewStyle}>
          <Button
            onPress={setIntervalStart}
            title="setInterval"
          />
          <TextInput
            style={{ height: 40, borderColor: 'gray', borderWidth: 1 }}
            placeholder="setInterval延时"
            onChangeText={(value)=>{setIntervalDelay(value)}}
            value={intervalDelay}
          />
        </View>
        <View style={[styles.viewStyle]}>
          <Button
            onPress={setIntervalStop}
            title="clearInterval"
          />
        </View>
      </View>
      
      <View style={[styles.viewStyle,styles.resetStyle]}>
        <Button
          onPress={resetNumber}
          title="Reset"
        />
      </View>
      <Text style={styles.textStyle}>{count}</Text>
      <Text style={styles.textStyle}>{text}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    borderColor: 'black',
    borderTopWidth: 0,
    borderBottomWidth: 5,
    borderLeftWidth: 0,
    borderRightWidth: 0,
    padding: 10,
  },
  resetStyle: {
    paddingTop: 10,
  },
  viewStyle:{
    marginBottom: 10,
  },
  textStyle: {
    fontSize: 30,
  },
});


```
<!-- {% endraw %} -->

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

### 在工程根目录的 `oh-package.json` 添加 overrides字段

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
    "@react-native-oh-tpl/react-native-background-timer": "file:../../node_modules/@react-native-oh-tpl/react-native-background-timer/harmony/background_timer.har"
  }
```

点击右上角的 `sync` 按钮

或者在终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 源码位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-background-timer": "file:../../node_modules/@react-native-oh-tpl/react-native-background-timer/harmony/background_timer"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 BackgroundTimerTurboModulePackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
import { BackgroundTimerTurboModulePackage } from '@react-native-oh-tpl/react-native-background-timer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [new SamplePackage(ctx), new BackgroundTimerTurboModulePackage(ctx)];
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-background-timer Releases](https://github.com/react-native-oh-library/react-native-background-timer/releases)


本文档内容基于以下版本验证通过：


RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.19;


## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | -------- | -------- | ------------------ |
| runBackgroundTimer  | 开启定时器，以固定的时间间隔重复执行指定代码     | no | all      | yes |
| stopBackgroundTimer  | 结束runBackgroundTimer开启的定时器     | no | all      | yes |
| start  | 后台开启新任务     | no | all     | no |
| stop  | 结束后台任务    | no | all      | no |
| setTimeout  | 开启定时器，定时器到期会执行指定代码，只会执行一次     | no | Android      | yes |
| clearTimeout  | 结束setTimeout开启的定时器          | no | Android      | yes |
| setInterval  | 开启定时器，以固定的时间间隔重复执行指定代码         | no | Android      | yes |
| clearInterval  | 结束setInterval开启的定时器           | no | Android      | yes |

## 遗留问题

- [ ] 使用worker开的新线程中不支持RNOHContext序列化传参，底层OS暂不支持，导致无法在新线程中发送事件，需要底层OS框架实现相关业务功能。不开线程的情况下，因setTimeout属于异步方法，定时器效果不受影响。[worker线程遗留问题:start和stop接口， HarmonyOS RN框架暂不支持](https://github.com/react-native-oh-library/react-native-background-timer/issues/3)

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/ocetnik/react-native-background-timer/blob/master/LICENSE) ，请自由地享受和参与开源。
