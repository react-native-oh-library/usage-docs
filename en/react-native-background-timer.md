> Template version: v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-background-timer</code> </h1>
</p>

This project is based on [react-native-background-timer@2.4.1](https://github.com/ocetnik/react-native-background-timer)。

This third-party library has been migrated to Gitee and is now available for direct download from npm, the new package name is: `@react-native-ohos/react-native-linear-gradient`, The version correspondence details are as follows:

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 2.4.1-0.0.2@deprecated | @react-native-oh-tpl/react-native-background-timer | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-background-timer) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-background-timer/releases) |
| > 2.4.2                   | @react-native-ohos/react-native-background-timer   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/releases) |

## 1. Installation and Usage

Go to the project directory and execute the following instruction:

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-ohos/react-native-background-timer
```

#### **yarn**

```bash
yarn add @react-native-ohos/react-native-background-timer
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

## 2. Manual Link

This step provides guidance for manually configuring native dependencies.

Open the `harmony` directory of the HarmonyOS project in DevEco Studio.

### 2.1 Overrides RN SDK

To ensure the project relies on the same version of the RN SDK, you need to add an `overrides` field in the project's root `oh-package.json5` file, specifying the RN SDK version to be used. The replacement version can be a specific version number, a semver range, or a locally available HAR package or source directory.

For more information about the purpose of this field, please refer to the [official documentation](https://developer.huawei.com/consumer/en/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#en-us_topic_0000001792256137_overrides).

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm version
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // a locally available HAR package
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // source code directory
  }
}
```

### 2.2 Introducing Native Code

Currently, two methods are available:

- Use the HAR file.
- Directly link to the source code。

Method 1 (recommended): Use the HAR file.

> [!TIP] The HAR file is stored in the `harmony` directory in the installation path of the third-party library.

Open `entry/oh-package.json5` file and add the following dependencies:

```json
"dependencies": {
    "@react-native-ohos/react-native-background-timer": "file:../../node_modules/@react-native-ohos/react-native-background-timer/harmony/background_timer.har"
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

### 2.3 Configuring CMakeLists and Introducing BackgroundTimerPackage

> [!TIP] Version v2.4.2 and above requires.

Open `entry/src/main/cpp/CMakeLists.txt` and add the following code:

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-background-timer/src/main/cpp" ./background_timer)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_background_timer)
# RNOH_END: manual_package_linking_2
```

Open `entry/src/main/cpp/PackageProvider.cpp` and add the following code:

```diff
#include "RNOH/PackageProvider.h"
#include "generated/RNOHGeneratedPackage.h"
+ #include "BackgroundTimerPackage.h"

using namespace rnoh;

std::vector<std::shared_ptr<Package>> PackageProvider::getPackages(Package::Context ctx) {
    return {
        std::make_shared<RNOHGeneratedPackage>(ctx),
+       std::make_shared<BackgroundTimerPackage>(ctx),
    };
}
```

### 2.4. Introducing BackgroundTimerPackage to ArkTS

Open the `entry/src/main/ets/RNPackagesFactory.ts` file and add the following code:

```diff
  ...
+ import { BackgroundTimerTurboModulePackage } from '@react-native-ohos/react-native-background-timer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new BackgroundTimerTurboModulePackage(ctx)
  ];
}
```

### 2.5 Running

Click the `sync` button in the upper right corner.

Alternatively, run the following instruction on the terminal:

```bash
cd entry
ohpm install
```

Then build and run the code.

## 3. Constraints

### 3.1 Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-ohos/react-native-background-timer Releases](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/releases)

This document is verified based on the following versions:

RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;

## 4. APIs 

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

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

## 5. Known Issues

- [ ] 使用 worker 开的新线程中不支持 RNOHContext 序列化传参，底层 OS 暂不支持，导致无法在新线程中发送事件，需要底层 OS 框架实现相关业务功能。不开线程的情况下，因 setTimeout 属于异步方法，定时器效果不受影响。[worker 线程 Known Issues:start 和 stop 接口， HarmonyOS RN 框架暂不支持](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/issues/IB8QGJ)

## 6. Others


## 7. License

This project is licensed under (https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/blob/master/LICENSE).

