> Template version: v0.2.2

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

> [!TIP] [GitHub address](https://github.com/react-native-oh-library/react-native-safe-modules)

## Installation and Usage

Find the matching version information in the release address of a third-party library and download an applicable .tgz package: [@react-native-oh-tpl/react-native-safe-modules Releases](https://github.com/react-native-oh-library/react-native-safe-modules/releases).

Go to the project directory and execute the following instruction:

> [!TIP] Replace the content with the path of the .tgz package at the comment sign (#).

<!-- tabs:start -->

#### **npm**

```bash
npm install @react-native-oh-tpl/react-native-safe-modules@file:#
```

#### **yarn**

```bash
yarn add @react-native-oh-tpl/react-native-safe-modules@file:#
```

<!-- tabs:end -->

The following code shows the basic use scenario of the repository:

> [!WARNING] The name of the imported repository remains unchanged.

```js
import React from "react";
import { View, Button } from "react-native";
import SafeModule from "react-native-safe-modules";

const App = () => {
  const myModule = SafeModule.create({
    moduleName: "MyNativemodule",
    mock: {
      someAPI: () => "doSomething",
    },
  });
  myModule.someAPI();

  const NativeLottieView = SafeModule.component({
    viewName: "LottieAnimationView",
    mockComponent: View,
  });

  return (
    <View style={{ flex: 1, justifyContent: "center", alignItems: "center" }}>
      <NativeLottieView
        style={{ backgroundColor: "red", width: 100, height: 100 }}
      />
    </View>
  );
};

export default App;
```

## Constraints

### Compatibility

To use this repository, you need to use the correct React-Native and RNOH versions. In addition, you need to use DevEco Studio and the ROM on your phone.

Check the release version information in the release address of the third-party library: [@react-native-oh-tpl/react-native-safe-modules Releases](https://github.com/react-native-oh-library/react-native-safe-modules/releases)

## API

### SafeModule.create(options)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                                                                                                                                                                                                                                                                                                                                                                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- | -------- | ----------- | ----------------- |
| options.moduleName       | the name, or array of names, to look for the module at on the NativeModules namespace.                                                                                                                                                                                                                                                                                                                       | string/string[] | yes      | iOS,Android | yes               |
| options.mock             | The mock implementation of the native module.                                                                                                                                                                                                                                                                                                                                                                | object          | yes      | iOS,Android | yes               |
| options.getVersion       | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.                                                                                                                                                                                                                | Function        | no       | iOS,Android | yes               |
| options.versionOverrides | A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...). | object          | no       | iOS,Android | yes               |
| options.isEventEmitter   | A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.                                                                                                                                                                                                                               | boolean         | no       | iOS,Android | yes               |

### SafeModule.module(options)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                     | Description                                                                                                                                                                                                                                                                                                                                                                                                  | Type            | Required | Platform    | HarmonyOS Support |
| ------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | --------------- | -------- | ----------- | ----------------- |
| options.moduleName       | the name, or array of names, to look for the module at on the NativeModules namespace.                                                                                                                                                                                                                                                                                                                       | string/string[] | yes      | iOS,Android | yes               |
| options.mock             | The mock implementation of the native module.                                                                                                                                                                                                                                                                                                                                                                | object          | yes      | iOS,Android | yes               |
| options.getVersion       | A function that returns the version of the native module. Only needed if you are specifying overrides and not exporting a VERSION property on your native module. Defaults to x => x.VERSION.                                                                                                                                                                                                                | Function        | no       | iOS,Android | yes               |
| options.versionOverrides | A map of version numbers to overridden implementations of the corresponding property/method. If an overridden property or method is a function, it will be called during SafeModule.create(...) with two arguments, the original value of that property on the original module, and the original module itself. The return value of this function will be put on the return value of SafeModule.create(...). | object          | no       | iOS,Android | yes               |
| options.isEventEmitter   | A flag indicating that the native module is expected to be an EventEmitter. Puts the EventEmitter instance on the emitter property of the resulting module. Defaults to false.                                                                                                                                                                                                                               | boolean         | no       | iOS,Android | yes               |

### SafeModule.component(options)

> [!TIP] The **Platform** column indicates the platform where the properties are supported in the original third-party library.

> [!TIP] If the value of **HarmonyOS Support** is **yes**, it means that the HarmonyOS platform supports this property; **no** means the opposite; **partially** means some capabilities of this property are supported. The usage method is the same on different platforms and the effect is the same as that of iOS or Android.

| Name                       | Description                                                                                                                                           | Type                    | Required | Platform    | HarmonyOS Support |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------- | -------- | ----------- | ----------------- |
| options.viewName           | 传入的组件名称                                                                                                                                        | string/string[]         | yes      | iOS,Android | yes               |
| options.mockComponent      | 传入一个模拟的组件，当 viewName 查找不到的时候，component 会返回这个模拟的组件                                                                        | React.ComponentType\<T> | yes      | iOS,Android | yes               |
| options.componentOverrides | 根据版本获取其中定义的组件，如果和 viewName 相同，覆盖原生组件的 React 组件，需要确保返回的 React 组件是有效的                                        | object                  | no       | no          | no                |
| options.propOverrides      | 根据版本获取其中定义的组件 Properties，如果是相同组件的相同 Properties，根据版本覆盖原生组件的 Properties，需要确保覆盖的 Properties 在原生组件中存在 | object                  | no       | no          | no                |
| options.mock               | 原生模块的模拟实现，原生模块中存在什么成员，可使用该 Properties 自己模拟编写                                                                          | object                  | no       | no          | no                |
| options.getVersion         | 返回本机模块版本的函数。仅在指定替代且不导出本机模块上的版本 Properties 时才需要。默认值为 x => x.VERSION。                                           | Function                | no       | no          | no                |

## Known Issues

## Others

- component 接口问题： 该接口在 iOS 和 Android 上均无法正常使用，不管输入的 viewName 是什么，都只会返回用户传递的 mockComponent，无法获得封装后的组件，HarmonyOS 与其表现一致:[issue#19](https://github.com/emilioicai/react-native-safe-modules/issues/19)。

## License

This project is licensed under [The MIT License (MIT)](https://github.com/emilioicai/react-native-safe-modules/blob/master/LICENSE).
