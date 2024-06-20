> 模板版本：v0.2.1

<p align="center">
  <h1 align="center"> <code>react-native-orientation-locker</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/wonday/react-native-orientation-locker">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/wonday/react-native-orientation-locker/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-orientation-locker)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-library/react-native-orientation-locker Releases](https://github.com/react-native-oh-library/react-native-orientation-locker/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-orientation-locker@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-orientation-locker@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

<!-- {% raw %} -->
```tsx

import {
  Alert,
  Button,
  StyleSheet,
  Text,
  TouchableOpacity,
  View,
} from 'react-native';
import {useCallback, useEffect, useState} from 'react';
import Orientation, {
  OrientationLocker,
  PORTRAIT,
  LANDSCAPE,
  useOrientationChange,
  useDeviceOrientationChange,
  useLockListener,
} from 'react-native-orientation-locker';

export function OrientationLockerExample() {
  const [showVideo, setShowVideo] = useState(true);
  const [orientation, setOrientation] = useState<string>();
  const [isLock, setIsLock] = useState<boolean>(false);
  const updateOrientation = (orientation: string) => {
    console.info('---orientation-----22222', orientation);
    setOrientation(orientation);
  };

  const updateDeviceOrientation = (orientation: string) => {
    console.info('---updateDeviceOrientation-----1111111', orientation);
    setOrientation(orientation);
  };

  const updateLock = (orientation: string) => {
    console.info('---updateLock-----', orientation);
  };

  useEffect(() => {
    // 开启方向变化的监听
    getOrientationInt();
  }, []);


  //获取方向
  const getOrientationInt = () => {
    Orientation.getOrientation((orientation: string) => {
      updateOrientation(orientation);
      if (orientation) {
        Alert.alert(`当前屏幕方向为${orientation}`);
      } else {
        Alert.alert('获取当前屏幕方向失败');
      }
    });
  };

  // 锁定方向为纵向（竖屏）
  const setLockToPortrait = () => {
    Orientation.lockToPortrait();
  };
  // 锁定方向为横向（横屏）
  const setLockToLandscape = () => {
    Orientation.lockToLandscape();
  };
  // 锁定方向为横向，并且是向左旋转的方向
  const setLockToLandscapeLeft = () => {
    Orientation.lockToLandscapeLeft();
  };
  // 锁定方向为横向，并且是向右旋转的方向
  const setLockToLandscapeRight = () => {
    Orientation.lockToLandscapeRight();
  };
  // 解除方向的锁定，允许自由旋转
  const unlockAllOrientations = () => {
    Orientation.unlockAllOrientations();
  };

  // 锁定上下的方向
  const lockToPortraitUpsideDown = () => {
    Orientation.lockToPortraitUpsideDown();
  };

  // 锁定除了上下的所有方向
  const lockToAllOrientationsButUpsideDown = () => {
    Orientation.lockToAllOrientationsButUpsideDown();
  };
  // 添加监听a
  const addTisten = () => {
    Orientation.addDeviceOrientationListener(updateDeviceOrientation);
  };
  // 取消监听
  const cancelAddTisten = () => {
    Orientation.removeDeviceOrientationListener(updateDeviceOrientation);
  };

  return (
    <View style={styles.container}>
      <Text>{`Current Orientation----: ${orientation}`}</Text>
      <TouchableOpacity
        onPress={lockToPortraitUpsideDown}
        style={styles.button}>
        <Text style={styles.instructions}>锁定上下的方向</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={lockToAllOrientationsButUpsideDown}
        style={styles.button}>
        <Text style={styles.instructions}>锁定除了上下的所有方向</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToPortrait} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为竖屏</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscape} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为横屏</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeLeft} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为横屏,左旋转</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={setLockToLandscapeRight} style={styles.button}>
        <Text style={styles.instructions}>锁定当前屏幕为横屏,右旋转</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={unlockAllOrientations} style={styles.button}>
        <Text style={styles.instructions}>解锁当前屏幕旋转锁定</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={addTisten} style={styles.button}>
        <Text style={styles.instructions}>添加监听</Text>
      </TouchableOpacity>
      <TouchableOpacity onPress={cancelAddTisten} style={styles.button}>
        <Text style={styles.instructions}>取消监听</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'flex-start',
    alignItems: 'center',
    backgroundColor: '#F5FCFF',
    marginTop: 20,
  },
  welcome: {
    fontSize: 20,
    textAlign: 'center',
    margin: 10,
  },
  instructions: {
    textAlign: 'center',
    color: '#eeeeee',
    marginBottom: 0,
  },
  buttonContainer: {
    flex: 0,
    flexDirection: 'row',
    justifyContent: 'space-around',
  },
  button: {
    padding: 5,
    margin: 5,
    borderWidth: 1,
    borderColor: 'white',
    borderRadius: 3,
    backgroundColor: 'grey',
  },
});


```
<!-- {% endraw %} -->

