> 模板版本：v0.2.0

<p align="center">
  <h1 align="center"> <code>react-native-orientation</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/yamill/react-native-orientation">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/react-native-oh-library/react-native-orientation/blob/sig/LICENSE.md">
        <img src="https://img.shields.io/badge/license-ISC-green.svg" alt="License" />
    </a>
   
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-orientation)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[<@react-native-oh-library/react-native-orientation> Releases](https://github.com/react-native-oh-library/react-native-orientation/releases)，并下载适用版本的 tgz 包。

进入到工程目录并输入以下命令：

>[!TIP] # 处替换为 tgz 包的路径

<!-- tabs:start -->

####  npm

```bash
npm install @react-native-oh-tpl/react-native-orientation@file:#
```

#### yarn

```bash
yarn add @react-native-oh-tpl/react-native-orientation@file:#
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

>[!WARNING] 使用时 import 的库名不变。

```tsx

import Orientation from 'react-native-orientation';
import {Alert, StyleSheet, Text, TouchableOpacity, View} from 'react-native';
import {useEffect, useState} from 'react';

export default function OrientationDemo() {
  const [orientation, setOrientation] = useState<string>();
  const [SpecificOrientation, setSpecificOrientation] = useState<string>();
  const updateOrientation = (orientation: string) => {
    console.info('orientation', orientation);
    setOrientation(orientation);
  };
  const UpdateSpecificOrientation = (SpecificOrientation: string) => {
    console.info('SpecificOrientation', SpecificOrientation);
    setSpecificOrientation(SpecificOrientation);
  };
  useEffect(() => {
    // 开启方向变化的监听
    Orientation.addOrientationListener(updateOrientation);
    Orientation.addSpecificOrientationListener(UpdateSpecificOrientation);
    return () => {
     // 移除方向变化的监听
      Orientation.removeOrientationListener(updateOrientation);
      Orientation.removeSpecificOrientationListener(UpdateSpecificOrientation);
    };
  }, []);
  // 获取方向
  const getOrientationInt = () => {
    Orientation.getOrientation((err: string, orientation: string) => {
      if (orientation) {
        Alert.alert(`当前屏幕方向为${orientation}`);
      } else {
        Alert.alert(err);
      }
    });
  };
  // 获取具体方向
  const getSpecificOrientationInt = () => {
    Orientation.getSpecificOrientation((err: string, orientation: string) => {
      if (orientation) {
        Alert.alert(`当前屏幕方向为${orientation}`);
      } else {
        Alert.alert(err);
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
  return (
    <View style={styles.container}>
      <Text>{`Current Orientation: ${orientation}`}</Text>
      <Text>{`Current SpecificOrientation: ${SpecificOrientation}`}</Text>
      <TouchableOpacity onPress={getOrientationInt} style={styles.button}>
        <Text style={styles.instructions}>获取当前屏幕的方向</Text>
      </TouchableOpacity>
      <TouchableOpacity
        onPress={getSpecificOrientationInt}
        style={styles.button}>
        <Text style={styles.instructions}>获取当前屏幕具体的方向</Text>
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

## Link

目前鸿蒙暂不支持 AutoLink，所以 Link 步骤需要手动配置。

首先需要使用 DevEco Studio 打开项目里的鸿蒙工程 `harmony`

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

1. 通过 har 包引入（在 IDE 完善相关功能后该方法会被遗弃，目前首选此方法）;
2. 直接链接源码。

方法一：通过 har 包引入

> [!TIP] har 包位于三方库安装路径的 `harmony` 文件夹下。

打开 `entry/oh-package.json5`，添加以下依赖

```json
"dependencies": {
    "@rnoh/react-native-openharmony": "file:../react_native_openharmony",
    "@react-native-oh-tpl/rnoh-orientation": "file:../../node_modules/@react-native-oh-tpl/react-native-orientation/harmony/rn_orientation.har"
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

打开终端，执行：

```bash
cd entry
ohpm install --no-link
```

### 在 ArkTs 侧引入 SoundPackage

打开 `entry/src/main/ets/RNPackagesFactory.ts`，添加：

```diff
...
+ import { RNOrientationPackage } from '@react-native-oh-tpl/rnoh-orientation/ts';

export function createRNPackages(ctx: RNPackageContext): RNPackage[] {
  return [
    new SamplePackage(ctx),
+   new RNOrientationPackage(ctx)
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

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[<@react-native-oh-library/react-native-orientation> Releases](https://github.com/react-native-oh-library/react-native-orientation/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-orientation](https://github.com/react-native-oh-library/react-native-orientation)

| Name           | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| lockToPortrait  | Lock the orientation of the application to portrait (portrait)         | function | No       | IOS/Android | yes               |
| lockToLandscape  | Lock the orientation of the application to landscape (landscape)         | function | No       | IOS/Android | yes               |
| lockToLandscapeLeft  | Lock the orientation of the app to landscape and rotated to the left         | function | No       | IOS/Android | yes               |
| lockToLandscapeRight  | Lock the orientation of the app to landscape and rotated to the right         | function | No       | IOS/Android | yes               |
| unlockAllOrientations  | Unlocks the orientation of the app, allowing the device to rotate freely          | function | No       | IOS/Android | yes               |
| getOrientation  | Get the direction of the current device        | callback | No       | IOS/Android | yes               |
| getSpecificOrientation  | Obtains the direction of the current device        | callback | No       | IOS/Android | yes               |

## Events

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

详情请见[react-native-orientation](https://github.com/react-native-oh-library/react-native-orientation)

| Name           | Description                              | Type   | Required | Platform    | HarmonyOS Support |
| -------------- | ---------------------------------------- | ------ | -------- | ----------- | ----------------- |
| addOrientationListener  | Enable monitoring of screen orientation changes         | callback | No       | IOS/Android | yes               |
| addSpecificOrientationListener  | Start to monitor the change of screen orientation | callback | No       | IOS/Android | yes               |
| removeOrientationListener  | Remove Listen Screen Orientation Change    | callback | No       | IOS/Android | yes               |
| removeSpecificOrientationListener  | Remove Monitor Screen Specific Orientation Change        | callback | No       | IOS/Android | yes               |
## 其他

## 开源协议

本项目基于 [ISC License](https://github.com/react-native-oh-library/react-native-orientation/blob/master/LICENSE) ，请自由地享受和参与开源。