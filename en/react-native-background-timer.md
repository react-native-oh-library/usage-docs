> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-background-timer)

## Installation and Usage

Find the matching version information in the release address of a third-party library: [@react-native-oh-tpl/react-native-background-timer Releases](https://github.com/react-native-oh-library/react-native-background-timer/releases).For older versions that are not published to npm, please refer to the [installation guide](/en/tgz-usage-en.md) to install the tgz package.

Go to the project directory and execute the following instruction:



<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-background-timer
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-background-timer
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import {View, Button, StyleSheet, Text,TextInput} from 'react-native';
import React, {useState} from 'react';
import BackgroundTimer from "react-native-background-timer";
export function BackgroundTimerExample() {
  let [count, setCount] = useState(0);
  let [text, setText] = useState("");
  let [delay, setDelay] = useState("1000");
  let [timeoutDelay, setTimeoutDelay] = useState("1000");
  let [intervalDelay, setIntervalDelay] = useState("1000");
  let timeoutList:number[] = []
  let [intervalList, setIntervalList] = useState<number[]>([]);

  // runBackgroundTimer
  function onPressStart(){
    setText("Turn on the timer...")
    BackgroundTimer.runBackgroundTimer(()=>{
      setCount(count+=1)
    },parseInt(delay))
  }
  function onPressStop(){
    setText("Turn off the timer")
    BackgroundTimer.stopBackgroundTimer()
  }

  // setTimeout
  function setTimeoutStart(){
    setText("Turn on the timer...")
    let timeoutId = BackgroundTimer.setTimeout(()=>{
      setCount(count+=1)
    },parseInt(timeoutDelay))
    timeoutList.push(timeoutId)
  }
  function setTimeoutStop(){
    setText("Turn off the timer")
    if(timeoutList.length>0){
      BackgroundTimer.clearTimeout(timeoutList[0])
      timeoutList.shift()
    }
  }

  // setInterval
  function setIntervalStart(){
    setText("Turn on the timer...")
    let intervalId = BackgroundTimer.setInterval(()=>{
      setCount(count+=1)
    },parseInt(intervalDelay))
    setIntervalList([...intervalList,intervalId])
  }
  function setIntervalStop(){
    setText("Turn off the timer")
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
            placeholder="BackgroundTimer delay"
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
            placeholder="setTimeout delay"
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

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-background-timer": "file:../../node_modules/@react-native-oh-tpl/react-native-background-timer/harmony/background_timer.har"
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

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/react-native-background-timer": "file:../../node_modules/@react-native-oh-tpl/react-native-background-timer/harmony/background_timer"
  }
```

Opening the terminal and executing:

```bash
cd entry
ohpm install --no-link
```

### 3. Introducing BackgroundTimerTurboModulePackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { BackgroundTimerTurboModulePackage } from '@react-native-oh-tpl/react-native-background-timer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new BackgroundTimerTurboModulePackage(ctx)
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

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-background-timer Releases](https://github.com/react-native-oh-library/react-native-background-timer/releases)

This document is verified based on the following versions:

RNOH: 0.72.20; SDK: HarmonyOS NEXT Developer Beta1 B.0.18; IDE: DevEco Studio 5.0.3.200; ROM: 3.0.0.19;

## API

> [!tip] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!tip] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                | Description                                        | Required | Platform | HarmonyOS Support |
| ------------------- | -------------------------------------------------- | -------- | -------- | ----------------- |
| runBackgroundTimer  | 开启定时器，以固定的时间间隔重复执行指定代码       | no       | all      | yes               |
| stopBackgroundTimer | 结束 runBackgroundTimer 开启的定时器               | no       | all      | yes               |
| start               | 后台开启新任务                                     | no       | all      | no                |
| stop                | 结束后台任务                                       | no       | all      | no                |
| setTimeout          | 开启定时器，定时器到期会执行指定代码，只会执行一次 | no       | Android  | yes               |
| clearTimeout        | 结束 setTimeout 开启的定时器                       | no       | Android  | yes               |
| setInterval         | 开启定时器，以固定的时间间隔重复执行指定代码       | no       | Android  | yes               |
| clearInterval       | 结束 setInterval 开启的定时器                      | no       | Android  | yes               |

## Known Issues

- [ ] 使用 worker 开的新线程中不支持 RNOHContext 序列化传参，底层 OS 暂不支持，导致无法在新线程中发送事件，需要底层 OS 框架实现相关业务功能。不开线程的情况下，因 setTimeout 属于异步方法，定时器效果不受影响。[worker 线程 Known Issues:start 和 stop 接口， HarmonyOS RN 框架暂不支持](https://github.com/react-native-oh-library/react-native-background-timer/issues/3)

## Others

## License

This project is licensed under [The MIT License (MIT)](https://github.com/ocetnik/react-native-background-timer/blob/master/LICENSE).
