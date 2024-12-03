> 模板版本：v0.3.0

<p align="center">
  <h1 align="center"> <code>react-native-background-timer</code> </h1>
</p>

本项目基于 [react-native-background-timer@2.4.1](https://github.com/ocetnik/react-native-background-timer) 开发。

该第三方库的仓库已迁移至 Gitee，且支持直接从 npm 下载，新的包名为：`@react-native-ohos/react-native-background-timer`，具体版本所属关系如下：

| Version                   | Package Name                                      | Repository         | Release                    |
| ------------------------- | ------------------------------------------------- | ------------------ | -------------------------- |
| <= 2.4.1-0.0.2@deprecated | @react-native-oh-tpl/react-native-background-timer | [Github(deprecated)](https://github.com/react-native-oh-library/react-native-background-timer) | [Github Releases(deprecated)](https://github.com/react-native-oh-library/react-native-background-timer/releases) |
| > 2.4.2                   | @react-native-ohos/react-native-background-timer   | [Gitee](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer) | [Gitee Releases](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/releases) |

## 1. 安装与使用

进入到工程目录并输入以下命令：

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

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

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

此步骤为手动配置原生依赖项的指导。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`。

### 2.1 Overrides RN SDK

为了让工程依赖同一个版本的 RN SDK，需要在工程根目录的 `oh-package.json5` 添加 overrides 字段，指向工程需要使用的 RN SDK 版本。替换的版本既可以是一个具体的版本号，也可以是一个模糊版本，还可以是本地存在的 HAR 包或源码目录。

关于该字段的作用请阅读[官方说明](https://developer.huawei.com/consumer/cn/doc/harmonyos-guides-V5/ide-oh-package-json5-V5#zh-cn_topic_0000001792256137_overrides)

```json
{
  "overrides": {
    "@rnoh/react-native-openharmony": "^0.72.38" // ohpm 在线版本
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony.har" // 指向本地 har 包的路径
    // "@rnoh/react-native-openharmony" : "./react_native_openharmony" // 指向源码路径
  }
}
```

### 2.2 引入原生端代码

目前有两种方法：

- 通过 har 包引入；
- 直接链接源码。

方法一：通过 har 包引入（推荐）

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@react-native-ohos/react-native-background-timer": "file:../../node_modules/@react-native-ohos/react-native-background-timer/harmony/background_timer.har"
  }
```

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

方法二：直接链接源码

> [!TIP] 如需使用直接链接源码，请参考[直接链接源码说明](/zh-cn/link-source-code.md)

### 2.3 配置 CMakeLists 和引入 BackgroundTimerPackage

> [!TIP] 版本 v2.4.2 及以上需要.

打开 `entry/src/main/cpp/CMakeLists.txt`，添加：

```diff
+ set(OH_MODULES "${CMAKE_CURRENT_SOURCE_DIR}/../../../oh_modules")

# RNOH_BEGIN: manual_package_linking_1
+ add_subdirectory("${OH_MODULES}/@react-native-ohos/react-native-background-timer/src/main/cpp" ./background_timer)
# RNOH_END: manual_package_linking_1

# RNOH_BEGIN: manual_package_linking_2
+ target_link_libraries(rnoh_app PUBLIC rnoh_background_timer)
# RNOH_END: manual_package_linking_2
```

打开 `entry/src/main/cpp/PackageProvider.cpp`，添加：

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

### 2.4 在 ArkTs 侧引入 BackgroundTimerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
  ...
+ import { BackgroundTimerTurboModulePackage } from '@react-native-ohos/react-native-background-timer/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
+   new BackgroundTimerTurboModulePackage(ctx)
  ];
}
```

### 2.5 运行

点击右上角的 `sync` 按钮

或者在命令行终端执行：

```bash
cd entry
ohpm install
```

然后编译、运行即可。

## 3. 约束与限制

### 3.1 兼容性


要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-ohos/react-native-background-timer Releases](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/releases)


本文档内容基于以下版本验证通过：


RNOH: 0.72.38; SDK: HarmonyOS-5.0.0(API12); ROM: 5.0.0.107;


## 4. API

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

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

## 5. 遗留问题

- [ ] 使用worker开的新线程中不支持RNOHContext序列化传参，底层OS暂不支持，导致无法在新线程中发送事件，需要底层OS框架实现相关业务功能。不开线程的情况下，因setTimeout属于异步方法，定时器效果不受影响。[worker线程遗留问题:start和stop接口， HarmonyOS RN框架暂不支持](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/issues/IB8QGJ)

## 6. 其他


## 7. 开源协议

本项目基于 [The MIT License (MIT)](https://gitee.com/openharmony-sig/rntpc_react-native-background-timer/blob/master/LICENSE) ，请自由地享受和参与开源。