## Link

目前 HarmonyOS 暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的 HarmonyOS 工程 `harmony`

## 在工程根目录的 `oh-package.json` 添加 `overrides`字段

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
    "@react-native-oh-tpl/react-native-orientation-locker":"file：../../node_modules/@react-native-oh-tpl/react-native-orientation-locker/harmony/orientation_locker.har"
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
    "@react-native-oh-tpl/react-native-orientation-locker":"file:../../node_modules/@react-native-oh-tpl/react-native-orientation-locker/harmony/orientation_locker"
  }
```

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 RNOrientationLockerPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNOrientationLockerPackage } from '@react-native-oh-tpl/react-native-orientation-locker/ts';
export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOrientationLockerPackage(ctx)
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

然后编译、运行即可。

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-library/react-native-orientation-locker Releases](https://github.com/react-native-oh-library/react-native-orientation-locker/releases)

本文档内容基于以下版本验证通过：

1. RNOH: 0.72.20; SDK：HarmonyOS NEXT Developer Beta1; IDE：DevEco Studio 5.0.3.200; ROM：3.0.0.18;

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-orientation-locker](https://github.com/react-native-oh-library/react-native-orientation-locker)

| Name | Description | Type | Required | Platform | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | ------------------------  | ---------------- | ----------------- |
| lockToPortrait   |   Lock the orientation of the application to portrait (portrait)         |  function  | No       | IOS/Android | yes               |
| lockToLandscape  |    Lock the orientation of the application to landscape (landscape)         | function | No       | IOS/Android | yes               |
| lockToLandscapeLeft  | Lock the orientation of the app to landscape and rotated to the left         | function | No       | IOS/Android | yes               |
| lockToLandscapeRight  | Lock the orientation of the app to landscape and rotated to the right         | function | No       | IOS/Android | yes               |
| unlockAllOrientations  | Unlocks the orientation of the app, allowing the device to rotate freely          | function | No       | IOS/Android | yes               |
| getOrientation  | Get the direction of the current device        | callback | No       | IOS/Android | yes               |
| getDeviceOrientation  | Obtains the direction of the current device        | callback | No       | IOS/Android | yes               |

## Events

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-orientation-locker](https://github.com/react-native-oh-library/react-native-orientation-locker)

| Name   | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| addOrientationListener  | When UI orientation changed, callback function will be called. But if lockToXXX is called , callback function will be not called untill unlockAllOrientations. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN When lockToXXX/unlockAllOrientations, it will force resend UI orientation changed event.| callback | No       | IOS/Android | yes               |
| addDeviceOrientationListener  | When device orientation changed, callback function will be called. When lockToXXX is called, callback function also can be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT PORTRAIT-UPSIDEDOWN UNKNOWN | callback | No       | IOS/Android | yes               |
| removeOrientationListener  |    | callback | No       | IOS/Android | yes               |
| removeDeviceOrientationListener  |         | callback | No       | IOS/Android | yes               |
| addLockListener  | When call lockToXXX/unlockAllOrientations, callback function will be called. It can return either PORTRAIT LANDSCAPE-LEFT LANDSCAPE-RIGHT UNKNOWN UNKNOWN means not be locked. | callback | No       | IOS/Android | yes               |
| removeLockListener  |     | callback | No       | IOS/Android | yes              |
| removeAllListeners  |       | callback | No       | IOS/Android | yes              |

## 其他

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/wonday/react-native-orientation-locker/blob/master/LICENSE) ，请自由地享受和参与开源。