> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-module</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/lelandrichardson/react-native-safe-module">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/lelandrichardson/react-native-safe-module/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-safe-module)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-safe-module Releases](https://github.com/react-native-oh-library/react-native-safe-module/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。


进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-module
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-module
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View } from 'react-native';
import SafeModule from 'react-native-safe-module';

const App = () => {
  const NativeLottieView = SafeModule.component({
    viewName: 'LottieAnimationView',
    mockComponent: View,
  });
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <NativeLottieView
        style={{backgroundColor: 'red', width: 100, height: 100}}
      />
    </View>
  );
};

export default App;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-safe-module Releases](https://github.com/react-native-oh-library/react-native-safe-module/releases)

## API

> [!tip] "Platform"列表示该属性在原三方库上支持的平台。

> [!tip] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。


Name | Description | Type | Required | Platform | HarmonyOS   Support
-- | -- | -- | -- | -- | --
SafeModule.create(options) | 创建Module | Object | Yes | iOS/Android | Yes |  


**options**：SafeModule.create(options) 方法的参数

| Name                                                      | Description                                                                                                         | Type     | Required | Platform | HarmonyOS Support |
| --------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | -------- | -------- | -------- | ----------------- |
| options.moduleName                                             |  The name, or array of names, to look for the module at on the NativeModules namespace.                                                                                      | string/Array<string> | Yes       | iOS/Android      | Yes               |
| options.mock                                              | The mock implementation of the native module.                                        | mixed | Yes       | iOS/Android      | Yes               |
| options.getVersion                                | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.                                                                                                  | (module) => string/number | No       | iOS/Android      | Yes                |
| options.overrides                                 | A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...).                                                                                                  | [version: string]: mixed   | No       | iOS/Android      | Yes               |
| options.isEventEmitter                              |  A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.                                                                                                  | bool   | No       | iOS/Android      | Yes                |


## 遗留问题


## 其他

## 开源协议

本项目基于 [MIT License](https://github.com/lelandrichardson/react-native-safe-module/blob/master/LICENSE) ，请自由地享受和参与开源。