> 模板版本：v0.2.2

<p align="center">
  <h1 align="center"> <code>react-native-safe-modules</code> </h1>
</p>
<p align="center">
    <a href="https://github.com/emilioicai/react-native-safe-modules">
        <img src="https://img.shields.io/badge/platforms-android%20|%20ios%20|%20windows%20|%20harmony%20-lightgrey.svg" alt="Supported platforms" />
    </a>
    <a href="https://github.com/emilioicai/react-native-safe-modules/blob/master/LICENSE">
        <img src="https://img.shields.io/badge/license-MIT-green.svg" alt="License" />
        <!-- <img src="https://img.shields.io/badge/license-Apache-blue.svg" alt="License" /> -->
    </a>
</p>

> [!TIP] [Github 地址](https://github.com/react-native-oh-library/react-native-safe-modules)

## 安装与使用

请到三方库的 Releases 发布地址查看配套的版本信息：[@react-native-oh-tpl/react-native-safe-modules Releases](https://github.com/react-native-oh-library/react-native-safe-modules/releases) 。对于未发布到npm的旧版本，请参考[安装指南](/zh-cn/tgz-usage.md)安装tgz包。

进入到工程目录并输入以下命令：

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-modules
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-modules
```

<!-- tabs:end -->

下面的代码展示了这个库的基本使用场景：

> [!WARNING] 使用时 import 的库名不变。

```js
import React from 'react';
import { View, Button } from 'react-native';
import SafeModule from 'react-native-safe-modules';

const App = () => {
  const myModule = SafeModule.create({
    moduleName: 'MyNativemodule',
    mock: {
      someAPI: () => 'doSomething'
    }
  })
  myModule.someAPI()
  
  const NativeLottieView = SafeModule.component({
    viewName: 'LottieAnimationView',
    mockComponent: View,
  });
  
  return (
    <View style={{ flex: 1, justifyContent: 'center', alignItems: 'center' }}>
      <NativeLottieView
        style={{ backgroundColor: 'red', width: 100, height: 100 }}
      />
    </View>
  );
};

export default App;
```

## 约束与限制

### 兼容性

要使用此库，需要使用正确的 React-Native 和 RNOH 版本。另外，还需要使用配套的 DevEco Studio 和 手机 ROM。

请到三方库相应的 Releases 发布地址查看 Release 配套的版本信息：[@react-native-oh-tpl/react-native-safe-modules Releases](https://github.com/react-native-oh-library/react-native-safe-modules/releases)

## API

### SafeModule.create(options)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| options.moduleName  |     the name, or array of names, to look for the module at on the NativeModules namespace.     | string/string[]  |    yes    |  iOS,Android  |         yes        |
| options.mock  |   The mock implementation of the native module.     | object  |    yes    |  iOS,Android  |         yes        |
| options.getVersion  |   A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.   | Function  |    no    |  iOS,Android  |         yes        |
| options.versionOverrides  |    A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...).    | object  |    no    |  iOS,Android  |         yes        |
| options.isEventEmitter  |   A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.     | boolean  |    no    |  iOS,Android  |         yes        |

### SafeModule.module(options)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

| Name | Description | Type | Required | Platform | HarmonyOS Support  |
| ---- | ----------- | ---- | -------- | -------- | ------------------ |
| options.moduleName  |     the name, or array of names, to look for the module at on the NativeModules namespace.     | string/string[]  |    yes    |  iOS,Android  |         yes        |
| options.mock  |   The mock implementation of the native module.     | object  |    yes    |  iOS,Android  |         yes        |
| options.getVersion  |   A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.   | Function  |    no    |  iOS,Android  |         yes        |
| options.versionOverrides  |    A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...).    | object  |    no    |  iOS,Android  |         yes        |
| options.isEventEmitter  |   A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.     | boolean  |    no    |  iOS,Android  |         yes        |


### SafeModule.component(options)

> [!TIP] "Platform"列表示该属性在原三方库上支持的平台。

> [!TIP] "HarmonyOS Support"列为 yes 表示 HarmonyOS 平台支持该属性；no 则表示不支持；partially 表示部分支持。使用方法跨平台一致，效果对标 iOS 或 Android 的效果。

|              Name              | Description |         Type        | Required | Platform | HarmonyOS Support  |
| ------------------------------ | ----------- | ------------------- | -------- | -------- | ------------------ |
|   options.viewName             |  传入的组件名称  |  string/string[]    |   yes    | iOS,Android |         yes        |
|   options.mockComponent        |  传入一个模拟的组件，当viewName查找不到的时候，component会返回这个模拟的组件  |  React.ComponentType\<T>    |   yes    | iOS,Android |         yes        |
|   options.componentOverrides   |  根据版本获取其中定义的组件，如果和viewName相同，覆盖原生组件的React组件，需要确保返回的React组件是有效的  |  object             |   no     | no         |         no        |
|   options.propOverrides        |  根据版本获取其中定义的组件属性，如果是相同组件的相同属性，根据版本覆盖原生组件的属性，需要确保覆盖的属性在原生组件中存在  |  object             |   no     | no         |         no        |
|   options.mock                 |  原生模块的模拟实现，原生模块中存在什么成员，可使用该属性自己模拟编写  |  object             |   no     | no         |         no        |
|   options.getVersion           |  返回本机模块版本的函数。仅在指定替代且不导出本机模块上的版本属性时才需要。默认值为x => x.VERSION。  |  Function           |   no     | no         |         no        |


## 遗留问题

## 其他

- component接口问题： 该接口在iOS和Android上均无法正常使用，不管输入的viewName是什么，都只会返回用户传递的mockComponent，无法获得封装后的组件，HarmonyOS与其表现一致:[issue#19](https://github.com/emilioicai/react-native-safe-modules/issues/19)。

## 开源协议

本项目基于 [The MIT License (MIT)](https://github.com/emilioicai/react-native-safe-modules/blob/master/LICENSE) ，请自由地享受和参与开源。
